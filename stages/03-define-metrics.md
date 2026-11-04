# Stage 3 — Define metrics and success

> Part of the eight-stage workflow in the [README](../README.md#the-framework). Previous: [Stage 2](02-frame-the-question.md) · Next: [Stage 4](04-get-and-trust-the-data.md)

**Primary abilities:** Analytical reasoning · Business acumen · Collaboration & influence

## What this stage is
Choose the measures that map to the decision, agree them with stakeholders, and define what "done" and "success" mean *before* touching data.

**Running example.** "Conversion" turns out to mean three different things to three people: sessions→orders, checkout-starts→orders, and revenue per session. Agree on checkout-starts→orders as the primary metric, revenue per session as a guardrail, and "done" as a memo by Thursday.

## Hard skills
- Metric design: ratios vs. counts, numerator/denominator choice, windowing, attribution
- Guardrail and counter-metrics (what could we accidentally make worse?)
- Leading vs. lagging indicators; proxy metrics and their failure modes
- Variance and minimum detectable effect — if this will become an experiment, know the sample you need *now*

## Judgment & business skills
- Aligning three stakeholders on one definition is a negotiation, not a lookup
- Resisting the metric that is easy to move over the one that matters
- Writing metrics down somewhere permanent so the definition doesn't drift

## With AI
Ask an agent to propose metrics and guardrails for a decision and it will give you a reasonable, generic set. The specific trap is that it will not know your organisation's existing definitions, so it invents new ones that conflict with the glossary. Metric definitions are a negotiation between people; use the agent to draft options, never to settle them.

## Interview lens
- *"How would you measure the success of [feature]?"* — North-star, supporting metrics, guardrails; state the trade-offs.
- *"What's wrong with using average order value as the primary metric here?"* — Skewed distributions, mix effects, gaming.
- *"Define 'active user.'"* — There is no right answer; interviewers want to see you reason about the decision it feeds.

## Resources
- Ron Kohavi, Diane Tang, Ya Xu, *Trustworthy Online Controlled Experiments* — ch. 7 on metrics
- [Lean Analytics](https://leananalyticsbook.com/) — one-metric-that-matters framing
