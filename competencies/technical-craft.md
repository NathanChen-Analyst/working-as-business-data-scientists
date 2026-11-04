# Technical craft

> **Definition.** The ability to execute analytical work cleanly, correctly, and reproducibly: SQL and the data platform it runs on, a programming language for what SQL cannot do, the statistics and experimentation mechanics behind the methods, and the tooling that turns a result into something others can see and reuse.

**Why it matters — and why it matters less than people think.** Craft is the entry ticket. Without it nothing else in this repo can happen, and it is the single most-tested thing in analyst interviews. But it is primary in only two of the eight stages, and it is the ability AI agents have changed most: the fluent production of code is now cheap, while specifying and verifying it is not. Craft today means knowing what correct looks like well enough to check it, more than typing it fast.

---

## Where it shows up in the workflow

| Stage | What technical craft looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Knowing what data exists and roughly what it can answer | ○ |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Knowing whether the tracking can distinguish the branches of the issue tree | ○ |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Computing variance and minimum detectable effect; knowing how a metric is implemented in the metrics layer | ● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | SQL at the right grain; platform navigation; data-quality checks; reconciliation | ●● |
| [5 Analyse](../workflow.md#stage-5--analyse) | Statistics, experimentation mechanics, causal-inference methods, modelling when warranted | ●● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Sensitivity checks run, not just imagined; effect sizes with intervals | ● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Charts that are correct and legible; a dashboard when one is warranted | ○ |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Monitoring queries, alerting, post-launch measurement | ○ |

---

## The toolkit

### SQL and the data platform

**SQL** — *The core skill.* Joins and their fan-out behaviour, aggregation at a chosen grain, window functions (running totals, rank, lag/lead), CTEs for readable multi-step logic, date handling, `CASE` logic, `QUALIFY` where the dialect has it. The interview classics: funnel conversion by step, retention cohorts, top-N per group, sessionisation. Stage 4 and 5.

**The platform** — *Where the data is and how it got there.* Sources → event tracking → warehouse → transformation (dbt) → metrics layer → BI → catalog. Knowing which layer to query, how to read a dbt model and its lineage, when the data was last loaded, and what a query costs. The full layer table is in [Stage 4](../workflow.md#stage-4--get-and-trust-the-data).

**Data-quality checks** — *Is this table what it claims to be?* Row counts over time, null rates, duplicate keys, schema changes, reconciliation against an independent source. A short, reusable script of these is one of the highest-return things an analyst can own. Stage 4.

**Event-tracking literacy** — *What does an event actually mean?* Client vs. server events, identity resolution across devices, sessionisation rules, what happens when a release renames an event. Stage 4. *Running example:* the tracking break that explained half the drop.

### Programming

**Python or R** — *For what SQL cannot do cleanly.* pandas or dplyr for reshaping; statistical libraries (statsmodels, scipy, R's base and tidymodels) for tests and models; matplotlib/seaborn/plotnine/ggplot2 for charts. One language fluently beats two badly. Stage 5 and 6.

**Notebooks and reproducibility** — *Can someone else run this and get the same answer?* Jupyter, Hex, Deepnote, Quarto. Parameterise dates, pin the data snapshot, clear and re-run before sharing. Stage 5 through 7.

**Version control** — *What changed, when, and why?* Git for anything that will be reused or reviewed. Stage 4 onward.

### Statistics

**Descriptive foundations** — distributions, skew, percentiles, why the mean misleads on order value. Stage 5.

**Inference** — confidence intervals, hypothesis tests, what a p-value is and is not, power and minimum detectable effect, multiple comparisons. Stage 3 (power, before the test) and Stage 5. The *reasoning* side of these lives in [analytical reasoning](analytical-reasoning.md); this is the mechanics.

**Regression** — as a tool for understanding relationships and adjusting for covariates, not only for prediction. Interpreting coefficients, interactions, and what controlling for something does and does not buy you. Stage 5.

### Experimentation mechanics

**A/B test implementation** — randomisation unit, bucketing and hashing, sample-ratio mismatch checks, assignment logging. Stage 5; coordinated with engineering.

**Analysis of experiments** — the right test for the metric type (means, proportions, ratio metrics via the delta method), variance reduction (CUPED), stratification, handling peeking (sequential methods or a fixed horizon). Stage 5.

**Quasi-experimental methods** — difference-in-differences, regression discontinuity, synthetic control, matching, instrumental variables. Knowing the implementation *and* the assumption each one rests on. Stage 5; [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference) for depth.

### Modelling (where the role calls for it)

**Supervised learning basics** — regression and classification, train/validation/test, cross-validation, the evaluation metric that matches the business cost of errors, feature leakage. Stage 5. Most analyst roles need the ability to read and evaluate a model more than to build one.

**Forecasting** — seasonality, trend, simple baselines before anything elaborate. Stage 5 and 8.

### Visualisation and delivery

**Chart grammar** — the right chart for the comparison, decluttering, annotation, one message per chart. The craft side of [communication](communication.md). Stage 7.

**Dashboards** — when a question recurs, a dashboard beats a repeated analysis. Looker, Tableau, Power BI, Metabase, or whatever the organisation uses; the skill is knowing what belongs on one and what does not. Stage 7 and 8.

---

## How it looks in practice

- **Learn your warehouse's dialect and your company's models.** Generic SQL gets you to the interview; knowing that orders live in `fct_orders` with a grain of one row per order line gets you through the first month.
- **Predict, then query.** Write the expected row count and headline number before running anything. The habit catches most errors and all agent hallucinations.
- **Reconcile every headline number** against an independent source before it leaves your hands.
- **Keep a checks script.** Row counts, nulls, duplicates, freshness — one file you run against any new table.
- **Make it reproducible before you make it pretty.** A notebook that re-runs top to bottom is worth more than a beautiful one that doesn't.
- **With AI: specify and verify.** Let agents draft; state the grain and expected shape first; check joins, columns, and reconciliation after. See [working with AI](working-with-ai.md).

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **SQL** | Correct on simple queries; learning window functions | Fluent; right grain by reflex; reads others' SQL critically | Sets query standards; designs the models others query |
| **Platform** | Finds tables with help | Navigates the stack; reads dbt lineage; knows freshness and cost | Shapes what gets modelled and instrumented |
| **Statistics** | Runs the test they were taught | Chooses the right test; computes power; knows the assumptions | Knows when the textbook test is wrong for this data |
| **Experiments** | Analyses a test with a template | Designs and analyses tests end to end, including the engineering spec | Owns the experimentation platform's standards |
| **Reproducibility** | Shares a notebook | Shares a notebook that re-runs | Everything is versioned; others build on it |
| **With AI** | Uses it for syntax | Specifies tasks; verifies routinely | Decides what the team delegates |

---

## Interview lens

Craft is tested directly and early — usually a live SQL round, a take-home, and statistics questions inside the case.

**Live SQL.** Funnel conversion by step; retention cohort by signup month; top-N per group; running totals; sessionising events with a timeout. *What they want:* correct grain, awareness of fan-out, clean CTEs, and that you talk through the approach before typing. Narrate the predicted shape of the result.

**"The numbers look wrong. What do you check?"** Freshness, tracking changes, date boundaries and time zones, duplicates, filters, join fan-out, late-arriving data. Ordered, not scattered.

**"Walk me through your company's data stack."** Layers, not logos; which layer you query for what; where the metric definitions live.

**"Explain a p-value / confidence interval / power to me."** Correctly, in plain language, with what it does *not* mean.

**"Design an A/B test for X."** Randomisation unit, primary and guardrail metrics, sample size and duration, analysis plan, and what you do with each outcome.

**Take-homes.** Reviewers look at reproducibility, verification, and whether the conclusion follows, far more than at code style. AI use is usually allowed; show the checks.

### Story bank prompts (STAR)
1. A data-quality problem you found and how you found it
2. A query or analysis you made reproducible, and what that enabled later
3. An experiment you implemented end to end, including the engineering coordination
4. A time the textbook method was wrong for the data and what you did instead

---

## Resources

- [Mode SQL Tutorial](https://mode.com/sql-tutorial/) and [Select Star SQL](https://selectstarsql.com/) — SQL from basics to interview level
- [dbt — What is analytics engineering?](https://www.getdbt.com/what-is-analytics-engineering) — the modern platform from the transformation side
- Ron Kohavi, Diane Tang, Ya Xu, *Trustworthy Online Controlled Experiments* — experimentation mechanics, the reference
- Scott Cunningham, [*Causal Inference: The Mixtape*](https://mixtape.scunning.com/) — quasi-experimental methods, free online
- Hadley Wickham et al., [*R for Data Science*](https://r4ds.hadley.nz/) or Wes McKinney, *Python for Data Analysis* — one language, properly
- Cole Nussbaumer Knaflic, *Storytelling with Data* — chart craft

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
