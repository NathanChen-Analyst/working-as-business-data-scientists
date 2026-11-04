# Technical craft

*Executing analytical work correctly and reproducibly: SQL and the data platform it runs on, a programming language for what SQL cannot do, the statistics and experiment mechanics behind the methods, and the tooling that turns a result into something others can see and reuse.*

**On this page:** [Why it matters](#why-it-matters) · [Where it shows up](#where-it-shows-up-in-the-workflow) · [The toolkit](#the-toolkit) — [SQL & platform](#1-sql-and-the-data-platform) · [Programming](#2-programming-and-reproducibility) · [Statistics](#3-statistics) · [Experiments](#4-experiments-ab-tests) · [Causal methods](#5-causal-inference-without-an-experiment) · [Modelling](#6-modelling) · [Charts](#7-charts-and-dashboards) · [In practice](#in-practice) · [By level](#what-good-looks-like-by-level) · [Interview lens](#interview-lens) · [Resources](#resources)

---

## Why it matters

*What this ability changes about how you work — and why it matters less than people think.*

Craft is the entry ticket. Without it nothing else in this repo can happen, and it is the most-tested thing in analyst interviews. But it is primary in only two of the eight stages, and it is the ability AI agents have changed most: producing fluent code is now cheap, while specifying it and checking it is not.

> **The one thing to remember:** craft today means knowing what *correct* looks like well enough to check it — more than typing it fast.

---

## Where it shows up in the workflow

*Primary in Stages 4 and 5; supporting in Stage 3 and 6.*

| Stage | What it looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Knowing what data exists and roughly what it can answer | ○ |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Knowing whether the tracking can tell the branches of the issue tree apart | ○ |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Computing variance and the smallest effect you could detect; knowing how a metric is implemented | ● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | SQL at the right grain; navigating the platform; quality checks; reconciliation | ●● |
| [5 Analyse](../workflow.md#stage-5--analyse) | Statistics, experiment mechanics, causal methods, modelling when warranted | ●● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Sensitivity checks actually run; effect sizes with intervals | ● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Charts that are correct and legible; a dashboard when one is warranted | ○ |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Monitoring queries, alerts, post-launch measurement | ○ |

---

## The toolkit

*Seven groups. Each concept is defined in plain words, with the detail that matters in practice and the trap that catches people. The methods that interviews test most — power, A/B analysis, the causal designs — get the most detail.*

### 1. SQL and the data platform

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Grain** | What one row of a table represents: one order, one order line, one user-day. | Every aggregate has a grain. Decide it before writing the query, and state it in the query's comment. `COUNT(DISTINCT key)` against the raw table tells you if a table's grain is what you think. | The commonest error in all of analytics: aggregating at the wrong level — sessions when you meant users. |
| **Joins and fan-out** | Combining tables on a key. Fan-out is when a one-to-many join multiplies rows. | Check row counts before and after every join. Joining orders to order lines and then summing order value counts each order once per line. | Fan-out is silent. The query runs, the number is wrong, nothing warns you. |
| **Window functions** | Calculations across a set of rows related to the current row, without collapsing them. `ROW_NUMBER`, `RANK`, `LAG`, `LEAD`, `SUM(...) OVER (...)`. | Running totals, first/last event per user, time since previous event, top-N per group. `PARTITION BY` sets the group; `ORDER BY` sets the sequence. | Forgetting the frame clause: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` vs the default `RANGE`, which treats ties differently. |
| **CTEs** | Named sub-queries (`WITH step AS (...)`) that break a query into readable steps. | One CTE per logical step: filter, then join, then aggregate. Each one can be run alone to check its row count. | Chains of eight CTEs that nobody can follow. If a CTE is reused across queries, it should be a model. |
| **Funnel query** | Conversion between ordered steps. | One row per user with a flag per step reached (`MAX(CASE WHEN event = 'x' THEN 1 END)`), then aggregate. Conversion at step *n* = users reaching *n* ÷ users reaching *n-1*. | Counting events instead of users; ignoring step order (a user can hit step 3 without step 2 if tracking misfired). |
| **Retention cohort** | Share of users from a signup period who return in each later period. | Cohort = signup month; period = months since signup; retained = any activity in that period. Pivot to a cohort × period grid. | Mixing calendar months with months-since-signup; counting the signup month as "retained". |
| **Sessionisation** | Grouping events into sessions by inactivity gap. | `LAG(timestamp)` per user → flag a new session when the gap exceeds the timeout (often 30 minutes) → running `SUM` of flags gives the session id. | Timeout choice changes every session metric. State it. |
| **The platform** | Sources → event tracking → warehouse → transformation (dbt) → metrics layer → BI → catalog. | Query the modelled layer, not raw. Read the dbt model and its lineage before trusting a column. Check the load timestamp. Know what a scan costs. The full layer table is in [Stage 4](../workflow.md#stage-4--get-and-trust-the-data). | Reporting a "drop" that is a half-loaded day. |
| **Data-quality checks** | A short script run against any new table. | Row counts by day, null rate per column, duplicate keys, distinct values of categoricals, min/max of dates and amounts, and a reconciliation of the headline number against an independent source (finance, the payments provider, last month's report). | Checking once and never again. Tables change under you. |
| **Event tracking** | Instrumentation that records what users do. | Client-side events can be blocked, duplicated, or renamed in a release; server-side events are more reliable but sparser. Identity: one person, several devices, several ids. | A release renames one event and half your funnel "disappears" — the running example's tracking break. |

### 2. Programming and reproducibility

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Python or R** | For what SQL cannot do cleanly: reshaping, statistics, modelling, charts. | pandas or dplyr for data; statsmodels/scipy or R's base stats for tests; matplotlib/seaborn or ggplot2 for charts. One language fluently beats two badly. | Doing in Python what the warehouse would do faster in SQL. Pull aggregates, not raw rows. |
| **Notebooks** | Jupyter, Hex, Deepnote, Quarto: code, output, and narrative together. | Parameterise dates and ids at the top; pin the data snapshot; restart and run all before sharing. | A notebook that only works because of cells run out of order. |
| **Version control** | Git, for anything reused or reviewed. | Commit per logical change with a message that says why. Code review for anything that reaches a stakeholder. | Analysis code that lives only on one laptop. |
| **Reproducibility** | Someone else can run it and get the same answer. | Fixed random seeds; recorded package versions; data pulled by query, not by hand-exported CSV. | "It worked on my machine" is not an analysis. |

### 3. Statistics

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Distributions and summaries** | The shape of a variable, and the numbers that describe it. | Order value, session length, and revenue per user are right-skewed: the mean sits far above the median, driven by a few large values. Report medians and percentiles alongside means. | Comparing means of skewed metrics with a test that assumes they aren't. |
| **Standard error** | How much a statistic (a mean, a proportion) would vary from sample to sample. | For a mean: *s / √n*. For a proportion: *√(p(1−p)/n)*. Halving the standard error needs four times the sample. | Confusing the standard deviation (spread of the data) with the standard error (precision of the estimate). |
| **Confidence interval** | A range of values for the true quantity that is consistent with the data. | A 95% interval is roughly *estimate ± 2 × standard error*. The width is the honest statement of what you know. | "95% chance the truth is in here" is not what it means, but it is close enough for a memo if you say "plausible range". |
| **Hypothesis test and p-value** | A test asks whether the data would be surprising if there were no effect. The p-value is how surprising. | *p* = probability of a result at least this extreme if the null were true. Small *p* → the null is a poor explanation. It says nothing about the size of the effect or the probability the effect is real. | Treating *p* < 0.05 as proof, *p* > 0.05 as "no effect", and 0.049 as different from 0.051. |
| **Which test** | Matching the test to the metric type. | Means of continuous metrics: Welch's t-test (does not assume equal variance). Proportions (conversion): two-proportion z-test. Ratio metrics (revenue per session, where both numerator and denominator vary per user): the delta method, or bootstrap. Counts: Poisson or negative binomial. | Using a t-test on a ratio metric computed at session level when the randomisation was at user level — the units are not independent. |
| **Power and minimum detectable effect (MDE)** | Power: the chance of detecting a real effect of a given size. MDE: the smallest effect you have a good chance of detecting with a given sample. | Sample per group for a proportion, at 80% power and 5% significance: *n ≈ 16 × p(1−p) / δ²*, where *p* is the baseline rate and *δ* the absolute lift. For *p* = 0.30 and *δ* = 0.02 → *n ≈ 16 × 0.21 / 0.0004 ≈ 8,400* per group. Compute this in Stage 3, before anything runs. | Running a test for a week, finding nothing, and concluding there is nothing. With too little data you could not have seen a real effect. Report the MDE with every null result. |
| **Multiple comparisons** | Testing many things raises the chance that something looks significant by chance. | Twenty independent tests at 5% → about a 64% chance of at least one false positive. Fixes: pre-register one primary metric; treat the rest as exploratory; or correct (Bonferroni divides the threshold by the number of tests; Benjamini–Hochberg controls the false discovery rate and is less harsh). | Slicing a result by twelve segments and reporting the one that "worked". |
| **Regression** | A model of how an outcome changes with one or more inputs. | *y = β₀ + β₁x₁ + … + ε*. A coefficient is the change in *y* for a one-unit change in that *x*, holding the others fixed. Use it to adjust for covariates and to estimate effects, not only to predict. Log the outcome when the effect is multiplicative; interpret the coefficient as a percentage. | "Controlling for" a variable that is itself caused by the treatment (a collider or mediator) biases the estimate. |

### 4. Experiments (A/B tests)

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Randomisation unit** | The thing that gets assigned to control or treatment: user, session, device, account. | Choose the unit at which the experience must be consistent and at which the metric is computed. User-level is the default; session-level inflates sample size but a user can see both variants. | Analysing at a finer grain than you randomised. Units must be independent for the test to be valid. |
| **Assignment and bucketing** | How units get split. | Hash the unit id with a per-experiment salt; take the modulo; assign. Log every assignment with timestamp. Traffic allocation can be unequal (e.g. 10% treatment) but is usually 50/50 for power. | Reusing a salt across experiments: the same users land in the same arm every time. |
| **Sample-ratio mismatch (SRM)** | The observed split (e.g. 48/52) differs from the intended one by more than chance. | A chi-squared test on the counts. SRM almost always means a bug — in assignment, logging, or a redirect that drops users — and invalidates the result until fixed. Check it first, every time. | Analysing an experiment with SRM. The result is meaningless. |
| **Primary metric, guardrails, duration** | What decides the test; what must not get worse; how long to run. | One primary metric (pre-registered); two or three guardrails (latency, error rate, revenue, unsubscribes); run for whole weekly cycles and until the pre-computed sample is reached. | Stopping early because the result looks good. Novelty and primacy effects fade over weeks. |
| **Analysing the result** | Computing the effect and its uncertainty. | Difference in means (or proportions) with a confidence interval; the right test for the metric type (see Statistics). Report the absolute and the relative lift, the interval, and the guardrails. Segment results are exploratory unless pre-registered. | Reporting only the point estimate. The interval is the result. |
| **Variance reduction (CUPED)** | Using pre-experiment data to remove noise and reach significance with fewer users. | Adjusted metric: *Y_adj = Y − θ (X − mean(X))*, where *X* is the same metric for that user in the period before the experiment and *θ = cov(X, Y) / var(X)*. Typical variance reduction 20–50% on metrics with stable per-user baselines. | Using a covariate that could be affected by the treatment. It must be from before assignment. |
| **Stratification** | Splitting randomisation or analysis by a known factor (country, platform) so arms are balanced on it. | Post-stratification in analysis gives most of the benefit without touching assignment. | Stratifying on something that is a consequence of treatment. |
| **Peeking and sequential tests** | Looking at results repeatedly and stopping when significant. | Repeated looks at a fixed-horizon test inflate the false-positive rate badly (five looks → roughly 14% instead of 5%). Either fix the horizon and look once, or use a method designed for repeated looks: group-sequential boundaries, or always-valid inference (mSPRT). | A dashboard that shows live *p*-values to stakeholders who will stop the test when it hits 0.05. |
| **Interference** | When one unit's treatment affects another unit's outcome. | Marketplaces (treated buyers compete with control buyers for the same sellers), social features, shared inventory, ads auctions. Fixes: cluster randomisation (by city, by seller), switchback designs (alternate treatment over time), or synthetic control. | Running a simple A/B test on a two-sided market and reporting a lift that cannot exist at full rollout. |

### 5. Causal inference without an experiment

*Each design buys you a causal estimate at the price of an assumption. Know the assumption; it is the first thing an interviewer or a sceptical stakeholder will ask about.*

| Method | What it does | How it works | The assumption you are buying | Use it when |
|---|---|---|---|---|
| **Difference-in-differences (DiD)** | Compares the change over time in a treated group with the change in an untreated group. | Effect = (treated after − treated before) − (control after − control before). In a regression: outcome on *treated*, *after*, and *treated × after*; the interaction is the effect. | **Parallel trends:** without the treatment, both groups would have moved the same way. Check it on the pre-period. | A change was rolled out to some units (regions, stores, user groups) and not others, at a known time. |
| **Regression discontinuity (RDD)** | Compares units just above and just below a threshold that determines treatment. | Fit the outcome on each side of the cutoff; the jump at the cutoff is the effect. Use a narrow window and show the result is stable as the window changes. | Units cannot precisely manipulate which side of the threshold they land on; nothing else changes at the cutoff. | Treatment is assigned by a rule on a continuous score: credit limit above a score, free shipping above a basket value, a discount for accounts older than *n* days. |
| **Synthetic control** | Builds a weighted combination of untreated units that tracks the treated unit before treatment, then compares after. | Choose weights so the synthetic unit matches the treated unit's pre-period outcome; the post-period gap is the effect. Placebo tests on untreated units give a sense of significance. | The pre-period fit is good, and the untreated units were not affected by the treatment. | One treated unit (a country, a city, a product line) and a handful of comparable untreated ones. |
| **Matching and propensity scores** | Compares treated units with untreated units that look the same on observed characteristics. | Estimate the probability of treatment from covariates (the propensity score); match or weight on it; compare outcomes. Check balance on covariates after matching. | **No unobserved confounding:** everything that drives both treatment and outcome is in the covariates. This is the strong one. | Observational data with rich covariates, and no natural experiment to exploit. Treat the result as suggestive. |
| **Instrumental variables (IV)** | Uses something that shifts treatment but affects the outcome only through treatment. | Two-stage least squares: predict treatment from the instrument, then regress the outcome on the predicted treatment. | The instrument affects the outcome *only* through the treatment (exclusion), and is strong enough to shift it. | Rare in product analytics; common in pricing (cost shocks as instruments for price) and in encouragement designs. |
| **Interrupted time series** | Compares the outcome's trend before and after a change, with no control group. | Fit a trend to the pre-period; forecast it forward; the gap to actuals is the effect. | Nothing else changed at the same time, and the pre-trend would have continued. | The change hit everyone at once and there is a long, stable history. Weak alone; stronger combined with DiD. |

### 6. Modelling

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Train / validation / test** | Fitting on one set, tuning on a second, reporting on a third the model never saw. | Split by time when the model will predict the future; a random split leaks tomorrow into today. Cross-validation (k-fold) when data is scarce. | Reporting training-set performance. |
| **Leakage** | A feature that would not be known at prediction time, or that encodes the outcome. | "Days since last order" computed with data after the prediction date; "customer status = churned". The model looks excellent and is useless. | Any feature with suspiciously high importance. |
| **Evaluation metric** | The number that says how good the model is — chosen to match the business cost of errors. | Classification: precision, recall, and the trade-off between them; AUC for ranking; calibration if you will use the probabilities. Regression: MAE when errors cost linearly, RMSE when big errors cost disproportionately. | Accuracy on an imbalanced outcome: 97% accuracy predicting "no churn" when 3% churn. |
| **Regression for understanding** | Using coefficients to explain, not only to predict. | Keep the model interpretable; check residuals; standardise inputs if you want to compare coefficient sizes. | Interpreting coefficients causally without a causal design behind them. |
| **Forecasting** | Predicting a time series forward. | Start with a seasonal naive baseline (same period last year, adjusted for trend). Anything fancier must beat it on held-out recent periods. Decompose into trend, seasonality, residual. | A forecast with no interval, or one that was never compared with a baseline. |

### 7. Charts and dashboards

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Chart choice** | The chart type follows the comparison. | Change over time → line. Categories → sorted bar. Part of whole → stacked bar (rarely pie). Relationship → scatter. Distribution → histogram or box. | A line chart of categories; a pie with eleven slices. |
| **One message per chart** | A chart has a sentence title that states its point. | Remove gridlines, legends that can be direct labels, colours without meaning. Annotate the event. Show uncertainty where it matters. | Charts as data dumps. The craft side of [communication](communication.md). |
| **Dashboards** | For questions that recur. | What belongs: the few metrics the team is judged on, with the agreed definitions, and a load timestamp. What does not: everything else. | A dashboard nobody opens, or one that disagrees with the governed metric. |

---

## In practice

*The habits that make this ability routine.*

- **Predict, then query.** Write the expected row count and headline number before running anything. The habit catches most errors and all agent hallucinations.
- **Learn your warehouse's dialect and your company's models.** Generic SQL gets you to the interview; knowing that `fct_orders` has one row per order line gets you through the first month.
- **Reconcile every headline number** against an independent source before it leaves your hands.
- **Keep a checks script.** Row counts, nulls, duplicates, freshness — one file you run against any new table.
- **Compute power before the test, not after.** The MDE is part of the experiment design, and part of any null result.
- **Make it reproducible before you make it pretty.** A notebook that re-runs top to bottom beats a beautiful one that doesn't.
- **With AI: specify, then verify.** Let agents draft; state the grain and expected shape first; check joins, columns, and reconciliation after. See [working with AI](working-with-ai.md).

> **The one thing to remember:** every number you report should have passed two checks — it matched your prediction or you know why it didn't, and it matched an independent source or you know why it didn't.

---

## What "good" looks like by level

*The same ability, at three depths.*

| | Junior | Mid | Senior |
|---|---|---|---|
| **SQL** | Correct on simple queries; learning window functions | Fluent; right grain by reflex; reads others' SQL critically | Sets query standards; designs the models others query |
| **Platform** | Finds tables with help | Navigates the stack; reads dbt lineage; knows freshness and cost | Shapes what gets modelled and instrumented |
| **Statistics** | Runs the test they were taught | Chooses the right test; computes power; knows the assumptions | Knows when the textbook test is wrong for this data |
| **Experiments** | Analyses a test with a template | Designs and analyses tests end to end, including the engineering spec and SRM check | Owns the experimentation platform's standards; handles interference |
| **Causal methods** | Knows the names | Can run DiD and matching and state their assumptions | Chooses the design from the situation; knows when none is credible |
| **Reproducibility** | Shares a notebook | Shares a notebook that re-runs | Everything is versioned; others build on it |
| **With AI** | Uses it for syntax | Specifies tasks; verifies routinely | Decides what the team delegates |

---

## Interview lens

*Craft is tested directly and early — a live SQL round, a take-home, and statistics questions inside the case.*

| Question | What they want to hear |
|---|---|
| Live SQL: funnel by step, retention cohort, top-N per group, running total, sessionisation | Correct grain, awareness of fan-out, clean CTEs. Say the approach and the expected shape of the result before typing. |
| "The numbers look wrong. What do you check?" | In order: load freshness, tracking changes, date boundaries and time zones, duplicates, filters, join fan-out, late-arriving data. |
| "Walk me through your company's data stack." | Layers, not logos: which layer you query for what, and where the metric definitions live. |
| "Explain a p-value / confidence interval / power to me." | Plain language, correct, and what each does *not* mean. See [communication](communication.md#explaining-statistical-results-to-non-technical-audiences). |
| "Design an A/B test for X." | Hypothesis, randomisation unit, primary and guardrail metrics, sample size from a stated baseline and MDE, duration in whole weeks, SRM check, analysis plan, decision rule for each outcome. |
| "The test shows a 2% lift with p = 0.04. Ship it?" | Was it the pre-registered primary metric? Power and MDE? Interval? Guardrails? How many segments were examined? Was there peeking? Then a decision. |
| "You can't randomise. How would you estimate the effect?" | Pick a design from the causal table, state its assumption, say how you would check it. |
| "Users who use feature X retain better. Should we push everyone to X?" | Selection; the ideal experiment; what observational design could approximate it. |
| Take-home | Reproducibility, verification, and whether the conclusion follows. AI use is usually allowed — show the checks. |

**Story bank prompts (STAR)**

1. A data-quality problem you found, and how you found it
2. An experiment you implemented end to end, including the engineering coordination and what the SRM check showed
3. A time the textbook method was wrong for the data and what you did instead
4. A causal estimate you made without an experiment, and how you defended the assumption

---

## Resources

*A short list. Read one per group.*

- **SQL:** [Mode SQL Tutorial](https://mode.com/sql-tutorial/) and [Select Star SQL](https://selectstarsql.com/) — basics to interview level
- **Platform:** [dbt — What is analytics engineering?](https://www.getdbt.com/what-is-analytics-engineering)
- **Statistics and experiments:** Ron Kohavi, Diane Tang, Ya Xu, *Trustworthy Online Controlled Experiments* — the reference; [Evan Miller, How Not to Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html) — peeking in two pages
- **Causal methods:** Scott Cunningham, [*Causal Inference: The Mixtape*](https://mixtape.scunning.com/) — free online; [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference) for depth
- **Programming:** Hadley Wickham et al., [*R for Data Science*](https://r4ds.hadley.nz/) or Wes McKinney, *Python for Data Analysis*
- **Charts:** Cole Nussbaumer Knaflic, *Storytelling with Data*
