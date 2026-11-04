# Stage 2 — Frame the question

> Part of the eight-stage workflow in the [README](../README.md#the-framework). Previous: [Stage 1](01-receive-the-ask.md) · Next: [Stage 3](03-define-metrics.md)

**Primary abilities:** Analytical reasoning · Business acumen

## What this stage is
Turn the ask into a precise, answerable question with explicit hypotheses, scope, and a definition of done. This is the stage most analysts skip, and the one that most often sinks a project.

A good frame answers four things (CoNVO):

| | Question | Running example |
|---|---|---|
| **Context** | Who is asking and what is the organisational situation? | Growth team; Q4 targets at risk; leadership review in 10 days |
| **Need** | What does the stakeholder need to *know* in order to act? | Whether the drop is real, what is driving it, and whether it is fixable before quarter end |
| **Vision** | What will the output look like? | A one-page memo with a ranked list of causes and a recommended action |
| **Outcome** | What changes once they have it? | A go/no-go on diverting engineering time to checkout this sprint |

## Hard skills
- **Hypothesis structuring.** Build an issue tree: the 8% drop is either a *measurement artefact* or a *real change*; a real change is either *fewer people entering checkout* or *fewer completing it*; completion drops split by *platform*, *payment method*, *new vs. returning*, *geography*, and *time of day*; and so on until each leaf is directly testable.
- **Scoping with data.** Know, before committing, whether the event tracking can actually distinguish the branches of your tree.
- **Prioritising hypotheses.** Rank by (a) prior likelihood and (b) cost to test. Check the cheap, likely ones first — "did a deploy happen on the day the drop started?" takes five minutes.

## Judgment & business skills
- **Separating the question from the answer the stakeholder already has.** PMs often arrive with a theory. Treat it as one hypothesis, not the frame.
- **Agreeing scope in writing.** Two sentences in a channel — "I'm going to check X, Y, Z by Thursday; I am *not* going to look at W" — prevents the most common failure mode, which is discovering on Friday that W was the point.
- **Deciding what would change the decision.** If the answer to "is it fixable before quarter end?" is no either way, the deep dive on causes can wait.
- **Knowing when to stop framing.** Thirty minutes to an hour for most asks. Perfection here is procrastination.

## With AI
Agents are good at generating issue trees and hypothesis lists, and they generate *too many*. The value you add is pruning: which branches the data can actually test, which are cheap to check first, which would change the decision. Ask the agent for the tree, then cut it in half yourself and write down why.

## Interview lens

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

## Resources
- Max Shron, *Thinking with Data* (O'Reilly, 2014) — CoNVO, short and essential
- Barbara Minto, *The Pyramid Principle* — the origin of issue trees and answer-first structure
- [Emma Ding — Cracking Product Sense / Metric / Business Case problems](https://www.youtube.com/@emma_ding) — the interview-side version of this stage
