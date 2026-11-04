# Working with AI agents

> **Definition.** Using AI agents to do parts of the analytical workflow faster, while keeping the judgment, the verification, and the accountability. Knowing what to delegate, how to check what comes back, and what stays yours.

**Why this is a competency and not a tool.** Agents now draft SQL, run a first pass of analysis, and write the first version of the memo. That does not shrink the job; it moves it. The stages where agents are weakest — framing the ask, agreeing metrics, persuading a room, driving a decision — were already where most of the value was. The stages where they are strongest are the ones where an unverified output does the most damage. An analyst who can use agents well *and* evaluate them honestly is more valuable than before; one who cannot evaluate them is more dangerous than before.

This file is cross-cutting, like [collaboration](collaboration.md): it is exercised in every stage and explained in none of them, so it gets its own treatment here.

---

## Where it shows up in the workflow

| Stage | What the agent does well | Where it fails | What stays yours |
|---|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Summarises the thread; lists obvious clarifying questions | Does not know who needs the answer or why | The conversation |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Generates issue trees and hypotheses | Generates too many; cannot rank by what the data can test | The pruning and the scope |
| [3 Define metrics](../workflow.md#stage-3--define-metrics-and-success) | Proposes metrics and guardrails | Invents definitions that conflict with the existing glossary | The negotiation |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Writes SQL fast; drafts quality checks | Fabricates column names; assumes a grain; joins that fan out | Specification and verification |
| [5 Analyse](../workflow.md#stage-5--analyse) | First-pass EDA, segmentation, power calculations, analysis plans | Fits models you did not need; finds a significant segment if allowed to look | Method choice; pre-registration |
| [6 Synthesise](../workflow.md#stage-6--synthesise-into-insight) | Lists findings; pressure-tests a conclusion when asked | Reports fifteen findings with equal confidence | Choosing three and stating confidence |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Drafts and tightens memos and decks | Does not know what this audience needs to hear | The message, and standing behind it |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Sets up monitoring; drafts follow-ups | Cannot chase a decision or notice it was ignored | Follow-through |

Read the third column against the [stages × abilities matrix](../README.md#abilities-by-stage-the-matrix): agents are strongest where technical craft is primary and weakest where collaboration and business acumen are primary. That is the whole argument of this repo in one table.

---

## How to use an agent well

### Delegate tasks, not judgment
A task has a specification and a checkable output: "write a query returning daily checkout-start → order conversion by platform for the last 90 days, one row per day per platform." A judgment has neither: "what's going on with conversion?" Give agents the first kind. Turn the second kind into the first kind yourself — that conversion *is* the analyst's job.

### Specify before you ask
The quality of what comes back is set by what you put in. For data work that means: the tables and their grain, the metric definition, the date range, the expected shape of the result (rows, columns, rough magnitudes). For writing it means: the audience, the decision, the one-sentence answer. An agent given a vague brief will fill the gaps with plausible defaults, and plausible defaults are how wrong answers get through.

### Keep the method decision
Agents reach for the most capable tool, not the most appropriate one. If a segmentation answers the question, do not let a model be built. If an A/B test is the right tool, write the pre-registration (primary metric, sample size, decision rule) before the agent runs anything, so it cannot drift toward whatever looks significant.

### Use agents for the parts of your own work you skip
Most analysts under-invest in Stage 2 (framing) and Stage 6 (synthesis) because they are uncomfortable and unglamorous. Agents make them cheap: "give me ten hypotheses for this drop and the cheapest way to test each" and "what would have to be true for this conclusion to be wrong?" are both excellent prompts. Use the speed to do the thinking you would otherwise skip, not to skip it faster.

### Be honest about what you used
If an agent wrote the query, say so when it matters — in review, in a take-home, when a number is challenged. Hiding it is a credibility risk; owning it and showing the verification is a credibility asset.

---

## How to evaluate what an agent gives you

The question is never "is this output good?" It is "how would I know if it were wrong?" — asked *before* you look at the answer.

### For code and SQL
- **Predict first.** Before running, write down the expected row count and a rough magnitude for the headline number. If the result surprises you, the surprise is the finding — either in the data or in the query.
- **Check the grain.** The single most common agent error is aggregating at the wrong level — sessions where you wanted users, events where you wanted sessions. One `COUNT(DISTINCT …)` against the raw table tells you.
- **Check the joins.** Row count before and after each join. Fan-out is silent.
- **Check the columns exist.** Agents invent plausible column names. Query the schema, not the agent.
- **Reconcile.** Compare the headline figure against an independent source: the finance system, the payments provider, last month's report.

### For analysis and conclusions
- **Ask for the opposite.** "Argue that this conclusion is wrong." A conclusion that survives its own agent-generated rebuttal is worth more.
- **Ask for the assumption.** Every causal claim rests on one. If the agent cannot name it, the claim is not causal.
- **Look for the garden of forking paths.** How many segments, cut-offs, and metric variants were tried before this one was reported? If you do not know, assume many.
- **Check confidence against evidence.** Agents state everything with the same fluency. Re-grade each claim yourself: *established / likely / possible / cannot tell from this data*.

### For writing
- **Does it answer first?** Agent drafts tend to narrate the analysis rather than lead with the recommendation. Reorder.
- **Could you defend every sentence?** If a sentence is in the memo because it sounded right rather than because you checked it, cut it.
- **Is the caveat still there?** Agents drop caveats during "tightening". The caveat from Stage 4 belongs in the memo.

### A one-line test
If you could not reproduce the result without the agent, you do not understand it well enough to put your name on it.

---

## Evaluating AI tools and AI-produced work more formally

Sometimes the question is not "is this one output right?" but "is this agent reliable enough to use for this kind of task?" — for yourself, for a team, or because a stakeholder asked. That is an evaluation problem, and it uses the same discipline as everything else in this repo:

1. **Define the task precisely** (Stage 2) and **the success metric** (Stage 3): accuracy against a known answer, time saved, error rate per query, proportion of outputs needing correction.
2. **Build a small labelled set** — twenty to fifty realistic tasks where you know the right answer. Include the awkward cases: ambiguous asks, schema quirks, questions where the correct response is "cannot tell from this data".
3. **Run it, score it, look at the failures** (Stages 4–6). Failure *types* matter more than the failure rate: a tool that is wrong loudly is safer than one that is wrong fluently.
4. **Decide and write it down** (Stage 7): what it is approved for, what it is not, and what verification is required when it is used.
5. **Re-check after changes** (Stage 8): tools update; an evaluation from six months ago is not an evaluation.

This is also how to answer the increasingly common stakeholder request: "can we just let the AI do this?" The honest answer is an evaluation, not an opinion.

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Delegation** | Uses agents for syntax and drafts | Specifies tasks precisely; keeps method choice | Designs the team's division of labour between people and agents |
| **Verification** | Runs the code and eyeballs the output | Predicts first; checks grain, joins, reconciliation as routine | Sets the team's verification standards; knows which tasks need none and which need all |
| **Judgment** | Accepts fluent outputs | Re-grades confidence; asks for the rebuttal | Knows from experience which agent failures are systematic for which task types |
| **Evaluation** | — | Evaluates a tool for own use with a small labelled set | Runs formal evaluations; decides what the team may and may not delegate |
| **Honesty** | Discloses when asked | Discloses when it matters | Makes disclosure the norm |

---

## Interview lens

This is now asked directly, and it is also assessed silently in take-homes.

**"How do you use AI tools in your work?"**
*What they want:* that you have a considered division of labour, not that you are enthusiastic or sceptical. A strong answer names what you delegate, what you verify and how, and what you keep. Weak answers: "for everything" or "I don't trust it".

> I use agents heavily in Stages 4 to 6 — drafting queries, first-pass segmentation, pressure-testing conclusions — and lightly in the stages that are about people and decisions. For anything that reaches a stakeholder, I predict the result before I run the query, check the grain and the joins, and reconcile against an independent source. If I couldn't reproduce it without the tool, I don't put my name on it.

**"An AI tool gave you an analysis. How would you know if it was wrong?"**
*What they want:* a verification routine, in order. Prediction, grain, joins, schema, reconciliation, assumption behind any causal claim, forking paths. Bonus: "the surprise is the finding".

**"A stakeholder wants to replace an analyst task with an AI agent. What do you do?"**
*What they want:* you treat it as an evaluation, not a debate. Define the task and success metric, build a labelled set, score it, look at the failure types, write down what it is approved for.

**Take-home assignments.** Most now permit or expect AI use. Reviewers look past the code at the verification: did you check what the tool gave you, and can you explain every step? A take-home with visibly agent-written code and no evidence of checking is a worse signal than slower hand-written work.

### Story bank prompts (STAR)
1. A time an agent's output was wrong and how you caught it
2. A task you deliberately did *not* delegate, and why
3. A time AI use let you do framing or synthesis you would otherwise have skipped
4. An evaluation you ran before adopting a tool, and what you decided

---

## Resources

- Ethan Mollick, *Co-Intelligence* — the clearest general account of working alongside AI rather than through it
- [Simon Willison's weblog](https://simonwillison.net/) — practical, sceptical, continuously updated on what LLM tools actually do
- The [workflow page](../workflow.md): the "With AI" section in each stage applies this one stage at a time

---

*Follows the structure of [collaboration.md](collaboration.md): definition and why it matters · where it shows up in the workflow · the substance of the ability · what good looks like by level · interview lens · resources.*
