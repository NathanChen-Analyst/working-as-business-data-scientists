# Communication

> **Definition.** Getting a finding into someone else's head in a form they can act on: answer-first structure, tailoring to the audience, charts that carry one message each, delivering unwelcome results, and handling challenge without folding or digging in.

**Why it matters.** An analysis that is correct and unread changed nothing. Communication is where the value created in six stages is either realised or lost, and it is the ability whose absence is most visible to stakeholders — they cannot judge your SQL, but they can tell whether your memo answered their question. It is primary in Stage 7 and supporting almost everywhere else, because every stage involves telling someone something.

---

## Where it shows up in the workflow

| Stage | What communication looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Asking clarifying questions that don't sound like obstruction; reflecting the ask back | ● |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Writing the two-sentence scope agreement so it is read and agreed | ● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Explaining why one definition is better than another to people who prefer theirs | ● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Reporting a data problem usefully; writing a caveat that survives to the memo | ○ |
| [5 Analyse](../workflow.md#stage-5--analyse) | A mid-project "here's what it looks like so far" that is useful without being over-claimed | ○ |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Phrasing claims at the right confidence; sizing in the audience's units | ● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | The memo, the deck, the chart, the meeting, the pushback | ●● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | The follow-up that keeps the decision alive; the honest post-mortem | ● |

---

## The toolkit

### Structure

**Answer first (the Pyramid Principle)** — *What is the one thing they need to know?* Lead with the recommendation, then the supporting claims, then the evidence, then the detail. The reader can stop at any level and have the right picture. Stage 7, and every message longer than a sentence. *Running example:* "Fix tracking today; A/B test the payment fallback from Monday; expected recovery about €24k of margin a week" is the first line of the memo, not the last.

**SCQA (Situation, Complication, Question, Answer)** — *How do I open so they want the answer?* Where we were, what changed, the question that raises, the answer. Four sentences that make any memo or deck readable. Stage 7.

**The one-page memo** — *Can the whole thing fit on a page?* Recommendation, three supporting claims, caveats, next steps; appendix for the detail. If it does not fit, the synthesis in Stage 6 is not finished. Stage 7.

**The rule of three** — three claims, three options, three next steps. Not because three is magic, but because four is where attention goes.

### Audience

**Audience mapping** — *Who is reading, what do they already believe, and what do they need to do?* The CFO needs the money and the risk; the PM needs the cause and the fix; the engineer needs the spec. One analysis, three versions. Stage 7.

**Level of detail by altitude** — executives get the answer and the size; managers get the claims and the trade-offs; practitioners get the method. Sending the practitioner version to the executive is the commonest failure.

**Pre-wiring** — *Who should hear this before the meeting?* Walking key people through the finding one-on-one turns surprise into support. The [collaboration](collaboration.md) side of communication. Stage 7.

### Charts

**Chart choice** — *What comparison am I showing?* Change over time → line; comparison across categories → bar (sorted); part of a whole → bar or stacked bar, rarely pie; relationship → scatter; distribution → histogram or box. Stage 7.

**One message per chart** — *If this chart had a title that was a sentence, what would it say?* Make that the title. Remove everything that doesn't support it: gridlines, legends that can be labels, colours that don't mean anything.

**Annotation over legend** — label the line, mark the event, circle the point. The reader should not have to decode.

**Uncertainty shown honestly** — intervals where they matter, and not where they clutter; never a chart that implies more precision than the analysis has.

### Delivering difficult results

**Unwelcome news** — *How do I say "it didn't work" so it is heard?* Lead with it, state what was learned, propose the next step. Burying it in slide nine is read as evasion.

**Handling pushback** — *Is the challenge about the data or about the decision?* "Your numbers are wrong" is answered with the verification; "we shouldn't do that" is a different conversation, about priorities, and should be treated as one. Engage with the strongest version of the objection.

**Saying "I don't know"** — with what you would need in order to know. It builds more credibility than a confident guess.

### Explaining statistical results to non-technical audiences

The commonest communication failure in analytics is not a bad chart; it is a correct result reported in the analyst's language rather than the decision-maker's. Two tools fix most of it: a translation table for the statistics, and a four-layer structure for the message.

**Translating the statistics.** Never report a number the audience cannot act on without its translation:

| What you have | What not to say | What to say instead |
|---|---|---|
| A coefficient (0.032 on `is_returning`) | "The coefficient on returning users is 0.032, significant at 5%" | "Returning users on the new payment method complete checkout about 3 points less often than comparable new users — roughly 1 in 30 who would have bought didn't" |
| A p-value (p = 0.04) | "p = 0.04" | "If there were really no difference, we'd see a gap this big by chance about 1 time in 25. That's unlikely but not impossible, so I'd call it *likely real*, not *certain*" — and then say what else you checked |
| A confidence interval (1.8pp, 95% CI 0.6–3.0) | "The 95% CI is 0.6 to 3.0" | "Our best estimate is a 1.8-point lift; the plausible range is somewhere between 0.6 and 3 points. Even the low end pays for the engineering time" |
| An effect size | "The effect is statistically significant" | "The effect is about €24k of margin a week. Significance tells you it's probably real; the size tells you whether it matters. Here it's both" |
| A null result | "No significant difference was found" | "We saw no difference we could distinguish from noise. That could mean there's no effect, or an effect too small to detect with this much data — we had enough data to spot anything bigger than about 2 points, so if there's an effect it's smaller than that" |
| R², model fit | "R² was 0.31" | "The things we measured explain about a third of the variation in order value; most of it is driven by things we don't have data on" |
| A correlation | "X is strongly correlated with Y" | "Customers who do X also tend to do Y. We can't tell from this whether X causes Y, or whether some third thing drives both — that would take an experiment" |

The pattern: *the estimate in the audience's units, the uncertainty in plain words, what it means for the decision.* A p-value or an interval is evidence about the first two; it is never the message.

**The four layers.** Separate what you *found* from what you *think it means*, what you *recommend*, and what you *don't know*. Audiences conflate these unless you keep them apart, and conflating them is how an interpretation gets quoted as a fact.

| Layer | What it is | Running example |
|---|---|---|
| **Findings** | What the data shows, stated neutrally, with uncertainty | Checkout completion among returning users on the new payment method is about 3 points below comparable users (plausible range 1.5–4.5). The gap appeared in the week the method launched. |
| **Interpretation** | What you think explains it, and how confident you are | Most likely the new method's authentication step is failing for stored cards. Likely, not certain: we see the timing and the segment, but not the failure itself. |
| **Conclusions** | What follows for the decision | The drop is worth about €24k of margin a week. A fallback to the previous method is cheap to build and testable in two weeks. We recommend testing it. |
| **Limitations** | What this cannot tell you, and what would change the picture | The data is observational, so the cause is inferred, not demonstrated — the test will settle it. Half the headline drop was a tracking break, now fixed; the trend before the fix is not comparable. We have no view of users who abandoned before checkout. |

Lead with the conclusion (answer first), but keep all four visible and labelled, so a reader can see where the evidence ends and the judgment begins. Limitations go last but never get cut: a limitation the audience discovers for themselves costs you more credibility than one you stated.

**Three habits that make this routine:**
- **Units, then uncertainty, then decision.** Every number gets all three or it doesn't go in the memo.
- **Grade every claim.** *Established / likely / possible / cannot tell from this data* — in the text, not just in your head. The vocabulary is borrowed from [analytical reasoning](analytical-reasoning.md); communication is where it becomes visible.
- **Rehearse the one-sentence version** of the finding, the interpretation, and the limitation. If any of them cannot be said in one sentence, it is not ready for a non-technical room.

---

## How it looks in practice

- **Write the first sentence last.** Draft, then ask what the one-sentence answer is, then put it at the top.
- **Title charts with sentences.** "Conversion by platform" is a label. "iOS conversion fell 6 points after the 14 Oct release" is a message.
- **Send the short version.** A three-line Slack message with the finding and a link to the memo gets read; the memo alone gets opened later.
- **Share early and rough.** A Tuesday "it looks like iOS, still confirming" is worth more than a polished Friday deck. Mark confidence clearly so rough does not get quoted as final.
- **Keep the caveat.** The Stage 4 data caveat belongs in the Stage 7 memo. Dropping it is how a careful analyst gets blamed for a confident wrong number.
- **Rehearse the objection.** Before any meeting, write down the three hardest questions and your answers.
- **With AI:** agents draft well and structure badly — they narrate the analysis instead of leading with the answer. Reorder, cut, and make sure every sentence is one you would defend. See [working with AI](working-with-ai.md).

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Structure** | Reports what was done, in order | Answer first; one-page memos | Shapes the narrative the organisation tells itself about a problem |
| **Audience** | One version for everyone | Tailors by altitude; pre-wires | Knows what each executive will ask before they ask it |
| **Charts** | Correct | Clear; one message each; sentence titles | Rarely needs more than one chart |
| **Difficult news** | Delivers it when asked | Leads with it; proposes next step | Delivers it in a way that makes the organisation better at hearing it |
| **Pushback** | Folds or defends | Distinguishes data challenges from decision challenges; engages | Welcomes it; uses it to sharpen the recommendation |

---

## Interview lens

Communication is assessed in presentation rounds, take-home readouts, and silently throughout every other round — how you structure an answer *is* the evidence.

**Presentation / take-home readout.**
*What they want:* answer first, a clear structure, charts with messages, honest caveats, and composure under questioning. The commonest failure is walking through the analysis chronologically. Open with the recommendation and the size; the method is an appendix.

**"Explain a confidence interval / p-value / A/B test to a non-technical executive."**
*What they want:* plain language, an analogy that does not mislead, and what it means for their decision. Not a definition. The [translation table](#explaining-statistical-results-to-non-technical-audiences) above is the answer key.

**"Tell me about a time your analysis was challenged."**
*What they want:* that you distinguished a data challenge from a decision challenge, engaged with the strongest version, and either held your ground with evidence or changed your mind for a reason.

**"How would you present this to the CEO vs. the engineering team?"**
*What they want:* altitude. Money and risk for one; cause and spec for the other.

**In the case interview itself.** Structure your answer out loud before diving in; summarise where you've got to every few minutes; say what you'd conclude and how confident you are. The interviewer is scoring communication the whole time.

### Story bank prompts (STAR)
1. A result you delivered that nobody wanted to hear, and how
2. A time you changed how you presented something for a different audience, and what changed
3. A chart or memo that changed a decision — what made it land
4. A challenge to your analysis that turned out to be right, and what you did

---

## Resources

- Barbara Minto, *The Pyramid Principle* — answer-first structure and SCQA
- Cole Nussbaumer Knaflic, *Storytelling with Data* — the chart craft reference
- Edward Tufte, *The Visual Display of Quantitative Information* — the principles under the craft
- [Lea Pica — Present Beyond Measure](https://leapica.com/) — presenting data to business audiences
- Jean-luc Doumont, *Trees, Maps, and Theorems* — clear communication for technical people
- [Datawrapper's blog on chart choice](https://blog.datawrapper.de/) — practical, example-driven

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
