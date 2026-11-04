# Business acumen

> **Definition.** Understanding how the business makes money, what decision is actually on the table, what a result is worth in business terms, and which of fifteen findings matter. The ability to see an analytical question as a business question and back again.

**Why it matters.** Every ask comes from somewhere in the business, and every recommendation lands somewhere in it. An analyst without business acumen answers the question as asked, sizes results in percentage points, and is surprised when nobody acts. One with it answers the question that was meant, sizes results in money and customers, and knows which stakeholder's problem the finding solves. It is primary in six of the eight stages — more than any other ability except collaboration.

---

## Where it shows up in the workflow

| Stage | What business acumen looks like there | Weight |
|---|---|:-:|
| [1 Receive the ask](../workflow.md#stage-1--receive-the-ask) | Recognising which decision the ask serves and who owns it; knowing the business well enough to ask the right clarifying questions | ●● |
| [2 Frame the question](../workflow.md#stage-2--frame-the-question) | Choosing hypotheses that reflect how the business actually works, not just how the data is structured | ●● |
| [3 Define metrics & success](../workflow.md#stage-3--define-metrics-and-success) | Picking the metric that maps to the decision; knowing the company's existing definitions and why they exist | ●● |
| [4 Get & trust the data](../workflow.md#stage-4--get-and-trust-the-data) | Knowing which system is the source of truth for revenue, customers, orders | ○ |
| [5 Analyse](../workflow.md#stage-5--analyse) | Choosing segments that mean something commercially; spotting a result that is implausible given how the business works | ● |
| [6 Synthesise into insight](../workflow.md#stage-6--synthesise-into-insight) | Sizing findings in money, customers, and time; deciding which three matter | ●● |
| [7 Recommend & communicate](../workflow.md#stage-7--recommend-and-communicate) | Framing the recommendation in the language of the decision-maker's goals and constraints | ●● |
| [8 Drive the decision](../workflow.md#stage-8--drive-the-decision-and-measure-the-outcome) | Knowing what "worked" means for the business, not just for the metric | ●● |

---

## The toolkit

Frameworks are ways of organising a question, not answers. Each one below is listed with the question it answers and the stage where an analyst actually reaches for it. Eight to twelve of these, well understood, are worth more than fifty names.

### How does this business make money?

**Business model and unit economics** — *What does one customer, order, or subscription earn and cost?* Revenue per unit, variable cost, contribution margin, and how they change with scale. Used in Stage 1 to understand what the ask is worth, and in Stage 6 to size any finding. *Running example:* the 4% real drop in checkout completion is worth ~€X/week only once you know average order value, margin, and weekly checkout volume.

**Reading a P&L** — *Where does the money go, and which lines can this decision move?* Revenue, cost of sales, gross margin, operating costs. An analyst who can read the P&L knows which findings the CFO will care about. Stage 1 and Stage 7.

**Business model canvas** — *What are the parts of this business and how do they fit?* Customer segments, value proposition, channels, revenue streams, cost structure. Mostly useful in the first weeks at a new company, or when the ask comes from a part of the business you don't know. Stage 1.

### What is happening around it?

**PESTEL** — *What external forces (political, economic, social, technological, environmental, legal) could explain or threaten this?* Rarely the analysis itself; often the reason a metric moved that the data cannot show. Stage 2 — the "external causes" branch of the issue tree. *Running example:* a new payment regulation in one country would be a PESTEL hypothesis for a conversion drop.

**Porter's five forces** — *How much pricing power and margin can this business expect?* Supplier power, buyer power, substitutes, new entrants, rivalry. Useful context for pricing and strategy asks; rarely something an analyst computes. Stage 1 and Stage 7.

**SWOT** — *What are we good and bad at, and what is coming?* Best treated as a structured conversation with a stakeholder rather than an analysis: it tells you what *they* think matters, which shapes the frame. Stage 1.

### Who are the customers and why do they buy?

**Segmentation, targeting, positioning (STP)** — *Which customers are we for, and what do we say to them?* Segmentation is also the analyst's most-used technique in Stage 5; STP is the business logic that says which segments matter. *Running example:* "returning users on the new payment method" is a segment that matters because returning users carry most of the margin.

**Jobs to be done** — *What is the customer trying to accomplish when they use this?* Reframes metrics around progress the customer makes rather than features used. Stage 3, when choosing what to measure.

**Customer lifetime value and acquisition cost (LTV / CAC)** — *Is a customer worth what it costs to get them?* The two numbers behind most growth decisions; an analyst should know roughly what they are for their business without looking them up. Stage 6 for sizing, Stage 7 for recommending.

### How does it grow?

**Funnels and AARRR** — *Where do we lose people between first contact and loyal customer?* Acquisition, activation, retention, revenue, referral. The default structure for product and growth questions. Stage 2 (framing), Stage 5 (analysis). *Running example:* the whole case is a funnel question.

**Retention and cohorts** — *Do customers stay, and is that changing?* Retention is the metric that compounds; cohort analysis is how you see it. Stage 3 and Stage 5.

**North-star metric and metric trees** — *What one number best captures the value we create, and what drives it?* A metric tree links the north star to the levers teams can pull. Stage 3; also the fastest way to understand a new business.

### What should it charge?

**Price elasticity and willingness to pay** — *How much does demand change if price changes?* Elasticity from historical variation or experiments; willingness-to-pay from survey methods such as Van Westendorp, or from conjoint analysis for feature-price trade-offs. Stage 5, when the question is a pricing question. Elasticity estimated from observational data is a causal claim — treat it as one.

**Discounts, promotions, and their hangover** — *Did the promotion create demand or move it?* Pull-forward, cannibalisation, margin erosion. A common Stage 6 trap: a promotion that "worked" on revenue and failed on margin.

### What is it trying to achieve?

**Strategy, OKRs, and tracing the ask** — *Which objective does this ask serve, and what would success look like for that objective?* Every ask should trace to something the organisation has said it wants. If it doesn't, that is worth saying out loud. Stage 1 and Stage 8.

---

## How it looks in practice

- **Know the numbers cold.** Revenue, margin, customer count, average order value, LTV, CAC, the top three costs. Not precisely — roughly, from memory. It is the difference between sizing a finding in the meeting and sizing it next week.
- **Read what the business reads.** The board deck, the quarterly review, the strategy doc. They tell you what the organisation thinks matters, which is the frame every ask arrives in.
- **Translate both ways.** From business question to analytical question in Stage 2; from analytical result to business implication in Stage 6. If you can only do one direction, you are half an analyst.
- **Size everything.** Percentage points are not a result. "4 points of conversion on €2m of weekly checkout value at 30% margin is roughly €24k of margin a week" is a result.
- **Notice implausibility.** If the analysis says a tiny segment drives half the revenue, the business knowledge should fire before the statistics do.
- **Spend time with the people who run things.** Sales, support, operations, finance. An hour a month with each teaches more about the business than any dashboard.

---

## What "good" looks like by level

| | Junior | Mid | Senior |
|---|---|---|---|
| **Knowing the business** | Knows the product; learning the model | Knows the key numbers and how money is made; reads the board deck | Knows the strategy, the constraints, and the politics; is consulted on what to measure |
| **Framing** | Analyses the question as asked | Reframes around the decision; traces asks to objectives | Shapes which questions get asked at all |
| **Sizing** | Reports metrics | Sizes findings in money and customers | Sizes findings against the alternatives the business is weighing |
| **Frameworks** | Knows the names | Knows which question each one answers and uses two or three fluently | Knows when none of them fit and builds the frame from the business itself |
| **Commercial judgment** | Flags surprising results | Catches implausible results before they go out | Anticipates what the CFO, the CPO, and the CEO will each ask |

---

## Interview lens

Business acumen is probed through product-sense and case questions, and through how you handle numbers in a conversation.

**"How would you measure the success of [feature]?"**
*What they want:* that you start from what the feature is for in business terms, pick a primary metric that maps to it, add guardrails, and know what you would trade off. Weak answers list metrics without a purpose.

**"Our revenue is down 10%. Where would you look?"**
*What they want:* a decomposition that follows how the business makes money — volume × price × mix, by segment, by channel — before any data. Revenue = customers × orders per customer × value per order is the usual first cut.

**"Estimate the size of [market / opportunity]."**
*What they want:* a structured estimate with stated assumptions, not a number. The reasoning is the answer.

**"Should we run this promotion?"**
*What they want:* demand uplift vs. margin erosion vs. pull-forward, and what you would measure to know.

**"What's a metric this company tracks that you think is misleading?"**
*What they want:* evidence that you think about what a metric is *for*. This is the hardest one to fake.

### Story bank prompts (STAR)
1. A time you reframed an ask around the real business decision
2. A finding you sized in business terms and what that changed
3. A result that looked right in the data and wrong against the business, and what you did
4. A time you learned a part of the business from the people running it, and what it changed in your analysis

---

## Resources

- Alex Osterwalder, *Business Model Generation* — the canvas, and a fast way to learn a new business
- Karen Berman & Joe Knight, *Financial Intelligence* — reading a P&L and balance sheet without an accounting degree
- Alistair Croll & Benjamin Yoskovitz, *Lean Analytics* — the one-metric-that-matters and metric trees
- Clayton Christensen et al., *Competing Against Luck* — jobs to be done
- Hermann Simon, *Confessions of the Pricing Man* — pricing from a practitioner
- [Reforge blog](https://www.reforge.com/blog) — growth, retention, and metric-tree thinking as practised in product companies

---

*Follows the shared structure for ability files: definition and why it matters · where it shows up in the workflow · the toolkit · how it looks in practice · what good looks like by level · interview lens · resources.*
