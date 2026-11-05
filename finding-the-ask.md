# Finding the ask

*What happens before Stage 1 and after Stage 8: noticing where value is being left on the table, sizing it, deciding whether it is worth pursuing, and bringing it to the people who can act — before anyone asks. Also its mirror image: judging the initiatives other people propose.*

**On this page:** [Why it matters](#why-it-matters) · [Where it sits in the workflow](#where-it-sits-in-the-workflow) · [The toolkit](#the-toolkit) · [In practice](#in-practice) · [By level](#what-good-looks-like-by-level) · [Interview lens](#interview-lens) · [Resources](#resources)

---

## Why it matters

*What this ability changes about how you work.*

The workflow begins with "Receive the ask", which quietly assumes someone else finds the problem. Good analysts generate a meaningful share of their own asks — from a metric that drifted, a funnel step nobody owns, a complaint pattern in support tickets, a competitor's move. They also do the mirror image: they look at initiatives other people propose and say, with numbers, whether the thing is worth building.

Job postings describe this as "identify strategic opportunities", "review new business initiatives and confirm their impact", "proactive", "results-oriented". It is the difference between an analyst who is useful and one who is indispensable, and it is the thing most often missing in people who are strong at everything else — because everything else can be done on request.

> **The one thing to remember:** the best analysis you do this year may be one nobody asked for. The second best may be the one that stopped something from being built.

---

## Where it sits in the workflow

*At the two ends of the loop — where asks come from and where outcomes lead. It is not a seventh ability; it is the thing that starts the workflow, and it draws on all six.*

| Stage | What it looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](workflow.md#stage-1--receive-the-ask) | Finding the ask yourself; bringing a sized opportunity rather than waiting for a request | ●● |
| [2 Frame the question](workflow.md#stage-2--frame-the-question) | Framing around the opportunity's value, not only its cause | ● |
| [3 Define metrics & success](workflow.md#stage-3--define-metrics-and-success) | Choosing a metric that would show the opportunity was captured | ● |
| [4 Get & trust the data](workflow.md#stage-4--get-and-trust-the-data) | Noticing, while in the data for something else, the thing nobody is looking at | ○ |
| [5 Analyse](workflow.md#stage-5--analyse) | — | ○ |
| [6 Synthesise into insight](workflow.md#stage-6--synthesise-into-insight) | Spotting the finding that is bigger than the question | ● |
| [7 Recommend & communicate](workflow.md#stage-7--recommend-and-communicate) | Recommending what to do next, not only what was found | ○ |
| [8 Drive the decision](workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | The outcome of one project is the source of the next; keeping the list of what you noticed | ●● |

---

## The toolkit

*Ways of finding, sizing, and testing opportunities. The first table is for finding your own; the second for judging other people's.*

**Finding opportunities**

| Tool | The question it answers | When you use it |
|---|---|---|
| The leak scan | Where is the funnel losing the most, and who owns that step? | Quarterly. Walk every funnel; find the step with the biggest absolute drop and no owner. That is usually an opportunity. |
| Unowned metrics | Which numbers moved and nobody noticed? | Weekly, on the dashboards nobody opens. A metric drifting for a month without a Slack thread is a free finding. |
| Segment outliers | Which group behaves very differently from the rest, and why? | While doing any segmentation. A segment that converts at half or twice the rate is either a bug or a product. |
| Friction in the qualitative data | What are users complaining about, in their own words? | Support tickets, reviews, sales call notes. An LLM can classify thousands in an hour; the pattern is often invisible in the metrics until you know to look. |
| The "if we did nothing" baseline | What does the trend say will happen if nobody acts? | Forecasting the status quo. The gap between that and the goal is the size of the opportunity space. |
| Competitor and market moves | What just changed outside, and what does it do to our numbers? | When a competitor changes pricing, a platform changes rules, or a regulation lands. Business acumen's PESTEL, applied forward. |

**Sizing and judging — yours and other people's**

| Tool | The question it answers | When you use it |
|---|---|---|
| Opportunity sizing | Roughly how much is this worth, in the business's units? | Before pitching anything. *Reach* (how many users or orders are affected) × *impact per unit* (how much each would change) × *confidence* (how sure you are), expressed in money or customers per period. A number, with assumptions stated. |
| RICE / ICE scoring | How does this compare with the other things we could do? | When there are several candidates. Reach × Impact × Confidence ÷ Effort. The score is less useful than the argument about each factor. |
| Cost of delay | What does it cost per week not to do this? | Turning "nice to have" into a number. If the fallback test in the running example recovers €24k a week, every week of delay costs €24k. |
| Cheapest test first | What is the smallest thing we could do to learn whether this is real? | Before any build. A painted-door test, a manual version, a one-country pilot, a two-week A/B test. |
| The pre-mortem | If this initiative fails, why will it have failed? | Reviewing someone's proposal. Write the failure story first; it surfaces the assumption nobody has checked. |
| Reversibility | If we are wrong, how hard is it to undo? | Deciding how much evidence to demand. Reversible decisions deserve speed; irreversible ones deserve the full analysis. |
| Kill criteria | What result would make us stop? | Before starting anything you proposed. Deciding in advance is the only reliable protection against falling in love with your own idea. |

> **The one thing to remember:** an opportunity is a number with assumptions attached. Until you have sized it, it is an opinion.

---

## In practice

*The habits that make this routine.*

- **Keep an opportunity log** alongside the decision log: things you noticed, roughly sized, not yet pursued. Review it monthly. Most entries die; one or two a year become your best work.
- **Bring one unasked finding to every stakeholder meeting.** Small is fine. It changes how people see you from "answers questions" to "finds things".
- **Size before you pitch.** A pitch with a number and stated assumptions gets a decision; one without gets a polite nod.
- **Propose the test, not the build.** Opportunity sense is not advocacy. Your job is to say what it might be worth and how to find out cheaply.
- **Review proposals as if they were yours.** Pre-mortem, sizing, kill criteria. Being the person who makes other people's initiatives better is as valuable as having your own.
- **Kill your own ideas in public.** When the sizing says no, say so, out loud. It is what makes people believe you when the sizing says yes.
- **With AI:** agents are good at the leak scan and the qualitative classification — they can walk every funnel and read every ticket. They are bad at knowing which finding matters to this business now. See [working with AI](competencies/working-with-ai.md).

---

## What "good" looks like by level

*The same habit, at three depths.*

| | Junior | Mid | Senior |
|---|---|---|---|
| **Finding** | Notices things and mentions them | Runs the leak scan and the unowned-metrics check as routine; keeps an opportunity log | Sees the opportunity space of the whole domain; knows which gaps the company is structurally blind to |
| **Sizing** | Describes the opportunity | Sizes it in business units with assumptions | Sizes it against the alternatives, including doing nothing |
| **Judging others' initiatives** | Analyses what is asked | Pre-mortems and sizes proposals; proposes the cheap test | Is in the room when initiatives are chosen; has stopped things from being built |
| **Discipline** | Advocates for own ideas | Sets kill criteria; drops ideas the data does not support | Known for being right about what *not* to do |
| **Outcomes** | — | One self-originated project a year that landed | A track record of self-originated projects, and a team that does the same |

---

## Interview lens

*How this is tested, and what interviewers are listening for.*

| Question | What they want to hear |
|---|---|
| "Tell me about an analysis you did that nobody asked for." | That one exists. What you noticed, how you sized it, who you took it to, what happened. The best answers have a measurable outcome. |
| "A PM wants to build [feature]. How do you evaluate it?" | Sizing (reach × impact × confidence), the cheapest test, a pre-mortem, kill criteria, reversibility. Not a yes or no. |
| "Where would you look for growth in our product?" | The leak scan on their funnel, from what you can see publicly; a hypothesis about an unowned step; how you would size it. |
| "Tell me about a time you were wrong about an opportunity." | That you set kill criteria, hit them, and stopped. The absence of such a story is itself a signal. |
| "How do you decide what to work on when nobody is telling you?" | The opportunity log, sizing, cost of delay, and how you get stakeholder buy-in for self-originated work. |

**Story bank prompts (STAR)**

1. A finding you brought to the business unasked, and its outcome
2. An initiative you evaluated and recommended against — and what happened
3. An idea of your own you killed on the evidence
4. The cheapest test you designed to check whether an opportunity was real

---

## Resources

*A short list. Read one.*

- Marty Cagan, *Inspired* — how product teams find and validate opportunities; read it to understand the people you are pitching to
- Teresa Torres, *Continuous Discovery Habits* — opportunity solution trees; the product-side version of this ability
- Annie Duke, *Quit* — kill criteria and knowing when to stop
- [Intercom's RICE article](https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/) — the original description of the scoring method

---

This page draws on all six abilities: the leak scan is [technical craft](competencies/technical-craft.md); sizing is [business acumen](competencies/business-acumen.md); the pre-mortem is [analytical reasoning](competencies/analytical-reasoning.md); taking it to the right person is [collaboration](competencies/collaboration.md); the opportunity log is [ownership](competencies/ownership-and-delivery.md). The disposition behind it is [curiosity that goes one step further](dispositions.md#the-seven).
