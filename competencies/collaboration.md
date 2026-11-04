# Collaboration & influence

> **Definition.** Getting work done with and through other people: understanding what they need, agreeing what will be done, working alongside data engineering, product, engineering, and other analysts, and getting decisions made and resources committed when you own neither.

**Why it matters more than it looks.** An analyst almost never owns the data pipeline, the product roadmap, the engineering backlog, or the final decision. Every piece of work depends on someone else building, approving, or acting. Collaboration is the primary ability in five of the eight workflow stages — more than any other — and it is what most behavioural interview questions are actually probing.

---

## Where it shows up in the workflow

| Stage | What collaboration looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Stakeholder discovery; reading what's really being asked; finding out who else cares | ●● |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Agreeing scope in writing; treating the stakeholder's theory as one hypothesis without dismissing it | ● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Negotiating one metric definition across three people who each have their own | ●● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Working with data engineering; reporting data issues usefully; knowing what's cheap vs. expensive to ask for | ●● |
| [5 Analyse](../workflow.md#stage-5--analyse) | Coordinating experiment instrumentation and launch with engineering; peer review of analysis | ● |
| [6 Synthesise](../workflow.md#stage-6--synthesise-into-insight) | Pressure-testing conclusions with a colleague before they go out | ○ |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Pre-wiring the audience; handling pushback; tailoring to each stakeholder | ●● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Chasing the decision; getting engineering time committed; closing the loop | ●● |

---

## The toolkit

Collaboration's "frameworks" are fewer and plainer than the other abilities' — mostly named habits. The ones worth knowing by name:

- **Stakeholder mapping** — *Who cares, who decides, who can block?* A two-by-two of interest × influence tells you who to pre-wire and who to inform. Stage 1 and 7.
- **The scope agreement** — *What will I do, not do, by when?* Two sentences, in writing, before starting. Stage 2.
- **RACI (responsible, accountable, consulted, informed)** — *Who owns which part of this?* Overkill for most analyses; invaluable for experiments, where engineering, product, and analytics each own a piece. Stage 5.
- **Pre-wiring** — *Who should hear this before the room does?* Stage 7.
- **Disagree and commit** — *Can I argue my case fully and then support the decision?* The alternative — relitigating decisions — costs more credibility than losing the argument. Stage 7 and 8.
- **Non-violent pushback** — observation, impact, request: "the metric changed definition mid-quarter; it makes the trend unreadable; can we agree one definition and backfill?" Stage 3 and 4.

The rest of this ability is about relationships, and is best described by who they are with.

## The five relationships

### 1. With product managers and business owners (the people who ask)
- **Discovery, not order-taking.** Ask what decision they're facing and what they'd do with each possible answer. If no answer would change what they do, say so.
- **Scope agreement in writing.** Two sentences in a channel: what you'll check, what you won't, by when. Invite pushback before you start, not after.
- **Mid-project expectation management.** Share a rough finding early rather than a polished one late. A Tuesday "it looks like it's iOS, still confirming" is worth more than a Friday deck.
- **Their theory is a hypothesis.** Not the frame, and not something to dismiss. Test it first if it's cheap — it builds trust either way.

### 2. With data engineering (the people who own the data)
- **Ask well.** Bring the table, the column, the date range, and the specific discrepancy. "The numbers look off" is not a bug report.
- **Know the cost of what you're asking for.** A new column in an existing table is cheap; a new event in the client is a release cycle. Ask accordingly.
- **Report issues as contributions.** A data-quality finding with a reproducible query is a gift. The same finding delivered as a complaint is a tax.
- **Build the relationship before you need it.** They know where the undocumented joins and the silent tracking breaks are.

### 3. With engineering (the people who build and ship)
- **Experiments need instrumentation, randomisation, and a launch.** All three are engineering work. Scope them into the plan from the start.
- **Translate.** Engineers need a precise spec (randomisation unit, bucketing logic, events to fire); they don't need the statistical rationale unless they ask.
- **Respect the sprint.** Your urgent is not their urgent. Make the business case for priority to the PM, not to the engineer.

### 4. With other analysts (the people doing the same job)
- **Peer review.** Have someone else read your SQL and your conclusions before they go to a stakeholder. Offer the same back, promptly.
- **Shared definitions.** If three analysts define "active user" three ways, every stakeholder loses trust in all of them. Maintain the metric glossary together.
- **Handoffs and reuse.** Document so the next person doesn't redo your work. Check whether the question has already been answered before you start.
- **Don't duplicate; divide.** When two analysts are circling the same question, split it.

### 5. Cross-functional influence (getting things to happen without authority)
- **Pre-wire.** Walk the key people through the finding individually before the group meeting. Surprises in a room create defensiveness; the same information shared one-on-one creates allies.
- **Make the decision easy.** Present options with a recommendation, not a menu. Name the cost of not deciding.
- **Trade in credibility.** Every honest null result, every caveat you volunteered, every time you said "I don't know" — these are what make people act on your next recommendation.
- **Escalate early and lightly.** "Heads up, this might slip" on Wednesday beats "it slipped" on Friday.

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Stakeholders** | Takes the ask as given; clarifies when prompted | Runs discovery unprompted; agrees scope in writing | Reshapes the ask; declines or redirects low-value work; stakeholders come to them *before* forming the question |
| **Data engineering** | Reports issues; asks for help | Files reproducible issues; knows the data model | Shapes what gets instrumented; co-owns the metric layer |
| **Engineering** | Hands over a spec | Scopes experiment work into the plan; coordinates launch | Negotiates priority; designs experiments around engineering constraints |
| **Other analysts** | Asks for review | Reviews others' work; contributes to shared definitions | Sets review norms; owns the glossary; mentors |
| **Influence** | Presents findings | Pre-wires, handles pushback, gets decisions made | Changes what the organisation measures and how it decides |

---

## Interview lens

Collaboration is almost never asked about directly. It is probed through behavioural questions and through how you handle the case interview itself.

### Behavioural questions that are really about collaboration

**"Tell me about a time you disagreed with a stakeholder."**
*What they want:* that you distinguished "wrong about the data" from "wrong about the decision," that you engaged rather than folded or dug in, and how it resolved. A strong answer names what you did to understand their view before pushing yours.

**"Tell me about a time you needed something from another team and they said no."**
*What they want:* that you understood their constraints, found a smaller ask or a trade, and escalated appropriately if needed — not that you went around them.

**"Describe a time you had to influence a decision you didn't own."**
*What they want:* pre-wiring, options-with-a-recommendation, naming the cost of inaction, and a result. Bonus: a time it didn't work and what you learned.

**"How do you handle it when a PM asks for the wrong analysis?"**
*What they want:* you take their theory seriously as a hypothesis, reframe around the decision, agree scope, and keep the relationship.

**"Tell me about a mistake you made and how you handled it."**
*What they want:* you told the affected people yourself, early, with a fix. Collaboration under pressure.

### How collaboration shows up in case interviews
- Asking clarifying questions before diving in (Stage 1 behaviour) signals you'll do the same with real stakeholders.
- Saying "I'd check with data engineering whether that event is reliable" or "I'd confirm the metric definition with the PM" is a plus, not a dodge.
- Responding to the interviewer's pushback by engaging with it — "that's a fair point, if that were true I'd expect to see X" — is the thing they're watching for.

### Story bank prompts (STAR)
Prepare one story for each; quantify the result; add one line on what you'd do differently.

1. A stakeholder disagreement, resolved
2. A request to another team that was refused or delayed
3. A decision you influenced without owning it
4. A scope that changed mid-project and how you handled it
5. A data issue you found and how you reported it
6. Delivering an unwelcome result to someone senior

---

## Resources

- Chris Voss, *Never Split the Difference* — negotiation framing that transfers directly to scope and priority conversations
- Kim Scott, *Radical Candor* — on disagreeing without damaging the relationship
- Jeff Patton, *User Story Mapping* — for understanding how product teams think about scope
- [Cassie Kozyrkov — Decision Intelligence (Towards Data Science)](https://towardsdatascience.com/tagged/decision-intelligence) — on the analyst–decision-maker relationship

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
