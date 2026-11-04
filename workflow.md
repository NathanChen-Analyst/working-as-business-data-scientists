# The day-to-day workflow

**All eight stages on one page.** The [README](README.md#day-to-day-workflow-stage-framework) shows the shape; this page is the full account, stage by stage, with one case — *"checkout conversion dropped 8% last month"* — running through it.

## How to read this page

Every stage has the same sections, in the same order, so you can read straight through or jump to the part you need:

| Section | What it answers |
|---|---|
| **What this stage is** | The job to be done, and what "good" looks like |
| **Hard skills** | The technical competence the stage requires |
| **Judgment & business skills** | The non-technical competence — usually what separates a good analyst from an average one |
| **With AI** | What to delegate to an agent at this stage, and what goes wrong |
| **Interview lens** | The questions interviewers ask to probe this stage, with worked answers |
| **Resources** | A few things worth reading — short and opinionated |

Stage 4 has one extra section, **Where the data lives**, on the data platform. Stage 2 is the most fully worked and is the template the others follow. Each stage ends with a link back to this list.

## Contents

- **Frame** · *business judgment*
  - [Stage 1 — Receive the ask](#stage-1--receive-the-ask)
  - [Stage 2 — Frame the question](#stage-2--frame-the-question)
  - [Stage 3 — Define metrics and success](#stage-3--define-metrics-and-success)
- **Analyse** · *technical craft*
  - [Stage 4 — Get and trust the data](#stage-4--get-and-trust-the-data)
  - [Stage 5 — Analyse](#stage-5--analyse)
  - [Stage 6 — Synthesise into insight](#stage-6--synthesise-into-insight)
- **Act** · *persuasion & follow-through*
  - [Stage 7 — Recommend and communicate](#stage-7--recommend-and-communicate)
  - [Stage 8 — Drive the decision and measure the outcome](#stage-8--drive-the-decision-and-measure-the-outcome)

---

<a id="frame"></a>

## Frame · business judgment

## Stage 1 — Receive the ask

**Primary abilities:** Business acumen · Collaboration & influence

### What this stage is
A stakeholder brings you something. It is rarely a well-posed question. Your job is to understand *who* is asking, *what decision* they are facing, and *what they actually need* — which is often different from what they said.

**Running example.** A product manager messages: *"Checkout conversion is down 8% month-over-month. Can you look into it?"*

### Hard skills
- Enough domain and data-model familiarity to ask informed questions on the spot
- Knowing which dashboards, tables, and prior analyses already exist

### Judgment & business skills
- **Stakeholder discovery.** Who else cares about this? Who will act on the answer? Who might disagree with it?
- **Reading the ask.** Is this a *why* question (diagnosis), a *what should we do* question (decision), or a *how bad is it* question (sizing)? Each needs a different analysis.
- **Timeline and stakes.** A two-hour sanity check and a two-week deep dive are both valid answers. Find out which one is wanted before you start.
- **Pushing back gracefully.** Sometimes the right response is "that's already answered here" or "that's not a data question."

### With AI
An agent can summarise the thread, pull up the existing dashboards, and list the obvious clarifying questions in seconds. It cannot tell you who actually needs the answer or what they will do with it — that still comes from a conversation. Use the agent to arrive at that conversation prepared, not to replace it.

### Interview lens
- *"A PM says conversion is down. What do you do first?"* — Interviewers want to hear clarifying questions before any SQL: Over what period? Which funnel step? Which platforms and segments? Was anything shipped? Is it a real decline or a tracking change?
- *"Tell me about a time a stakeholder asked for the wrong thing."* — Behavioural; see [The six abilities](competencies/).

[↑ back to contents](#contents)

---

## Stage 2 — Frame the question

**Primary abilities:** Analytical reasoning · Business acumen

### What this stage is
Turn the ask into a precise, answerable question with explicit hypotheses, scope, and a definition of done. This is the stage most analysts skip, and the one that most often sinks a project.

A good frame answers four things (CoNVO):

| | Question | Running example |
|---|---|---|
| **Context** | Who is asking and what is the organisational situation? | Growth team; Q4 targets at risk; leadership review in 10 days |
| **Need** | What does the stakeholder need to *know* in order to act? | Whether the drop is real, what is driving it, and whether it is fixable before quarter end |
| **Vision** | What will the output look like? | A one-page memo with a ranked list of causes and a recommended action |
| **Outcome** | What changes once they have it? | A go/no-go on diverting engineering time to checkout this sprint |

### Hard skills
- **Hypothesis structuring.** Build an issue tree: the 8% drop is either a *measurement artefact* or a *real change*; a real change is either *fewer people entering checkout* or *fewer completing it*; completion drops split by *platform*, *payment method*, *new vs. returning*, *geography*, and *time of day*; and so on until each leaf is directly testable.
- **Scoping with data.** Know, before committing, whether the event tracking can actually distinguish the branches of your tree.
- **Prioritising hypotheses.** Rank by (a) prior likelihood and (b) cost to test. Check the cheap, likely ones first — "did a deploy happen on the day the drop started?" takes five minutes.

### Judgment & business skills
- **Separating the question from the answer the stakeholder already has.** PMs often arrive with a theory. Treat it as one hypothesis, not the frame.
- **Agreeing scope in writing.** Two sentences in a channel — "I'm going to check X, Y, Z by Thursday; I am *not* going to look at W" — prevents the most common failure mode, which is discovering on Friday that W was the point.
- **Deciding what would change the decision.** If the answer to "is it fixable before quarter end?" is no either way, the deep dive on causes can wait.
- **Knowing when to stop framing.** Thirty minutes to an hour for most asks. Perfection here is procrastination.

### With AI
Agents are good at generating issue trees and hypothesis lists, and they generate *too many*. The value you add is pruning: which branches the data can actually test, which are cheap to check first, which would change the decision. Ask the agent for the tree, then cut it in half yourself and write down why.

### Interview lens

**Q: "Conversion dropped 8%. Walk me through how you'd investigate."**

*What they are testing:* structured thinking, not SQL. A strong answer looks like:

> First I'd confirm it's real: check whether event tracking changed, compare against an independent source like order counts in the payments system, and see if the drop is a step change or a gradual slide.
>
> If it's real, I'd split the funnel — is it fewer people reaching checkout, or fewer completing it? Then I'd segment the step that moved by platform, new vs. returning users, payment method, country, and device, looking for a segment that explains most of the delta.
>
> In parallel I'd check external causes: releases, pricing changes, marketing mix shifts, seasonality, competitor activity.
>
> I'd time-box this to two days and come back with either a likely cause and a proposed fix, or a clear statement of what I ruled out and what I'd need to go further.

*Common weak answers:* jumping straight to "I'd build a model," listing every metric without a structure, or not mentioning the measurement-artefact check.

**Q: "How do you decide what's in and out of scope?"**

> I ask what decision the analysis is feeding and when it's due. Anything that wouldn't change that decision, or can't be done by the deadline, is out. I write the scope down and share it so the stakeholder can push back before I start rather than after.

**Q: "What's the difference between a question and a hypothesis?"**

> A question is open: "why did conversion drop?" A hypothesis is a specific, falsifiable claim: "the drop is concentrated in iOS users after the 14 October release." You can only test the second kind, so framing means converting the first into a set of the second.

### Resources
- Max Shron, *Thinking with Data* (O'Reilly, 2014) — CoNVO, short and essential
- Barbara Minto, *The Pyramid Principle* — the origin of issue trees and answer-first structure
- [Emma Ding — Cracking Product Sense / Metric / Business Case problems](https://www.youtube.com/@emma_ding) — the interview-side version of this stage

[↑ back to contents](#contents)

---

## Stage 3 — Define metrics and success

**Primary abilities:** Analytical reasoning · Business acumen · Collaboration & influence

### What this stage is
Choose the measures that map to the decision, agree them with stakeholders, and define what "done" and "success" mean *before* touching data.

**Running example.** "Conversion" turns out to mean three different things to three people: sessions→orders, checkout-starts→orders, and revenue per session. Agree on checkout-starts→orders as the primary metric, revenue per session as a guardrail, and "done" as a memo by Thursday.

### Hard skills
- Metric design: ratios vs. counts, numerator/denominator choice, windowing, attribution
- Guardrail and counter-metrics (what could we accidentally make worse?)
- Leading vs. lagging indicators; proxy metrics and their failure modes
- Variance and minimum detectable effect — if this will become an experiment, know the sample you need *now*

### Judgment & business skills
- Aligning three stakeholders on one definition is a negotiation, not a lookup
- Resisting the metric that is easy to move over the one that matters
- Writing metrics down somewhere permanent so the definition doesn't drift

### With AI
Ask an agent to propose metrics and guardrails for a decision and it will give you a reasonable, generic set. The specific trap is that it will not know your organisation's existing definitions, so it invents new ones that conflict with the glossary. Metric definitions are a negotiation between people; use the agent to draft options, never to settle them.

### Interview lens
- *"How would you measure the success of [feature]?"* — North-star, supporting metrics, guardrails; state the trade-offs.
- *"What's wrong with using average order value as the primary metric here?"* — Skewed distributions, mix effects, gaming.
- *"Define 'active user.'"* — There is no right answer; interviewers want to see you reason about the decision it feeds.

### Resources
- Ron Kohavi, Diane Tang, Ya Xu, *Trustworthy Online Controlled Experiments* — ch. 7 on metrics
- [Lean Analytics](https://leananalyticsbook.com/) — one-metric-that-matters framing

[↑ back to contents](#contents)

---

<a id="analyse"></a>

## Analyse · technical craft

## Stage 4 — Get and trust the data

**Primary abilities:** Technical craft · Collaboration & influence

### What this stage is
Source the data, check it, and understand its limits well enough to know what it *cannot* tell you.

**Running example.** Checkout events are logged client-side; a 14 October iOS release changed the event name for one step. Half the "drop" is a tracking break. The remaining 4% is real.

### Where the data lives

Before you can query anything you need to know how your organisation's data platform is put together. The names differ by company; the layers are nearly universal.

| Layer | What it is | Typical tools | What you need to know about it |
|---|---|---|---|
| **Sources** | The systems where data is created: the product database, payment provider, CRM, ad platforms, support tool | Postgres/MySQL replicas, Stripe, Salesforce, HubSpot, Zendesk | Which system is the *source of truth* for each entity. Revenue lives in the payments system, not in the product events. |
| **Event tracking** | Instrumentation that records what users do in the product | Segment, Amplitude, Mixpanel, Google Analytics, Snowplow, in-house | Client-side events can be blocked, duplicated, or renamed in a release; server-side events are more reliable but sparser. Know which yours are. |
| **Warehouse / lakehouse** | Where everything is copied and stored for analysis | Snowflake, BigQuery, Redshift, Databricks; dbt-modelled schemas on top | The raw layer mirrors sources; the modelled layer is what you should query. Queries cost money on most platforms — know roughly what a scan costs. |
| **Transformation** | The code that turns raw tables into clean, documented, tested models | dbt, Dataform, SQLMesh, Airflow/Dagster for orchestration | Read the model definitions. The lineage graph tells you where a column came from; the tests tell you what has been checked. |
| **Semantic / metrics layer** | The agreed definitions of business metrics, encoded once | dbt metrics, Looker's LookML, Cube, a governed BI layer | If a metric exists here, use it. If your number differs from the governed one, you have to explain why before anyone will believe you. |
| **BI / dashboards** | Where stakeholders look at data without you | Looker, Tableau, Power BI, Metabase, Mode, Hex | What stakeholders already see shapes what they will ask. Check the dashboard before answering the question it generated. |
| **Catalog / docs** | Where tables, owners, and definitions are described | dbt docs, DataHub, Atlan, Alation, a wiki | The first place to look, and the first thing to improve when it's wrong. |

Three practical habits that follow from this:

- **Start at the modelled layer, not the raw tables.** The modelled tables are tested, documented, and consistent with what everyone else uses. Go to raw only when the model doesn't have what you need — and then tell the data engineers, because that is a gap in the model.
- **Find the owner before you find the table.** Every table has someone who knows its quirks. Ten minutes with them saves a day of discovering that `user_id` means something different after March.
- **Know the freshness.** Most warehouses load on a schedule. A query run at 09:00 may be looking at data that ended at midnight. Check the load timestamp before you report a "drop" that is really a half-loaded day.

### Hard skills
- **SQL** — joins, window functions, CTEs, aggregation at the right grain; this is the single most-tested skill in analyst interviews. Dialects differ slightly between warehouses (date functions, `QUALIFY`, array handling); learn yours.
- **Platform literacy** — navigating the warehouse, reading dbt models and lineage, using the catalog, understanding load schedules and query cost
- Data-quality checks: row counts over time, null rates, duplicates, schema changes, reconciliation against an independent source
- Event-tracking literacy: client vs. server events, sessionisation, identity resolution
- Python/R for anything SQL can't do cleanly (pandas, dplyr); notebooks (Jupyter, Hex, Deepnote) for exploration that needs to be reproducible

### Judgment & business skills
- Knowing when data quality is "good enough for this decision" versus "needs fixing before anyone acts on it"
- Documenting caveats as you go, so they make it into the final memo
- Building relationships with data engineering — they know where the bodies are buried

### With AI
This is where agents help most and fail most quietly. They write SQL fast and fluently; they also invent column names, assume a grain, and join tables that fan out. The job shifts from writing queries to *specifying and verifying* them: state the grain and the expected row count before you ask, and reconcile the result against an independent source before you trust it. An agent-written query you did not check is not your analysis.

### Interview lens
- *"The numbers look wrong. What do you check?"* — Load freshness, tracking changes, time-zone and date boundaries, duplicates, filter logic, join fan-out, late-arriving data.
- *"Walk me through your company's data stack."* — Sources → tracking → warehouse → transformation → metrics layer → BI. Interviewers want to hear that you know which layer to query and why, not a list of logos.
- *"Your number doesn't match the dashboard. What now?"* — Find the governed definition, diff the two queries, explain the difference before reporting either number.
- Live SQL rounds: funnel conversion by step, retention cohorts, top-N per group, running totals.

### Resources
- [dbt — What is analytics engineering?](https://www.getdbt.com/what-is-analytics-engineering) — the modern warehouse stack from the transformation side
- [Mode SQL Tutorial](https://mode.com/sql-tutorial/) — the standard free reference
- [Select Star SQL](https://selectstarsql.com/) — interactive, interview-style practice
- [Data Science Interview Questions & Answers (youssefHosni)](https://github.com/youssefHosni/Data-Science-Interview-Questions-Answers) — SQL and statistics sections

[↑ back to contents](#contents)

---

## Stage 5 — Analyse

**Primary abilities:** Technical craft · Analytical reasoning

### What this stage is
Do the work the question calls for — and no more. The method is chosen by the question:

| Question type | Typical method |
|---|---|
| *What happened?* | Descriptive: segmentation, funnels, cohorts, trend decomposition |
| *Why did it happen?* | Diagnostic: root-cause analysis, contribution analysis, quasi-experimental comparison |
| *What will happen?* | Predictive: forecasting, propensity models |
| *What should we do, and would it work?* | **Causal: randomised controlled trials (A/B tests), or quasi-experiments when randomisation isn't possible** |

**Running example.** Segmentation shows the real 4% drop is concentrated in returning users on a newly introduced payment method. The team wants to test a fallback option. That is an A/B test.

### Hard skills

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

### Judgment & business skills
- **Proportionality.** A segmentation that answers the question in an afternoon beats a model that answers it in a fortnight.
- **Knowing when an experiment is the right tool** — and when it isn't (too slow, too costly, ethically questionable, interference between units).
- **Pre-registration mindset.** Write down the primary metric, the sample size, and the decision rule *before* the test starts. It protects you from your own future rationalisations.
- **Reporting negative and null results honestly.**

### With AI
Agents run a competent first pass of EDA and segmentation and will happily fit a model you did not need. Keep the method choice yours — it follows from the question, not from what the tool can do. For experiments, agents are useful for power calculations and for drafting the analysis plan, and dangerous for the discipline part: they will find a significant segment if you let them look for one. Pre-register, then let the agent compute.

### Interview lens
- *"Design an A/B test for [feature]."* — Hypothesis, randomisation unit, primary and guardrail metrics, sample size and duration, analysis plan, what you'd do with each outcome.
- *"The test shows a 2% lift with p = 0.04. Ship it?"* — Power, practical vs. statistical significance, guardrails, segment consistency, whether you peeked.
- *"You can't randomise. How would you estimate the effect?"* — Pick a quasi-experimental design and state its assumption.
- *"Explain Simpson's paradox with an example."*
- *"When would you use a model rather than an A/B test?"*

### Resources
- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* — the reference for A/B testing in industry
- [Evan Miller — How Not to Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html)
- Scott Cunningham, [*Causal Inference: The Mixtape*](https://mixtape.scunning.com/) — free online
- [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference)

[↑ back to contents](#contents)

---

## Stage 6 — Synthesise into insight

**Primary abilities:** Analytical reasoning · Business acumen

### What this stage is
Turn analysis output into a small number of claims someone can act on, each with a stated level of confidence. Findings are not insights; an insight says what the finding *means* for the decision.

**Running example.** Three claims: (1) half the headline drop is a tracking break — fix the instrumentation; (2) the real drop is a payment-method failure for returning users, costing ~€X/week; (3) the proposed fallback is testable in two weeks and we have the sample to detect a 2pp effect.

### Hard skills
- Effect-size and uncertainty communication
- Sensitivity checks: does the conclusion survive reasonable changes in assumptions?
- Separating signal from noise — resisting the narrative that fits a random fluctuation

### Judgment & business skills
- **Ruthless prioritisation.** Three claims that matter beat twelve that are true.
- Stating confidence honestly: "likely," "possible," "we can't tell from this data."
- Sizing the problem in business terms (money, users, time), not in analytical terms (percentage points, coefficients).

### With AI
An agent will produce fifteen findings with equal confidence. Synthesis is choosing three and saying how sure you are — exactly the judgment an agent lacks, because it does not know what the decision-maker already believes or what is at stake. Use it to pressure-test: "what would have to be true for this conclusion to be wrong?" is a good prompt here.

### Interview lens
- *"You found 15 interesting things. Which do you present?"*
- *"How confident are you in that conclusion, and why?"*
- Take-home assignments are scored heavily on this stage — reviewers look for whether you drew conclusions or just produced charts.

[↑ back to contents](#contents)

---

<a id="act"></a>

## Act · persuasion & follow-through

## Stage 7 — Recommend and communicate

**Primary abilities:** Business acumen · Communication · Collaboration & influence

### What this stage is
Deliver a recommendation, structured so the audience can act on it, in the format and length they will actually consume. This is the stage where most of the value is created or lost.

**Running example.** A one-page memo: recommendation first ("Fix tracking today; A/B test the payment fallback starting Monday; expected recovery of ~€X/week if it works"), then the three supporting claims, then caveats and next steps. Appendix with the detailed segmentation for anyone who wants it.

### Hard skills
- Data visualisation: chart choice, decluttering, annotation, one message per chart
- Memo and deck structure: answer first, then evidence, then detail (Pyramid Principle)
- Translating statistics for non-technical readers — coefficients, p-values, intervals, null results — and keeping findings, interpretation, conclusions, and limitations as four labelled layers; see [communication](competencies/communication.md#explaining-statistical-results-to-non-technical-audiences)
- Dashboards vs. one-off analyses — knowing which the situation needs

### Judgment & business skills
- **Audience tailoring.** The CFO, the PM, and the engineer need different versions of the same result.
- **Anticipating objections** and addressing them before they're raised.
- **Handling pushback** without either folding or digging in — distinguishing "you're wrong about the data" from "you're wrong about what we should do."
- **Delivering unwelcome results.** The test failed; the pet project isn't working; the metric was wrong all along.

### With AI
First drafts are nearly free now. What remains scarce is knowing what this audience needs to hear, in what order, and being willing to stand behind the recommendation when challenged. Let the agent draft and tighten; decide the message yourself, and never send a recommendation you could not defend without the tool in the room.

### Interview lens
- Presentation rounds and take-home readouts: structure, clarity, handling questions
- *"Tell me about a time your analysis was challenged."*
- *"How would you explain a confidence interval to a non-technical executive?"*

### Resources
- Cole Nussbaumer Knaflic, *Storytelling with Data*
- Barbara Minto, *The Pyramid Principle*
- [Lea Pica — Present Beyond Measure](https://leapica.com/) — data presentation for analysts

[↑ back to contents](#contents)

---

## Stage 8 — Drive the decision and measure the outcome

**Primary abilities:** Business acumen · Collaboration & influence · Ownership & delivery

### What this stage is
An analysis that doesn't change anything was a cost, not a contribution. This stage is about making sure a decision gets made, the action gets taken, and the outcome gets measured — which becomes the next ask.

**Running example.** Tracking is fixed; the A/B test ships; two weeks later the fallback shows a 1.8pp lift on the primary metric with guardrails flat. Rollout decision made. Three months later: is the lift still there? Did it change the metric definition conversation?

### Hard skills
- Experiment monitoring and post-launch measurement
- Dashboards and alerting for the metrics you recommended watching
- Basic deployment literacy (where DS roles own models in production)

### Judgment & business skills
- **Follow-through.** Scheduling the check-in, chasing the decision, closing the loop with the stakeholder.
- **Measuring adoption**, not just accuracy: was the recommendation acted on?
- **Learning from the ones that didn't land** — why didn't the analysis change anything?
- Keeping a personal log of decisions influenced; this is your evidence of impact at review time and in interviews.

### With AI
Agents can set up monitoring queries and draft the follow-up messages. They cannot chase a decision, notice that the recommendation was quietly ignored, or close the loop with a stakeholder. Follow-through is a human act. The one thing worth automating here is the reminder to do it.

### Interview lens
- *"Tell me about a project and its impact."* — Interviewers want a measurable outcome and your specific contribution, not a description of the method.
- *"What happened after you delivered the analysis?"* — A surprisingly discriminating question; many candidates don't know.

[↑ back to contents](#contents)

---
