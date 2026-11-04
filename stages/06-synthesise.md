# Stage 6 — Synthesise into insight

> Part of the eight-stage workflow in the [README](../README.md#the-framework). Previous: [Stage 5](05-analyse.md) · Next: [Stage 7](07-recommend-and-communicate.md)

**Primary abilities:** Analytical reasoning · Business acumen

## What this stage is
Turn analysis output into a small number of claims someone can act on, each with a stated level of confidence. Findings are not insights; an insight says what the finding *means* for the decision.

**Running example.** Three claims: (1) half the headline drop is a tracking break — fix the instrumentation; (2) the real drop is a payment-method failure for returning users, costing ~€X/week; (3) the proposed fallback is testable in two weeks and we have the sample to detect a 2pp effect.

## Hard skills
- Effect-size and uncertainty communication
- Sensitivity checks: does the conclusion survive reasonable changes in assumptions?
- Separating signal from noise — resisting the narrative that fits a random fluctuation

## Judgment & business skills
- **Ruthless prioritisation.** Three claims that matter beat twelve that are true.
- Stating confidence honestly: "likely," "possible," "we can't tell from this data."
- Sizing the problem in business terms (money, users, time), not in analytical terms (percentage points, coefficients).

## With AI
An agent will produce fifteen findings with equal confidence. Synthesis is choosing three and saying how sure you are — exactly the judgment an agent lacks, because it does not know what the decision-maker already believes or what is at stake. Use it to pressure-test: "what would have to be true for this conclusion to be wrong?" is a good prompt here.

## Interview lens
- *"You found 15 interesting things. Which do you present?"*
- *"How confident are you in that conclusion, and why?"*
- Take-home assignments are scored heavily on this stage — reviewers look for whether you drew conclusions or just produced charts.
