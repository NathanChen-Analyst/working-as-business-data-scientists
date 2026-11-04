# Analytical reasoning

> **Definition.** Structuring an ambiguous problem into something answerable, forming hypotheses that can be tested, choosing the method that fits the question, knowing what the data can and cannot say, and separating signal from noise. The thinking that happens before, around, and after the technical work.

**Why it matters.** Technical craft executes; analytical reasoning decides what to execute and whether to believe the result. It is the ability most often mistaken for intelligence and most often missing in people with strong technical skills — the analyst who runs the right query on the wrong question, or finds a significant result and does not ask how many other things were tried. It is primary in four stages, and in interviews it is what case questions are designed to probe.

---

## Where it shows up in the workflow

| Stage | What analytical reasoning looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Distinguishing a why-question from a what-should-we-do question from a how-bad-is-it question | ● |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Issue trees; converting questions into falsifiable hypotheses; deciding what evidence would change the decision | ●● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Choosing a measure that is valid for the decision; anticipating how it could mislead | ●● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Predicting what the data should show before looking; recognising when a surprise is a data problem | ● |
| [5 Analyse](../workflow.md#stage-5--analyse) | Matching method to question; causal vs. correlational thinking; experimental design; resisting the forking paths | ●● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Grading confidence; sensitivity to assumptions; choosing the claims that survive scrutiny | ●● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Anticipating the objection and the counter-evidence | ● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Designing the follow-up measurement so it can actually detect whether the decision worked | ○ |

---

## The toolkit

### Structuring the problem

**Issue trees (MECE decomposition)** — *What are all the ways this could be true, without overlap?* Break the question into mutually exclusive, collectively exhaustive branches until each leaf is testable. The single most useful habit in Stage 2. *Running example:* the 8% drop is a measurement artefact *or* a real change; a real change is fewer people entering checkout *or* fewer completing; and so on.

**Hypothesis-driven analysis** — *What do I expect to find, and what would prove me wrong?* State the hypothesis, decide the test, then look. The opposite of "let's explore the data and see". Stage 2 and 5.

**Decision-first framing** — *What are the options, and what evidence would change which one we pick?* If no plausible result would change the decision, the analysis is not worth doing. Stage 1 and 2.

**Fermi estimation** — *Roughly how big is this?* Order-of-magnitude reasoning from a few known quantities. Used to sanity-check results in Stage 4, size findings in Stage 6, and answer interview questions in every stage.

### Reasoning about evidence

**Correlation vs. causation, and the ladder in between** — *Does X cause Y, or do they just move together?* Confounding, reverse causality, selection. The question to ask of every "X drives Y" claim, including your own. Stage 5 and 6. The [causal-inference toolkit](../workflow.md#stage-5--analyse) in Stage 5 is the technical side; this is the habit of asking.

**Bayesian updating (informally)** — *How much should this evidence move my belief?* A prior, a likelihood, a posterior — in words, not numbers. Protects against both over-reacting to one data point and ignoring accumulating evidence. Stage 6.

**Base rates and regression to the mean** — *Would this have happened anyway?* Extreme values tend to be followed by less extreme ones; an intervention applied after a bad month will "work" by itself. Stage 5 and 6.

**Simpson's paradox and mix effects** — *Is the aggregate hiding opposite movements in the parts?* A metric can rise in every segment and fall overall if the mix shifts. Stage 5; it is also a standard interview question.

**The garden of forking paths** — *How many analyses were run before this one was reported?* Multiple comparisons, flexible metric definitions, optional stopping. The reason pre-registration exists. Stage 5.

**Survivorship and selection** — *Who is missing from this data?* Churned users, failed orders, people who never saw the feature. Stage 4 and 5.

### Choosing the method

**The question → method map** — *What kind of question is this, and what answers it?* Descriptive (what happened), diagnostic (why), predictive (what will happen), causal (what would happen if we acted). Each has a family of methods; using a predictive model to answer a causal question is the classic mismatch. The map is in [Stage 5](../workflow.md#stage-5--analyse).

**Proportionality** — *What is the simplest method that answers this well enough for this decision?* A segmentation in an afternoon beats a model in a fortnight. Stage 5.

**Experimental thinking** — *If we could run a test, what would it look like?* Even when you cannot randomise, asking what the ideal experiment would be clarifies what the observational analysis is trying to approximate and what it is missing. Stage 2 and 5.

### Judging the result

**Sensitivity analysis** — *Does the conclusion survive reasonable changes in assumptions?* Change the window, the definition, the exclusion rule. If the answer flips, say so. Stage 6.

**Confidence grading** — *How sure am I, and why?* Established / likely / possible / cannot tell from this data. Every claim gets a grade; every grade gets a reason. Stage 6 and 7.

**The pre-mortem** — *If this recommendation turns out to be wrong, why will it have been?* Run it before sending. Stage 7.

---

## How it looks in practice

- **Write the hypothesis before the query.** One sentence. If you cannot, you are exploring, not analysing — which is sometimes fine, but know which you are doing.
- **Predict the number.** Before every result, write down what you expect. The surprise is the finding, and the habit catches data errors faster than any check.
- **Ask "what would change the decision?"** in every Stage 1 conversation. It kills most unnecessary analyses and sharpens the rest.
- **Keep a count of what you tried.** If you cut the data ten ways to find the one that is significant, the result is worth a tenth of what it looks like.
- **Grade your confidence out loud.** Stakeholders calibrate on you over time; the ones who say "likely" when they mean "likely" get believed when it matters.
- **Argue the other side.** Before any conclusion goes out, spend ten minutes trying to break it. An AI agent is a good sparring partner for this.

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Structuring** | Follows a structure given to them | Builds issue trees unprompted; prunes to what the data can test | Reframes the problem itself; sees the question behind the question |
| **Hypotheses** | Explores, then rationalises | States hypotheses first; designs tests | Knows which hypotheses are worth the organisation's time |
| **Method** | Uses the method they know | Matches method to question; chooses proportionately | Knows the limits of every method and when to say "we cannot know this" |
| **Evidence** | Reports what the data shows | Asks what else could explain it; checks forking paths | Calibrated; their "likely" is reliably likely |
| **Judgment** | Trusts the output | Runs sensitivity checks and pre-mortems | Catches the error nobody else saw, from first principles |

---

## Interview lens

This is what case interviews test. The format varies — product sense, metric investigation, estimation — but the assessment is always the same: can you structure, hypothesise, choose a method, and judge a result, out loud.

**"Conversion dropped 8%. Walk me through how you'd investigate."**
*What they want:* measurement check first, then a clean decomposition, then prioritised hypotheses with the cheap ones first, then a time-box. A fully worked answer is in [Stage 2](../workflow.md#stage-2--frame-the-question).

**"How many [X] are there in [place]?"**
*What they want:* Fermi reasoning with stated assumptions. They do not care about the number.

**"Explain Simpson's paradox with an example."**
*What they want:* a concrete case (admissions, treatment outcomes, conversion by segment) and the sentence "the mix changed".

**"We saw a 2% lift with p = 0.04. Ship it?"**
*What they want:* power, practical vs. statistical significance, how many metrics and segments were examined, whether anyone peeked, what the guardrails did. Detail in [Stage 5](../workflow.md#stage-5--analyse).

**"Users who use feature X retain 30% better. Should we push everyone to use X?"**
*What they want:* the words "selection" or "confounding", then the ideal experiment, then what observational evidence could approximate it.

**"What would you need to believe for this to be true?"**
*What they want:* that you can reason backwards from a claim to its assumptions.

### Story bank prompts (STAR)
1. An ambiguous ask you structured into something answerable
2. A result you were about to report that you caught as a mix effect, selection, or forking path
3. A time you chose the simpler method over the impressive one, and why
4. A conclusion that changed when you ran a sensitivity check

---

## Resources

- Barbara Minto, *The Pyramid Principle* — issue trees and MECE
- Max Shron, *Thinking with Data* — scoping and the question behind the question
- Daniel Kahneman, *Thinking, Fast and Slow* — base rates, regression to the mean, overconfidence
- Richard McElreath, *Statistical Rethinking* — the Bayesian habit of mind, even if you never run the models
- Judea Pearl & Dana Mackenzie, *The Book of Why* — causal thinking for non-specialists
- Andrew Gelman & Eric Loken, ["The garden of forking paths"](http://www.stat.columbia.edu/~gelman/research/unpublished/p_hacking.pdf) — the short paper every analyst should read once

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
