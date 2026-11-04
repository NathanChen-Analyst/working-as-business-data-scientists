# Technical craft

*Executing analytical work correctly and reproducibly: the data platform and the SQL that runs on it, a programming language for what SQL cannot do, the statistics, experiments, causal methods, and models behind the analysis — including enough about machine learning, deep learning, and LLMs to use and evaluate them — and the tooling that turns a result into something others can see and reuse.*

**On this page:** [Why it matters](#why-it-matters) · [Where it shows up](#where-it-shows-up-in-the-workflow) · [The toolkit](#the-toolkit) — [Platform](#1-the-data-platform) · [SQL](#2-sql) · [Programming](#3-programming-and-reproducibility) · [Statistics](#4-statistics) · [Experiments](#5-experiments-ab-tests) · [Causal methods](#6-causal-inference-without-an-experiment) · [ML & evaluation](#7-statistical-learning-and-machine-learning) · [Deep learning & LLMs](#8-deep-learning-transformers-llms-and-ai-agents) · [Charts](#9-charts-and-dashboards) · [In practice](#in-practice) · [By level](#what-good-looks-like-by-level) · [Interview lens](#interview-lens) · [Resources](#resources)

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

*Nine groups. Each concept is defined in plain words, with the detail that matters in practice and the trap that catches people. The methods interviews test most — power, A/B analysis, the causal designs, model evaluation — get the most detail.*

### 1. The data platform

*Where the data lives, how it got there, and what each layer means for the analyst. Names differ by company; the layers are nearly universal.*

**The layers**

| Layer | What it is | Typical tools | What the analyst needs to know |
|---|---|---|---|
| **Sources** | The systems where data is created: the product database, the payment provider, the CRM, ad platforms, the support tool. | Postgres/MySQL replicas, Stripe, Salesforce, HubSpot, Zendesk | Which system is the *source of truth* for each thing. Revenue lives in the payments system, not in product events. |
| **Event tracking** | Instrumentation that records what users do in the product. | Segment, Amplitude, Mixpanel, Google Analytics, Snowplow, in-house | Client-side events can be blocked, duplicated, or renamed in a release; server-side events are more reliable but sparser. One person can have several ids across devices. |
| **Ingestion** | Copying data from sources into the warehouse, usually on a schedule. | Fivetran, Airbyte, Stitch, custom pipelines; streaming via Kafka for near-real-time | The load schedule sets the *freshness*. A query at 09:00 may see data that ended at midnight. Check the load timestamp before reporting a "drop". |
| **Warehouse / lakehouse** | The central store for analysis. Columnar, distributed, built for large scans. | Snowflake, BigQuery, Redshift, Databricks | The raw layer mirrors sources; the modelled layer is what you should query. Queries cost money on most platforms. |
| **Transformation** | The code that turns raw tables into clean, tested, documented models. | dbt (dominant), Dataform, SQLMesh; orchestrated by Airflow, Dagster, Prefect | Read the model definition and its lineage before trusting a column. Tests tell you what has been checked. Models are version-controlled SQL — you can read the git history. |
| **Semantic / metrics layer** | The agreed definitions of business metrics, encoded once so every tool computes them the same way. | dbt Semantic Layer / MetricFlow, Looker's LookML, Cube | If a metric exists here, use it. If your number differs from the governed one, explain why before reporting either. |
| **BI / dashboards** | Where stakeholders look at data without you. | Looker, Tableau, Power BI, Metabase, Mode, Hex | What stakeholders already see shapes what they ask. Check the dashboard before answering the question it generated. |
| **Catalog / docs** | Where tables, owners, and definitions are described. | dbt docs, DataHub, Atlan, Alation, a wiki | The first place to look, and the first thing to improve when it is wrong. |

**How a modern warehouse works — the concepts behind the tools**

| Concept | What it is | Why it matters to you |
|---|---|---|
| **Columnar storage** | Data stored by column, not by row. A query reads only the columns it names. | `SELECT *` scans everything and costs the most. Name your columns. Filters on a column the table is partitioned or clustered by are much cheaper. |
| **MPP (massively parallel processing)** | The query is split across many machines and the results combined. | Big aggregates are fast; row-by-row logic (correlated sub-queries, cursors) is slow. Think in sets. |
| **Separation of storage and compute** | Data sits in cheap object storage; compute is rented when a query runs. | You pay for scans and for warehouse time, not for data at rest. A careless query can cost real money; most platforms show the estimated bytes before you run it. |
| **Data lake vs warehouse vs lakehouse** | Lake: raw files in object storage, cheap, schema on read. Warehouse: structured tables, schema on write, fast SQL. Lakehouse: lake storage with warehouse features (tables, transactions, SQL) on top. | Databricks and the open table formats (Delta, Iceberg) are lakehouses; Snowflake and BigQuery began as warehouses and now do both. For an analyst the difference is mostly invisible — you write SQL either way. |
| **ELT, not ETL** | Load raw data first, then transform inside the warehouse with SQL. | This is why dbt exists and why the raw layer is there. Transformations are inspectable SQL, not hidden pipeline code. |
| **Raw → staging → marts (the medallion pattern)** | Raw: as loaded. Staging ("silver"): cleaned, renamed, typed, one model per source table. Marts ("gold"): business-level tables — `fct_orders`, `dim_customers` — built for analysis. | Query marts. Go to staging when a mart lacks a column. Go to raw only to debug, and tell data engineering what you found. |
| **Facts and dimensions** | Fact tables hold events or transactions at a stated grain (`fct_orders`: one row per order). Dimension tables hold descriptive attributes (`dim_customers`: one row per customer). | Join facts to dimensions on the key; never join two facts without checking the grain. Slowly changing dimensions record how an attribute changed over time — know whether you have the current value or the value at the time. |
| **Partitioning and clustering** | Physical layout of a table by a column (usually date) so queries that filter on it read less. | Always filter on the partition column when you can. A date filter on an unpartitioned column scans the whole table. |
| **Lineage** | The graph of which models feed which. | Answers "where did this column come from?" and "what breaks if this changes?" dbt draws it for you. |
| **Data tests** | Assertions on models: not null, unique, accepted values, referential integrity, freshness. | A model with tests has been checked for *those things*. It has not been checked for the thing you are about to assume. |

**The four big platforms, briefly**

| Platform | Character | What an analyst notices |
|---|---|---|
| **Snowflake** | Cloud-neutral warehouse; virtual warehouses of different sizes that you start and stop. | You pay per second of warehouse time. `QUALIFY` exists. Semi-structured JSON is easy with `VARIANT`. |
| **BigQuery** (Google) | Serverless; you pay per byte scanned (or buy slots). | The estimated bytes appear before you run; use them. Partition filters matter most here. Arrays and structs are native. |
| **Redshift** (AWS) | Cluster-based warehouse, closest to classic Postgres. | Dist keys and sort keys affect performance; some newer SQL features arrive later. |
| **Databricks** | Lakehouse on Spark; notebooks and SQL in one place; strong for ML and streaming. | Delta tables; SQL warehouses for BI; notebooks for Python at scale. The line between analyst and data scientist is thinnest here. |

> **The one thing to remember:** query the modelled layer, filter on the partition column, check the load timestamp, and read the model before you trust the column.

### 2. SQL

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Grain** | What one row of a table represents: one order, one order line, one user-day. | Every aggregate has a grain. Decide it before writing the query, and state it in the query's comment. `COUNT(DISTINCT key)` against the raw table tells you if a table's grain is what you think. | The commonest error in all of analytics: aggregating at the wrong level — sessions when you meant users. |
| **Joins and fan-out** | Combining tables on a key. Fan-out is when a one-to-many join multiplies rows. | Check row counts before and after every join. Joining orders to order lines and then summing order value counts each order once per line. | Fan-out is silent. The query runs, the number is wrong, nothing warns you. |
| **Window functions** | Calculations across a set of rows related to the current row, without collapsing them. `ROW_NUMBER`, `RANK`, `LAG`, `LEAD`, `SUM(...) OVER (...)`. | Running totals, first/last event per user, time since previous event, top-N per group. `PARTITION BY` sets the group; `ORDER BY` sets the sequence. | Forgetting the frame clause: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` vs the default `RANGE`, which treats ties differently. |
| **CTEs** | Named sub-queries (`WITH step AS (...)`) that break a query into readable steps. | One CTE per logical step: filter, then join, then aggregate. Each one can be run alone to check its row count. | Chains of eight CTEs that nobody can follow. If a CTE is reused across queries, it should be a model. |
| **Funnel query** | Conversion between ordered steps. | One row per user with a flag per step reached (`MAX(CASE WHEN event = 'x' THEN 1 END)`), then aggregate. Conversion at step *n* = users reaching *n* ÷ users reaching *n-1*. | Counting events instead of users; ignoring step order (a user can hit step 3 without step 2 if tracking misfired). |
| **Retention cohort** | Share of users from a signup period who return in each later period. | Cohort = signup month; period = months since signup; retained = any activity in that period. Pivot to a cohort × period grid. | Mixing calendar months with months-since-signup; counting the signup month as "retained". |
| **Sessionisation** | Grouping events into sessions by inactivity gap. | `LAG(timestamp)` per user → flag a new session when the gap exceeds the timeout (often 30 minutes) → running `SUM` of flags gives the session id. | Timeout choice changes every session metric. State it. |
| **Data-quality checks** | A short script run against any new table. | Row counts by day, null rate per column, duplicate keys, distinct values of categoricals, min/max of dates and amounts, and a reconciliation of the headline number against an independent source (finance, the payments provider, last month's report). | Checking once and never again. Tables change under you. |
| **Event tracking** | Instrumentation that records what users do. | Client-side events can be blocked, duplicated, or renamed in a release; server-side events are more reliable but sparser. Identity: one person, several devices, several ids. | A release renames one event and half your funnel "disappears" — the running example's tracking break. |

### 3. Programming and reproducibility

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Python or R** | For what SQL cannot do cleanly: reshaping, statistics, modelling, charts. | pandas or dplyr for data; statsmodels/scipy or R's base stats for tests; matplotlib/seaborn or ggplot2 for charts. One language fluently beats two badly. | Doing in Python what the warehouse would do faster in SQL. Pull aggregates, not raw rows. |
| **Notebooks** | Jupyter, Hex, Deepnote, Quarto: code, output, and narrative together. | Parameterise dates and ids at the top; pin the data snapshot; restart and run all before sharing. | A notebook that only works because of cells run out of order. |
| **Version control** | Git, for anything reused or reviewed. | Commit per logical change with a message that says why. Code review for anything that reaches a stakeholder. | Analysis code that lives only on one laptop. |
| **Reproducibility** | Someone else can run it and get the same answer. | Fixed random seeds; recorded package versions; data pulled by query, not by hand-exported CSV. | "It worked on my machine" is not an analysis. |

### 4. Statistics

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

### 5. Experiments (A/B tests)

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

### 6. Causal inference without an experiment

*Each design buys you a causal estimate at the price of an assumption. Know the assumption; it is the first thing an interviewer or a sceptical stakeholder will ask about.*

| Method | What it does | How it works | The assumption you are buying | Use it when |
|---|---|---|---|---|
| **Difference-in-differences (DiD)** | Compares the change over time in a treated group with the change in an untreated group. | Effect = (treated after − treated before) − (control after − control before). In a regression: outcome on *treated*, *after*, and *treated × after*; the interaction is the effect. | **Parallel trends:** without the treatment, both groups would have moved the same way. Check it on the pre-period. | A change was rolled out to some units (regions, stores, user groups) and not others, at a known time. |
| **Regression discontinuity (RDD)** | Compares units just above and just below a threshold that determines treatment. | Fit the outcome on each side of the cutoff; the jump at the cutoff is the effect. Use a narrow window and show the result is stable as the window changes. | Units cannot precisely manipulate which side of the threshold they land on; nothing else changes at the cutoff. | Treatment is assigned by a rule on a continuous score: credit limit above a score, free shipping above a basket value, a discount for accounts older than *n* days. |
| **Synthetic control** | Builds a weighted combination of untreated units that tracks the treated unit before treatment, then compares after. | Choose weights so the synthetic unit matches the treated unit's pre-period outcome; the post-period gap is the effect. Placebo tests on untreated units give a sense of significance. | The pre-period fit is good, and the untreated units were not affected by the treatment. | One treated unit (a country, a city, a product line) and a handful of comparable untreated ones. |
| **Matching and propensity scores** | Compares treated units with untreated units that look the same on observed characteristics. | Estimate the probability of treatment from covariates (the propensity score); match or weight on it; compare outcomes. Check balance on covariates after matching. | **No unobserved confounding:** everything that drives both treatment and outcome is in the covariates. This is the strong one. | Observational data with rich covariates, and no natural experiment to exploit. Treat the result as suggestive. |
| **Instrumental variables (IV)** | Uses something that shifts treatment but affects the outcome only through treatment. | Two-stage least squares: predict treatment from the instrument, then regress the outcome on the predicted treatment. | The instrument affects the outcome *only* through the treatment (exclusion), and is strong enough to shift it. | Rare in product analytics; common in pricing (cost shocks as instruments for price) and in encouragement designs. |
| **Interrupted time series** | Compares the outcome's trend before and after a change, with no control group. | Fit a trend to the pre-period; forecast it forward; the gap to actuals is the effect. | Nothing else changed at the same time, and the pre-trend would have continued. | The change hit everyone at once and there is a long, stable history. Weak alone; stronger combined with DiD. |

### 7. Statistical learning and machine learning

*What a model is, how it is fitted, and — the part that matters most for an analyst — how to tell whether it is any good. Most analyst roles need the ability to read, evaluate, and challenge a model more than to build one.*

**Foundations**

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **A model** | A function from inputs (features) to an output (prediction), with parameters learned from data. | Supervised: the data has the answer (labels) and the model learns to reproduce it — regression for numbers, classification for categories. Unsupervised: no labels; the model finds structure — clustering, dimensionality reduction. | Calling something "a model" when it is a lookup table or a rule. Both are fine; name them honestly. |
| **Estimation** | How the parameters are found. | Least squares: choose parameters that minimise the squared errors (closed form for linear regression). Maximum likelihood: choose parameters that make the observed data most probable (logistic regression, most statistical models). Gradient descent: start anywhere, repeatedly step downhill on the loss; the workhorse for anything too big or non-linear for closed forms, including every neural network. | An estimate without a standard error or an interval is a guess with decimals. |
| **Learning = estimation + selection** | "Learning" is the machine-learning word for estimation: choosing parameters from data. Machine learning adds a second step under the same word — choosing the model's *shape* from data as well. | Estimation sets the parameters (the coefficients, the split points, the weights) by minimising a loss. Selection sets the hyperparameters (tree depth, regularisation strength, number of trees, learning rate) by trying values and keeping the one that does best on validation data. Statistics tends to fix the shape by assumption and estimate the rest; machine learning lets data decide both. | Treating selection as free. Every hyperparameter you tune on validation data is a chance to overfit to it — which is why the test set exists. |
| **Statistical learning vs machine learning** | The same family of methods — regression, trees, nearest neighbours, boosting — seen from two sides. Statistical learning asks *why*: what the relationship is, how uncertain the estimate, whether the assumptions hold. Machine learning asks *how well*: how accurately the model predicts cases it has not seen. | Same model, different questions: a logistic regression used to *explain* which factors drive churn is statistical learning; the same regression used to *rank* customers by churn risk next month is machine learning. The explaining use needs standard errors and assumptions; the predicting use needs held-out evaluation. | Using a model built for prediction to make causal claims, or judging an explanatory model only by its accuracy. Decide which question you are asking first; it changes what "good" means. |
| **Loss function** | The number the fitting procedure minimises. | Squared error for regression; log-loss (cross-entropy) for classification. The loss defines what "good" means to the algorithm — it is not automatically what "good" means to the business. | Optimising log-loss when the business cost is asymmetric (a missed fraud case costs 100× a false alarm). |
| **Bias and variance** | Bias: error from a model too simple to capture the pattern. Variance: error from a model that fits the noise in this particular sample. | Total error ≈ bias² + variance + irreducible noise. Simple models have high bias, low variance; flexible models the reverse. The right complexity minimises the sum. | Chasing training error to zero. That is pure variance. |
| **Overfitting and regularisation** | Overfitting: the model learned this sample, not the pattern. Regularisation: penalising complexity so it cannot. | Ridge (L2) shrinks coefficients toward zero; lasso (L1) shrinks some to exactly zero, selecting features. Tree ensembles regularise through depth limits, minimum leaf sizes, and learning rate. Choose the strength on validation data. | A model that is perfect on training data and useless on last week's. |
| **Features** | The inputs, and the work of constructing them. | Most of the gain in applied ML is in features, not algorithms: ratios, lags, counts over windows, encodings of categories. Build them only from information available at prediction time. | Leakage — see Evaluation. |

**The common models**

| Model | What it does | When it fits | Watch out for |
|---|---|---|---|
| **Linear regression** | Fits a straight-line (or plane) relationship; coefficients are interpretable. | Understanding relationships; a baseline for any numeric prediction. | Non-linear patterns; outliers pulling the line. |
| **Logistic regression** | Linear model for a probability; outputs between 0 and 1. | Classification with interpretable effects: churn, conversion, default. The default baseline. | Coefficients are log-odds; translate before reporting. |
| **Decision tree** | Splits the data by one feature at a time into boxes with a prediction each. | Explaining a rule to a stakeholder; capturing interactions. | A single tree is unstable — small data changes, different tree. |
| **Random forest** | Many trees on random subsets of rows and features, averaged. | A strong default for tabular data; robust; little tuning. | Slower to score; less interpretable than one tree (use feature importance and partial-dependence plots). |
| **Gradient boosting** (XGBoost, LightGBM, CatBoost) | Trees built one after another, each correcting the last's errors. | The usual winner on tabular business data: churn, propensity, LTV, demand. | Easy to overfit without early stopping; tune learning rate, depth, number of trees on validation data. |
| **k-nearest neighbours** | Predicts from the most similar past cases. | Small data; a sanity check. | Slow at scale; sensitive to feature scaling. |
| **k-means clustering** | Groups points into *k* clusters around centroids. | Customer segmentation; choosing *k* by the elbow or silhouette, and by whether the segments mean anything commercially. | Clusters exist whether or not the structure is real. Scale features first. |
| **PCA** | Rotates the data to a few axes that capture most of the variation. | Compressing many correlated features; visualising high-dimensional data. | Components are hard to name; check how much variance the first few explain. |
| **Time-series models** | Forecasting from a series' own history. | Seasonal naive → exponential smoothing (ETS) → ARIMA → Prophet or gradient boosting with lag features. | Anything must beat the seasonal naive baseline on held-out recent periods. A forecast without an interval is not a forecast. |

**Error and evaluation — the part to know cold**

| Concept | What it is | The detail that matters | Watch out for |
|---|---|---|---|
| **Train / validation / test** | Fit on one set, tune on a second, report on a third the model never saw. | Split by *time* when the model will predict the future; a random split leaks tomorrow into today. Cross-validation (k-fold) when data is scarce: rotate which fold is held out, average the scores. | Reporting training performance. Tuning on the test set (it then becomes a validation set and you have no test). |
| **Leakage** | A feature that encodes the outcome or would not be known at prediction time. | "Days since last order" computed after the prediction date; "account status = closed" as a churn feature. The model looks superb and is useless. | Any feature with suspiciously high importance. Any score that seems too good. |
| **Confusion matrix** | For classification: true positives, false positives, true negatives, false negatives. | Everything below derives from it. Draw it for the chosen threshold, and say what each cell costs the business. | Reading it without the threshold that produced it. |
| **Precision and recall** | Precision: of those predicted positive, how many were. Recall: of the actual positives, how many were found. | They trade off through the threshold. F1 is their harmonic mean, for when you need one number. Choose the threshold from the business cost of each error, not from 0.5. | Reporting one without the other. 99% precision with 2% recall finds almost nobody. |
| **Accuracy** | Share of predictions that were right. | Fine when classes are balanced and errors cost the same. | 97% accuracy predicting "no churn" when 3% churn — the model that predicts nothing scores 97%. |
| **ROC and AUC** | ROC: true-positive rate against false-positive rate across all thresholds. AUC: the area under it — the chance the model ranks a random positive above a random negative. | Threshold-free; good for comparing models. AUC 0.5 is coin-flipping; 0.8 is useful; 0.95+ deserves a leakage check. | AUC says nothing about calibration or about performance at the one threshold you will use. Precision–recall curves are better for rare outcomes. |
| **Calibration** | Whether a predicted 30% actually happens 30% of the time. | Plot predicted against observed in bins. Matters whenever the probability itself is used — expected value, ranking by risk. | Tree ensembles are often poorly calibrated out of the box; Platt scaling or isotonic regression fixes it. |
| **Regression errors** | MAE: average absolute error, in the outcome's units. RMSE: root mean squared error — penalises large misses more. MAPE: percentage error, undefined at zero. | MAE when errors cost linearly; RMSE when big misses cost disproportionately. Always report against a baseline (predict the mean; predict last period). | A good-looking error with no baseline. R² without an interval. |
| **Baselines** | The simplest possible model, to beat. | Predict the mean; predict the majority class; predict last period's value; a logistic regression on three obvious features. | A complex model that nobody compared with the simple one. |
| **Explaining a model** | Saying which inputs drive the prediction. | Coefficients (linear models); feature importance and partial-dependence plots (tree ensembles); SHAP values for per-prediction explanations. | Reading importance as causation. It is not. |
| **Model monitoring** | Checking that a model still works after deployment. | Drift in input distributions; drift in the relationship; a performance metric tracked against the baseline on fresh labelled data. | A model that was good in March and nobody checked since. |

> **The one thing to remember:** a model's quality is a number on data it never saw, compared with a baseline, at the threshold you will actually use, with the business cost of each kind of error stated. Anything less is a demo.

### 8. Deep learning, transformers, LLMs, and AI agents

*Enough to understand what these systems are, why they behave as they do, and how to evaluate them — not to build them. The practical side of working with agents is in [working with AI](working-with-ai.md).*

**Neural networks and deep learning**

| Concept | What it is | The detail that matters |
|---|---|---|
| **Neural network** | Layers of simple units; each unit computes a weighted sum of its inputs and passes it through a non-linear function (an *activation*, such as ReLU). Stacking layers lets the network represent very complex functions. | A linear model is a network with no hidden layer. Depth (many layers) is what "deep" means. Parameters are the weights; a large model has billions. |
| **Training** | Gradient descent on a loss, with the gradient computed layer by layer backwards from the output — *backpropagation*. | Needs lots of data and compute. Learning rate, batch size, and number of passes (epochs) are the main dials. Overfitting is controlled by dropout, early stopping, and more data. |
| **Why deep learning won** | It learns features from raw data instead of needing them hand-built. | Images, audio, text: hand-built features were the bottleneck; networks learn them. For tabular business data, gradient boosting still usually wins — deep learning is not the default there. |
| **Specialised architectures** | CNNs (convolutional) for images: learn local patterns and build them up. RNNs/LSTMs for sequences: process one step at a time with memory. | Both are now largely superseded by transformers for most tasks, but the ideas — locality, sequence — remain. |
| **Embeddings** | Representing a word, a product, a user as a vector of numbers such that similar things are close together. | Learned, not designed. The basis of recommendation systems, semantic search, and every language model. Cosine similarity between embeddings is "how alike are these". |

**Transformers and large language models**

| Concept | What it is | The detail that matters |
|---|---|---|
| **Transformer** | The architecture behind modern language models. Its key mechanism is *attention*: for each token, the model computes how much to weigh every other token in the input when building its representation. | Attention replaced sequential processing: the whole input is seen at once, which allows parallel training and long-range context. Stacked attention and feed-forward layers, dozens to hundreds deep. |
| **Tokens** | The units a model reads and writes: pieces of words, roughly ¾ of a word each in English. | Context window = how many tokens the model can see at once. Cost and latency scale with tokens. Numbers and code tokenise awkwardly, which is one reason arithmetic is unreliable. |
| **Large language model (LLM)** | A transformer trained to predict the next token on a very large corpus of text, then tuned to follow instructions and to be helpful. | *Pre-training* gives general knowledge and language. *Fine-tuning* and *reinforcement learning from feedback* shape behaviour. The model has no database; what it "knows" is in its weights, frozen at training time. |
| **Why LLMs make things up** | The model produces the most plausible continuation, not the true one. If the truth is not in its weights or its context, it will still produce something plausible. | *Hallucination* is not a bug to be patched; it is what next-token prediction does when unconstrained. Fixes are external: give it the facts (retrieval), make it check (tools), verify the output (you). |
| **Prompting** | What you put in the context window: instructions, examples, data. | Specific beats vague; examples beat descriptions; asking for the reasoning before the answer helps on hard problems. The context is the only thing the model knows about your situation. |
| **Retrieval-augmented generation (RAG)** | Fetch relevant documents (by embedding similarity), put them in the context, then ask. | How an LLM answers questions about your company's data or docs without being retrained. Quality depends on the retrieval more than on the model. |
| **Fine-tuning** | Further training on your own examples to change behaviour or style. | Rarely needed for analytics work; prompting and retrieval cover most cases. Expensive to maintain as base models improve. |

**AI agents**

| Concept | What it is | The detail that matters |
|---|---|---|
| **Agent** | An LLM in a loop: it reads a goal, decides an action, calls a *tool* (run SQL, read a file, search the web, call an API), reads the result, and repeats until done. | The tools are what make it useful for analysis — the model writes and runs the query rather than describing one. The loop is what makes it risky — errors compound across steps, and the agent will keep going confidently. |
| **Tool use / function calling** | The model outputs a structured request to call a function; the harness runs it and returns the result. | Every tool is a capability and a surface for mistakes. An agent with warehouse access can run an expensive or destructive query. Read-only access and cost limits are not optional. |
| **Where agents are strong** | Fluent generation of code and text; first-pass exploration; applying known patterns at speed; tireless iteration. | Stages 4–6 of the workflow. See the per-stage table in [working with AI](working-with-ai.md). |
| **Where agents are weak** | Knowing what they don't know; the people side; judgment about what matters; anything requiring facts not in their context. | Stages 1–3 and 7–8. Fluency is not accuracy: an agent's wrong answer reads exactly like its right one. |
| **Evaluating an agent or LLM output** | The same discipline as evaluating any model: a labelled set of realistic tasks, a success metric, scoring, failure analysis. | For LLMs: exact-match or rubric scoring; an *LLM-as-judge* for scale, calibrated against human grading on a sample; and always a look at the failures by type. For code: does it run, is the grain right, does the number reconcile. The procedure is in [working with AI](working-with-ai.md#evaluating-ai-tools-and-ai-produced-work-more-formally). |
| **Analytics with LLMs in the loop** | Text-to-SQL, automated first-pass analysis, summarising documents and tickets, classifying free text at scale, drafting memos. | The classification and summarisation uses are mature and valuable — thousands of support tickets categorised in an hour. Text-to-SQL is useful with a good semantic layer and dangerous without one. All of it needs verification proportional to the stakes. |

> **The one thing to remember:** an LLM is a model of plausible text, not a model of the world. Everything useful about it comes from what you put in its context and how you check what comes out.

### 9. Charts and dashboards

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
| **Models** | Fits a model from a template | Evaluates any model properly: held-out data, baseline, threshold, cost of errors; builds boosted trees for tabular problems | Decides when a model is the right tool, challenges others' evaluations, sets monitoring standards |
| **LLMs and agents** | Uses them | Knows why they hallucinate; verifies; runs a small evaluation before adopting a tool | Designs the team's use and evaluation of agents; knows what to never delegate |
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
| "How would you evaluate this churn model?" | Held-out data split by time; a baseline; precision and recall at the threshold the business will use, with the cost of each error; calibration if the scores are used as probabilities; a leakage check on any feature that looks too good. |
| "Explain how an LLM works / why it makes things up." | Next-token prediction on a huge corpus; knowledge frozen in weights; plausible is not true; fixes are retrieval, tools, and verification. |
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
- **Models:** Gareth James et al., [*An Introduction to Statistical Learning*](https://www.statlearning.com/) — free, the standard first book; Aurélien Géron, *Hands-On Machine Learning* — the practical companion
- **Deep learning and LLMs:** [3Blue1Brown, Neural networks](https://www.3blue1brown.com/topics/neural-networks) — the visual intuition; Jay Alammar, [*The Illustrated Transformer*](https://jalammar.github.io/illustrated-transformer/); Simon Willison's [weblog](https://simonwillison.net/) for what LLM tools actually do
- **Programming:** Hadley Wickham et al., [*R for Data Science*](https://r4ds.hadley.nz/) or Wes McKinney, *Python for Data Analysis*
- **Charts:** Cole Nussbaumer Knaflic, *Storytelling with Data*
