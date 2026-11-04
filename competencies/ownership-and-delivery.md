# Ownership & delivery

> **Definition.** Treating the outcome as yours, not just the analysis: prioritising among more asks than there is time, time-boxing, managing up, following through until a decision is made and measured, and leaving work that others can find and reuse.

**Why it matters.** The gap between an analyst who is competent and one people rely on is almost entirely this ability. Competence produces correct analyses; ownership produces decisions. It is primary in Stage 8, which most analysts treat as optional, and supporting in every other stage, because every stage has a deadline, a scope, and someone waiting. It is also the ability that reviews and promotions actually reward, under names like "impact" and "reliability".

---

## Where it shows up in the workflow

| Stage | What ownership looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Deciding whether to take the ask at all, and at what size; saying no or not yet | ○ |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Time-boxing the framing; committing to a scope and a date | ● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Getting the definition actually signed off, not just proposed | ○ |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Fixing or reporting data problems rather than working around them silently | ● |
| [5 Analyse](../workflow.md#stage-5--analyse) | Stopping when the question is answered; not polishing past the point of use | ● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Finishing — producing three claims, not a notebook | ○ |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Delivering on the date promised; standing behind the recommendation | ● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Chasing the decision; measuring the outcome; closing the loop; logging it | ●● |

---

## The toolkit

### Prioritising

**Impact × confidence × effort** — *Of everything I could do, what is worth doing first?* Rough scores on each; the ask with high impact, decent confidence, and low effort wins. Useful mostly for making the trade-off explicit to the person whose ask lost. Stage 1.

**"What decision does this feed, and when?"** — *Is there a deadline that matters?* Work that arrives after the decision is worthless; work that arrives rough but on time is not. The question sorts most asks by itself. Stage 1.

**The smaller yes** — *What can I offer instead of no?* A two-hour sanity check instead of a two-week deep dive; a pointer to an existing dashboard; a date next month. Protects the relationship and the backlog. Stage 1.

### Managing the work

**Time-boxing** — *How long is this worth?* Set it before starting, say it out loud, stop when it runs out and report what you have. Analyses expand to fill the time available; a time-box is the only reliable defence. Stage 2 and 5.

**Scope in writing** — *What am I doing and not doing, by when?* Two sentences in a channel. The single highest-return habit in the repo; also appears under [collaboration](collaboration.md), because it is both. Stage 2.

**Definition of done** — *What does finished look like?* A memo sent, a decision scheduled, a metric agreed. Not "analysis complete". Stage 2 and 6.

**Working in the open** — *Can people see where this is?* A thread, a doc, a status line. It replaces the status meeting and makes "how's it going?" unnecessary. All stages.

### Managing up

**Early escalation** — *Is something about to go wrong?* "Heads up, this might slip" on Wednesday beats "it slipped" on Friday. Managers can fix a problem they hear about early; they can only absorb one they hear about late.

**Decisions, not updates** — *What do I need from my manager?* Bring options with a recommendation, not a status report. "I can do A by Thursday or B by Monday; I suggest A because…" gets a decision in one message.

**No surprises** — anything a stakeholder would be upset to learn from someone else, they should learn from you first.

### Following through

**The decision log** — *What did my work change?* One line per analysis: the ask, the recommendation, what was decided, what happened. It is your evidence at review time, your story bank for interviews, and the fastest way to notice which stages you avoid. Stage 8. *Running example:* "Checkout drop — recommended tracking fix + fallback test — both done — 1.8pp recovered — €X/week."

**The two-week follow-up** — *Did anything happen?* A calendar reminder after every delivery: was the recommendation acted on? If not, why not? Most analyses that fail, fail here, silently. Stage 8.

**Measuring the outcome** — *Did it work?* Set up the measurement when you make the recommendation, not after. If the decision cannot be measured, say so at the time. Stage 8.

**The post-mortem for your own work** — *Why didn't this land?* Not every analysis changes a decision; the ones that don't are where the learning is. Stage 8.

### Leaving things better

**Documentation that gets found** — *Will the next person redo this?* A short README with the question, the answer, the caveats, and where the code is. Filed where people look, not where it is convenient to write. All stages.

**Reusable assets** — a checks script, a metric definition in the glossary, a dashboard for a recurring question. The compounding return on an analyst's time. Stage 4, 7, 8.

---

## How it looks in practice

- **Say the time-box out loud.** "I'll give this two days and come back with what I have." It sets expectations and it holds you to them.
- **Keep the decision log from day one.** It takes a minute per analysis and it is the most valuable document you will own.
- **Follow up on everything you deliver,** two weeks later, without being asked.
- **Finish things.** A finished rough memo beats an unfinished excellent one. Perfectionism is a form of not delivering.
- **Decline in writing, with an alternative.** "I can't do this by Friday; I can do a quick check today or the full thing next Wednesday."
- **Report your own slips first.** Credibility is built on the bad news you volunteered.
- **With AI:** agents make the analysis faster and the follow-through no easier. Use the time saved on Stage 8, not on more Stage 5. See [working with AI](working-with-ai.md).

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Prioritising** | Does what is asked, in order received | Trades off explicitly; offers the smaller yes | Decides what the team works on; says no on others' behalf |
| **Delivery** | Delivers when prompted | Time-boxes; delivers on the date; works in the open | Delivery is assumed; attention goes to what gets delivered |
| **Managing up** | Reports status | Escalates early; brings options with a recommendation | Manager hears about problems and solutions in the same message |
| **Follow-through** | Delivers and moves on | Follows up; keeps a decision log; measures outcomes | Accountable for decisions changed, not analyses produced |
| **Leaving things better** | Shares notebooks | Documents so others reuse; builds a checks script | Builds the team's reusable assets and norms |

---

## Interview lens

Ownership is probed through behavioural questions about impact, prioritisation, and failure — and judged silently by whether your stories have outcomes.

**"Tell me about a project and its impact."**
*What they want:* a measurable outcome and your specific contribution — a decision changed, a number moved, a thing shipped. Weak answers describe the method and stop at delivery.

**"What happened after you delivered the analysis?"**
*What they want:* that you know. A surprising number of candidates don't. The decision log makes this trivial.

**"How do you prioritise when everyone's ask is urgent?"**
*What they want:* a rule (decision and deadline; impact × confidence × effort), an example of using it, and how you told the person whose ask lost.

**"Tell me about a time you missed a deadline / a project failed."**
*What they want:* early escalation, honest reporting, what you learned, what changed. Not a story where nothing was your fault.

**"Tell me about a time you said no."**
*What they want:* the smaller yes.

### Story bank prompts (STAR)
1. An analysis whose outcome you can state in numbers, and what you personally did to make it happen
2. A time you escalated early and what it saved
3. A deliberate trade-off between two asks, and how you communicated it
4. A delivery that didn't change anything — and what you did about it afterwards
5. Something you built once that others kept using

---

## Resources

- Cal Newport, *Deep Work* — time-boxing and finishing, from the productivity side
- Julie Zhuo, *The Making of a Manager* — managing up, read from the other side of the table
- Camille Fournier, *The Manager's Path* — what managers need from the people they manage
- Kim Scott, *Radical Candor* — delivering bad news and declining well
- Your own decision log — the most useful document on this list, and the only one you have to write

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
