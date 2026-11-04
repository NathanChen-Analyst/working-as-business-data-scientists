# Stage 4 — Get and trust the data

> Part of the eight-stage workflow in the [README](../README.md#the-framework). Previous: [Stage 3](03-define-metrics.md) · Next: [Stage 5](05-analyse.md)

**Primary abilities:** Technical craft · Collaboration & influence

## What this stage is
Source the data, check it, and understand its limits well enough to know what it *cannot* tell you.

**Running example.** Checkout events are logged client-side; a 14 October iOS release changed the event name for one step. Half the "drop" is a tracking break. The remaining 4% is real.

## Hard skills
- **SQL** — joins, window functions, CTEs, aggregation at the right grain; this is the single most-tested skill in analyst interviews
- Data-quality checks: row counts over time, null rates, duplicates, schema changes, reconciliation against an independent source
- Event-tracking literacy: client vs. server events, sessionisation, identity resolution
- Python/R for anything SQL can't do cleanly (pandas, dplyr)

## Judgment & business skills
- Knowing when data quality is "good enough for this decision" versus "needs fixing before anyone acts on it"
- Documenting caveats as you go, so they make it into the final memo
- Building relationships with data engineering — they know where the bodies are buried

## With AI
This is where agents help most and fail most quietly. They write SQL fast and fluently; they also invent column names, assume a grain, and join tables that fan out. The job shifts from writing queries to *specifying and verifying* them: state the grain and the expected row count before you ask, and reconcile the result against an independent source before you trust it. An agent-written query you did not check is not your analysis.

## Interview lens
- *"The numbers look wrong. What do you check?"* — Tracking changes, time-zone and date boundaries, duplicates, filter logic, join fan-out, late-arriving data.
- Live SQL rounds: funnel conversion by step, retention cohorts, top-N per group, running totals.

## Resources
- [Mode SQL Tutorial](https://mode.com/sql-tutorial/) — the standard free reference
- [Select Star SQL](https://selectstarsql.com/) — interactive, interview-style practice
- [Data Science Interview Questions & Answers (youssefHosni)](https://github.com/youssefHosni/Data-Science-Interview-Questions-Answers) — SQL and statistics sections
