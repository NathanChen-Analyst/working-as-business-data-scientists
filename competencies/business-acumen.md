# Business acumen

> **Definition.** Knowing how the business makes money, what the unit that is asking exists to do, what decision is actually on the table, and what a result is worth in business terms. The ability to turn a business question into an analytical one and the answer back again.

**Why it matters.** Every ask comes from somewhere in the business, and every recommendation lands somewhere in it. An analyst without business acumen answers the question as asked, reports results in percentage points, and is surprised when nobody acts. One with it answers the question that was meant, sizes results in money and customers, and knows whose problem the finding solves. It is primary in six of the eight stages — more than any other ability except collaboration.

---

## Where it shows up in the workflow

| Stage | What business acumen looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Knowing which goal the ask serves and who owns it; asking the right clarifying questions | ●● |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Choosing hypotheses that reflect how the business works, not just how the data is structured | ●● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Picking the metric that maps to the goal; knowing the company's existing definitions and why they exist | ●● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Knowing which system is the source of truth for revenue, customers, orders | ○ |
| [5 Analyse](../workflow.md#stage-5--analyse) | Choosing segments that mean something commercially; noticing a result that cannot be right | ● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Sizing findings in money, customers, and time; choosing the three that matter | ●● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Framing the recommendation in terms of the decision-maker's goal and constraints | ●● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Knowing what "worked" means for the business, not only for the metric | ●● |

---

## The quick read: four sentences before any ask

Frameworks help you analyse a business. They do not help you find your bearings in one. That needs a faster tool: four sentences you can write in ten minutes, on your first day or when an ask arrives from a part of the business you do not know. Write them down. If you cannot, that is the first finding.

### 1. The business in one sentence

Who pays whom, for what, and how the money works.

> *[Company] makes money by selling [what] to [whom] at [price], with [the main cost]. The number the company lives by is [metric].*

This is the business model and the unit economics in one line. If you do not know the main cost or the number the company lives by, ask someone in finance. They will be pleased you asked.

### 2. The unit in one sentence

Which part of the business is asking, what it exists to do, and the one number it is judged on.

> *[Unit] exists to [mission]. This quarter it is measured on [goal metric].*

A "unit" is whoever owns the ask: a product team, a marketing team, a country, a sales region. Most asks come from a unit, not from the company. The unit's goal is usually written down somewhere — an OKR, a team charter, a quarterly plan. Find it.

### 3. How the two connect

Does the unit's metric move the company's metric? Always, sometimes, or not at all?

> *[Unit metric] drives [company metric] because [reason]. It can be moved without moving the company metric when [case].*

This is a metric tree with two levels. Write the second part. That is where conflicts between teams hide: a unit can hit its number in a way that does the company no good, or harm.

### 4. Where the question sits

Place the question you were asked against the goal from sentence 2. There are four places it can sit:

| The question is… | Example | What it means for you |
|---|---|---|
| **the goal itself** | "How do we grow checkout conversion?" | Big, open, and worth a proper framing in Stage 2 |
| **a driver of the goal** | "Why did iOS conversion drop?" | The most common case. Answer it, but keep the goal in view: the real question is what the drop costs and whether it can be recovered |
| **a constraint on the goal** | "Can we do this without hurting margin?" | The unit wants to move its metric; someone else's metric is at risk. Your job is to measure both |
| **disconnected from the goal** | "Which day of the week has the most orders?" | Curiosity, politics, or an unstated goal. Ask what it is for before doing anything |

The question you are asked and the goal it serves are usually not the same thing. Sometimes they are. The point of this sentence is to know which.

### The quick read on the running example

> **1.** The company sells goods through its own online checkout and keeps the margin. It lives on orders × order value × margin.
> **2.** The growth team exists to turn existing traffic into orders. This quarter it is measured on checkout conversion.
> **3.** Conversion drives orders, and orders drive the company number. It can be moved without helping the company if it is moved by discounting, which raises orders and lowers margin.
> **4.** The PM's question — "why is conversion down 8%?" — is a driver question under the unit goal. The goal question behind it is "can we recover those orders before the quarter ends?"

Ten minutes. The analyst now knows the success metric at two levels and what the question is for.

### When a sentence stays blank

- **No sentence 1:** you do not yet understand the business well enough to size anything. Fix this first; it takes an hour with the right person.
- **No sentence 2:** the unit does not have a clear goal, or you have not found it. Either way, the ask is floating. Raise it gently: "What is this feeding into?"
- **No sentence 3:** nobody has checked whether the unit's metric helps the company. That is a finding worth more than the ask.
- **Sentence 4 says "disconnected":** do not start the analysis. Find out what the question is for.

### The same four sentences, from outside

In an interview, "tell me about our business" is asking for sentence 1 and, if you can manage it, sentence 2 for the team you would join. Both can be written from public information: the annual report, the pricing page, the careers page, a few earnings calls. Writing them before the interview is also the fastest way to decide whether you want the job.

---

## The toolkit

The frameworks below are tools for writing the four sentences, and for going deeper once they are written. Each one is listed with the question it answers, the sentence it serves, and the stage where an analyst reaches for it. Eight to twelve of these, well understood, are worth more than fifty names.

### For sentence 1 — how the business makes money

**Business model canvas** — *What are the parts of this business and how do they fit?* Customer segments, value proposition, channels, revenue streams, cost structure. The fastest way to write sentence 1 in a business you do not know. Stage 1.

**Unit economics** — *What does one customer, order, or subscription earn and cost?* Revenue per unit, variable cost, contribution margin, and how they change with scale. The second half of sentence 1, and the basis for sizing any finding in Stage 6. *Running example:* the 4% real drop is worth ~€X a week only once you know average order value, margin, and weekly checkout volume.

**Reading a P&L** — *Where does the money go, and which lines can this decision move?* Revenue, cost of sales, gross margin, operating costs. An analyst who can read the P&L knows which findings the CFO will care about. Stage 1 and 7.

### For sentences 2 and 3 — the unit and its goal

**OKRs and team charters** — *What has this unit said it is trying to do?* The written goal is sentence 2. If the unit has none, that is a finding. Stage 1.

**North-star metric and metric trees** — *What one number best captures the value the company creates, and which levers drive it?* The tree is sentence 3 drawn out: company metric at the top, unit metrics below, drivers below that. Also the fastest way to see which unit metrics can be moved without helping the company. Stage 1 and 3.

**Funnels and AARRR** — *Where do we lose people between first contact and loyal customer?* Acquisition, activation, retention, revenue, referral. The usual shape of a growth unit's metric tree. Stage 2 and 5. *Running example:* the whole case is a funnel question.

### For sentence 4 — placing the question

**Decision-first framing** — *What decision does this question feed, and what evidence would change it?* If no answer would change what anyone does, the question is disconnected. Stage 1 and 2. (The analytical side is in [analytical reasoning](analytical-reasoning.md).)

### For going deeper — the market around the business

**PESTEL** — *What outside forces (political, economic, social, technological, environmental, legal) could explain or threaten this?* Rarely the analysis itself. Often the reason a metric moved that the data cannot show. Stage 2, as the "external causes" branch of the issue tree. *Running example:* a new payment regulation in one country would be a PESTEL hypothesis.

**Porter's five forces** — *How much pricing power and margin can this business expect?* Supplier power, buyer power, substitutes, new entrants, rivalry. Context for pricing and strategy asks, and for understanding why margins differ across product lines. Stage 1 and 7.

**SWOT** — *What are we good and bad at, and what is coming?* Best used as a structured conversation with a stakeholder, not as analysis. It tells you what *they* think matters, which shapes the frame. Stage 1.

### For going deeper — the customers

**Segmentation, targeting, positioning (STP)** — *Which customers are we for, and what do we say to them?* Segmentation is also the analyst's most-used technique in Stage 5; STP is the business logic for which segments matter. *Running example:* "returning users on the new payment method" matters because returning users carry most of the margin.

**Jobs to be done** — *What is the customer trying to get done when they use this?* Reframes metrics around the customer's progress rather than the product's features. Stage 3.

**Lifetime value and acquisition cost (LTV / CAC)** — *Is a customer worth what it costs to get them?* The two numbers behind most growth decisions. Know roughly what they are for your business without looking them up. Stage 6 and 7.

**Retention and cohorts** — *Do customers stay, and is that changing?* Retention compounds; cohort analysis is how you see it. Stage 3 and 5.

### For going deeper — pricing

**Price elasticity and willingness to pay** — *How much does demand change if price changes?* Elasticity from past price variation or from experiments; willingness to pay from survey methods such as Van Westendorp, or from conjoint analysis for feature-price trade-offs. Stage 5. Elasticity from observational data is a causal claim; treat it as one.

**Promotions and their hangover** — *Did the promotion create demand or move it?* Pull-forward, cannibalisation, margin erosion. A common Stage 6 trap: a promotion that worked on revenue and failed on margin.

---

## How it looks in practice

- **Write the four sentences for every new ask.** It takes ten minutes and it is the difference between answering the question and answering the goal.
- **Know the numbers cold.** Revenue, margin, customer count, average order value, LTV, CAC, the top three costs. Roughly, from memory. It is what lets you size a finding in the meeting instead of next week.
- **Read what the business reads.** The board deck, the quarterly review, the strategy doc. They tell you what the organisation thinks matters.
- **Translate both ways.** Business question to analytical question in Stage 2; analytical result to business meaning in Stage 6.
- **Size everything.** Percentage points are not a result. "4 points of conversion on €2m of weekly checkout value at 30% margin is about €24k of margin a week" is a result.
- **Notice what cannot be right.** If the analysis says a tiny segment drives half the revenue, business knowledge should fire before statistics do.
- **Spend time with the people who run things.** Sales, support, operations, finance. An hour a month with each teaches more than any dashboard.

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Knowing the business** | Knows the product; learning how money is made | Can write sentence 1 and 2 for any unit; reads the board deck | Knows the strategy, the constraints, and the politics; is consulted on what to measure |
| **Placing the question** | Answers the question as asked | Places it against the goal; reframes when it is a driver or disconnected | Shapes which questions get asked at all |
| **Sizing** | Reports metrics | Sizes findings in money and customers | Sizes findings against the alternatives the business is weighing |
| **Frameworks** | Knows the names | Knows which question each answers; uses two or three fluently | Knows when none fit and builds the frame from the business itself |
| **Commercial judgment** | Flags surprising results | Catches results that cannot be right before they go out | Anticipates what the CFO, the CPO, and the CEO will each ask |

---

## Interview lens

Business acumen is probed through product-sense and case questions, and through how you handle numbers in conversation.

**"Tell me about our business."**
*What they want:* sentence 1, and sentence 2 for the team you would join, from public information. Most candidates describe the product. Strong candidates describe how the money works.

**"How would you measure the success of [feature]?"**
*What they want:* that you start from what the feature is for — the unit goal — pick a primary metric that maps to it, add guardrails, and say what you would trade off. Weak answers list metrics without a purpose.

**"Our revenue is down 10%. Where would you look?"**
*What they want:* a decomposition that follows how the business makes money — customers × orders per customer × value per order — before any data.

**"Estimate the size of [market / opportunity]."**
*What they want:* a structured estimate with stated assumptions. The reasoning is the answer.

**"Should we run this promotion?"**
*What they want:* demand uplift against margin erosion and pull-forward, and what you would measure to know.

**"What's a metric this company tracks that you think is misleading?"**
*What they want:* evidence that you think about what a metric is *for*. This is the hardest one to fake and the one that most clearly shows sentence 3.

### Story bank prompts (STAR)
1. A time you reframed an ask around the real goal behind it
2. A finding you sized in business terms, and what that changed
3. A result that looked right in the data and wrong against the business, and what you did
4. A time a unit's metric and the company's metric pulled in different directions, and how you handled it

---

## Resources

- Alex Osterwalder, *Business Model Generation* — the canvas; the fastest way to learn a new business
- Karen Berman & Joe Knight, *Financial Intelligence* — reading a P&L without an accounting degree
- Alistair Croll & Benjamin Yoskovitz, *Lean Analytics* — the one metric that matters, and metric trees
- Clayton Christensen et al., *Competing Against Luck* — jobs to be done
- Hermann Simon, *Confessions of the Pricing Man* — pricing from a practitioner
- [Reforge blog](https://www.reforge.com/blog) — growth, retention, and metric-tree thinking in product companies

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources. This file adds the quick read before the toolkit.*
