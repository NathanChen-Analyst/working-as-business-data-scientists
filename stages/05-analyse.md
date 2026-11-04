# Stage 5 — Analyse

> Part of the eight-stage workflow in the [README](../README.md#the-framework). Previous: [Stage 4](04-get-and-trust-the-data.md) · Next: [Stage 6](06-synthesise.md)

**Primary abilities:** Technical craft · Analytical reasoning

## What this stage is
Do the work the question calls for — and no more. The method is chosen by the question:

| Question type | Typical method |
|---|---|
| *What happened?* | Descriptive: segmentation, funnels, cohorts, trend decomposition |
| *Why did it happen?* | Diagnostic: root-cause analysis, contribution analysis, quasi-experimental comparison |
| *What will happen?* | Predictive: forecasting, propensity models |
| *What should we do, and would it work?* | **Causal: randomised controlled trials (A/B tests), or quasi-experiments when randomisation isn't possible** |

**Running example.** Segmentation shows the real 4% drop is concentrated in returning users on a newly introduced payment method. The team wants to test a fallback option. That is an A/B test.

## Hard skills

**Descriptive and diagnostic**
- Segmentation and mix-shift analysis (Simpson's paradox is the classic trap)
- Funnel and cohort analysis
- Time-series basics: seasonality, trend, anomaly detection

**Statistics**
- Distributions, confidence intervals, hypothesis tests, and what a p-value does and does not mean
- Power analysis and minimum detectable effect
- Multiple comparisons; the garden of forking paths

**Experimentation (RCTs / A/B tests)**
- Randomisation unit and its consequences (user vs. session vs. device)
- Sample-size calculation; experiment duration; novelty and primacy effects
- Variance reduction (CUPED), stratification
- Interference and network effects; when a simple A/B test is invalid
- Reading results: primary metric, guardrails, segment heterogeneity, and the discipline not to cherry-pick
- Sequential testing and peeking

**Causal inference when you can't randomise**
- Difference-in-differences, regression discontinuity, synthetic control, instrumental variables, matching — know what assumption each one buys you and when it breaks
- See [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference) for a curated deep dive

**Modelling** (where the role calls for it)
- Regression as a tool for understanding, not just prediction
- Classification and forecasting basics; feature engineering; evaluation that matches the business cost of errors

## Judgment & business skills
- **Proportionality.** A segmentation that answers the question in an afternoon beats a model that answers it in a fortnight.
- **Knowing when an experiment is the right tool** — and when it isn't (too slow, too costly, ethically questionable, interference between units).
- **Pre-registration mindset.** Write down the primary metric, the sample size, and the decision rule *before* the test starts. It protects you from your own future rationalisations.
- **Reporting negative and null results honestly.**

## With AI
Agents run a competent first pass of EDA and segmentation and will happily fit a model you did not need. Keep the method choice yours — it follows from the question, not from what the tool can do. For experiments, agents are useful for power calculations and for drafting the analysis plan, and dangerous for the discipline part: they will find a significant segment if you let them look for one. Pre-register, then let the agent compute.

## Interview lens
- *"Design an A/B test for [feature]."* — Hypothesis, randomisation unit, primary and guardrail metrics, sample size and duration, analysis plan, what you'd do with each outcome.
- *"The test shows a 2% lift with p = 0.04. Ship it?"* — Power, practical vs. statistical significance, guardrails, segment consistency, whether you peeked.
- *"You can't randomise. How would you estimate the effect?"* — Pick a quasi-experimental design and state its assumption.
- *"Explain Simpson's paradox with an example."*
- *"When would you use a model rather than an A/B test?"*

## Resources
- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* — the reference for A/B testing in industry
- [Evan Miller — How Not to Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html)
- Scott Cunningham, [*Causal Inference: The Mixtape*](https://mixtape.scunning.com/) — free online
- [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference)
