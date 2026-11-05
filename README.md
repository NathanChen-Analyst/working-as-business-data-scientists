# Working as a Business Data Scientist

**The workflow, the abilities, and what good looks like — from entering the field to teaching it.**

Using data to guide decisions is fundamental to how businesses operate, which puts the business data scientist between the data and the people who have to act on it. Yet despite a vast landscape of books, courses, and repositories dedicated to statistical foundations and technical tools, far less material shows how technical, strategic, and interpersonal abilities actually come together in day-to-day work.

This repository organises those abilities around the workflow itself. By following a project stage by stage — from an initial, ambiguous ask to a measured decision — it makes visible where each ability is drawn on, what the deliverables look like, how AI agents change the division of labour, and how the standard shifts from entering the field to teaching it. One case runs through everything, with the actual artefacts an analyst would produce.

It is written for data analysts, product analysts, and data scientists whose output is a business decision rather than a deployed model. Part I describes the job as a competent practitioner does it; [Part II](#part-ii--you-in-the-job) describes how the expectations shift from entering the field to teaching it, and what makes a career go well; Part III holds the worked example and the map of the repo.

---

**Contents**

- **Part I — The job.** How the work is done.
  - [1 · Day-to-day workflow](#1--day-to-day-workflow-stage-framework) · [2 · Abilities by stage](#2--abilities-by-stage-the-matrix) · [3 · Working with AI agents](#3--working-with-ai-agents) · [4 · Role notes](#4--role-notes)
- **Part II — You in the job.** Where you are, and what makes a career.
  - [5 · Where are you?](#5--where-are-you) · [6 · A successful career](#6--a-successful-career)
- **Part III — The example and the repo.**
  - [7 · The running example](#7--the-running-example) · [8 · How this repo is organised](#8--how-this-repo-is-organised) · [About](#about) · [Contributing](#contributing) · [License](#license)

---

# Part I — The job

*How the work is done: the eight stages, the six abilities they draw on, and how AI agents change the split between them.*

## 1 · Day-to-day workflow (stage framework)

Eight stages in three bands — what you do at each, and what exists when you are done. The full treatment of every stage, with the running example, is on the [workflow page](workflow.md); the matrix below links to each stage.

<p align="center"><img src="assets/framework.svg" alt="The eight-stage workflow in three bands with an action and a result for each stage. Frame: 1 receive the ask, 2 frame the question, 3 define metrics and success. Analyse: 4 get and trust the data, 5 analyse, 6 synthesise into insight. Act: 7 recommend and communicate, 8 drive the decision and measure the outcome. The outcome of stage 8 becomes the next ask." width="860"></p>

Machine learning and experimentation live inside Stage 5 as options, chosen when the question calls for them. The Frame and Act bands are where business judgment and persuasion do most of the work; the Analyse band is where technical skill does. Interviews probe all eight stages; most candidates prepare for the middle three.

The framework stitches together four established ideas — Google's *Ask → Prepare → Process → Analyse → Share → Act* process, Max Shron's CoNVO scoping framework, hypothesis-driven analysis from consulting, and decision-first framing — and deliberately differs from the ML lifecycles (CRISP-DM, TDSP), which assume the deliverable is a deployed model and compress framing and communication into single phases.

## 2 · Abilities by stage (the matrix)

A workflow alone hides whatever happens *across* stages — collaboration most of all, which is everywhere and therefore nowhere. So the eight stages are crossed with six abilities:

| | [Craft](competencies/technical-craft.md) | [Reasoning](competencies/analytical-reasoning.md) | [Business](competencies/business-acumen.md) | [Communication](competencies/communication.md) | [Collaboration](competencies/collaboration.md) | [Ownership](competencies/ownership-and-delivery.md) |
|---|:-:|:-:|:-:|:-:|:-:|:-:|
| **[1 Receive the ask](workflow.md#stage-1--receive-the-ask)** | ○ | ● | ●● | ● | ●● | ○ |
| **[2 Frame the question](workflow.md#stage-2--frame-the-question)** | ○ | ●● | ●● | ● | ● | ● |
| **[3 Define metrics & success](workflow.md#stage-3--define-metrics-and-success)** | ● | ●● | ●● | ● | ●● | ○ |
| **[4 Get & trust the data](workflow.md#stage-4--get-and-trust-the-data)** | ●● | ● | ○ | ○ | ●● | ● |
| **[5 Analyse](workflow.md#stage-5--analyse)** | ●● | ●● | ● | ○ | ● | ● |
| **[6 Synthesise into insight](workflow.md#stage-6--synthesise-into-insight)** | ● | ●● | ●● | ● | ○ | ○ |
| **[7 Recommend & communicate](workflow.md#stage-7--recommend-and-communicate)** | ○ | ● | ●● | ●● | ●● | ● |
| **[8 Drive the decision & measure](workflow.md#stage-8--drive-the-decision-and-measure-the-outcome)** | ○ | ○ | ●● | ● | ●● | ●● |

●● primary · ● supporting · ○ minor

*Craft* = technical craft · *Reasoning* = analytical reasoning · *Business* = business acumen · *Collaboration* = collaboration & influence · *Ownership* = ownership & delivery. Each header links to the ability's page; each row to the stage.

**Two things the matrix makes visible.** Technical craft is primary in only two of eight stages. Collaboration & influence is primary in five. Most candidates prepare in inverse proportion.

**How to read it.** Down a column: where an ability is exercised, and so where to practise it. Across a row: what a stage demands, and so what an interviewer probing that stage is really assessing.

Each column header links to that ability's file in [`competencies/`](competencies/): a definition, the concepts and frameworks it draws on, where it shows up in the workflow, what good looks like at junior, mid, and senior level, and the questions that probe it. Each row links to that stage on the workflow page.

## 3 · Working with AI agents

Agents now draft the SQL, run the first pass of the analysis, and write the first version of the memo. That shifts the job rather than shrinking it: the stages where agents are weakest — framing the ask, agreeing metrics, persuading a room, driving a decision — were already most of the value, and the stages where they are strongest are the ones where an unverified output does the most damage.

Every stage on the [workflow page](workflow.md) has a short **With AI** section on what to delegate there and what goes wrong. [`competencies/working-with-ai.md`](competencies/working-with-ai.md) has the full treatment: how to specify a task, how to verify what comes back, how to evaluate whether an agent is reliable enough for a kind of work, and how all of this is now assessed in interviews.

## 4 · Role notes

One workflow, but the weight shifts by role:

| Role | Where the weight sits |
|---|---|
| **Data analyst / BI analyst** | Stages 1–4, 6–7. Stage 5 is mostly descriptive and diagnostic. |
| **Product analyst** | All stages, with Stage 3 (metrics) and Stage 5 (experimentation) emphasised. |
| **Data scientist (analytics / inference)** | Stage 5 deepens into causal inference and modelling; Stage 8 may include owning models in production. |
| **Data scientist (ML)** | A different workflow fits better (CRISP-DM / TDSP); this repo is useful for the parts of that job that touch business decisions. |

---

# Part II — You in the job

*Where you are in your working life, and what makes a career go well beyond being good at the work.*

## 5 · Where are you?

Everything in Part I describes the job at a **competent, mid-level** standard: take an ambiguous ask through all eight stages, drawing on all six abilities. That is the baseline the whole repo is written to.

What changes with experience is not *which* stages and abilities apply, but how much of each you own and how far your judgment is trusted. Pick your phase; each page is a reading path for it.

| Phase | You are… | What to focus on |
|---|---|---|
| **[Becoming](phases/becoming.md)** | Entering the field, or switching into it | Read the workflow once. Then Stages 2, 4 and 7. Build one end-to-end case. |
| **[Working](phases/working.md)** | In the job, first three years or so | You have the technical half. The gap is Stages 1, 3 and 8, and [collaboration](competencies/collaboration.md). |
| **[Advancing](phases/advancing.md)** | Moving from doing the work to shaping it | Craft becomes something you review; judgment and influence become the job. Read the senior column of every ability table. |
| **[Reproducing](phases/reproducing.md)** | Hiring, onboarding, mentoring, building a team | The standard is now something you pass on. How to use this repo to onboard, review and hire. |


## 6 · A successful career

Part I describes the job; Section 5 describes how much of it you own at each point in your working life. Neither says how you get the chance to do it. Being good at the job is necessary, but it does not by itself get you the role, the project, or the room: the people who decide have to know you exist, and then they have to choose you. Only after that does the work of Part I begin — and what that work produces is what gets you known one level up. A successful career is that loop, run again and again: you and the company succeeding together.

| Step | What it means | How it happens | Page |
|---|---|---|---|
| **1. Be known** | The people who decide know you exist and roughly what you can do. Ends when you have the conversation — an interview, or the informal version of one. | Two doors. The open door: an application done well — targeted, evidenced, with a work sample and a referral. The network: work they have seen, a reputation that reaches them, an introduction, being useful before asking. The balance shifts toward the network as roles get more senior. | [Being known](career/being-known.md) |
| **2. Be picked** | Chosen for the role, the project, the room. Ends when the decision is made. | Being judged on three things: the six abilities of [Part I](#2--abilities-by-stage-the-matrix); a track record of outcomes, which is what step 3 produced last time round; and the traits people select for beyond the work itself — follow-through, ambition, courage, composure, generosity with a spine, structured curiosity, self-awareness. The interview is this step made formal; for internal moves it is often a decision by people who have watched you work. | [Career traits](career/career-traits.md) |
| **3. Make a difference** | Doing the job of Part I in a way that helps the business succeed: decisions changed, money and customers moved. Does not end — the outcomes become the track record, and the people who saw them are the start of the next step 1. | Finding the work rather than waiting for it, which is what happens before Stage 1; doing it the way a trusted person does; delivering outcomes, not analyses. | [Finding the ask](career/finding-the-ask.md) · [Dispositions](career/dispositions.md) |

**The interview** is where Part I and step 2 meet. Step 1 is what got you into the room; inside it, the job is to show the three things step 2 is judged on. The common mistake is to treat the interview as the end of applying rather than the beginning of being chosen — applying is telling, the interview is showing. That is why every stage and every ability page in Part I carries an *Interview lens*: the questions asked, what interviewers want, worked answers. The [interview guide](interview/) holds what cuts across them, including the story bank.

**What the rounds accumulate into** — trust with the people who matter, work others can see, what you have taught — is [career capital](career/career-capital.md). What it looks like at each phase of Section 5 is on the [phase pages](phases/).

> **The one thing to remember:** being good at the job gets you taken seriously; it does not get you chosen. Being known gets you considered, being picked gets you the chance, and the difference you then make is what gets you known one level up.

*Where this comes from.* The sequence is old advice under several names; Coleman's *performance, image, exposure* is the best known. Step 1 rests on the social-capital research (weak ties, brokerage, reciprocity); step 2 on personnel-selection research — what predicts performance and what good hiring weighs — and on the Big Five plus self-awareness, which is where the seven traits are drawn from; step 3 is Part I. Each page says which sources it uses.

---

# Part III — The example and the repo

*One case carried through everything, and how the files fit together.*

## 7 · The running example

*"Checkout conversion dropped 8% last month. Can you look into it?"*

One realistic case carried through all eight stages. Half the drop turns out to be a tracking break; the real drop is a payment-method failure for returning users; the fix is tested with an A/B test and shipped. The [`running-example/`](running-example/) folder holds the actual artefacts — the clarifying questions, the issue tree, the data-quality SQL, the segmentation notebook, the experiment design, the one-page memo — so the work is demonstrated rather than described.

## 8 · How this repo is organised

Three structures, one spine:

- **Stages** are the spine. Content lives here, on one page ([workflow.md](workflow.md)). Each stage has the same sections in the same order — what this stage is (with the running example) · hard skills · judgment & business skills · with AI · interview lens · resources.
- **Abilities** are the lens. Each competency file defines one ability and indexes back into the stages. They hold the level tables and the behavioural interview material.
- **Phases** are the doors. Each is a reading path through the above for a point in your career, plus the few things specific to that phase.
- **Career** is what sits around all of it — the three steps are in [§6](#6--a-successful-career); the pages behind them are in `career/`.

```
.
├── README.md                 ← you are here
├── phases/                   ← Becoming · Working · Advancing · Reproducing
├── workflow.md               ← the eight stages, fully worked, on one page
├── competencies/             ← the six abilities + working with AI
├── career/                   ← the pages behind §6: being known · traits · dispositions · finding the ask · career capital
├── running-example/          ← the checkout-conversion case, with artefacts
├── interview/                ← cross-cutting interview material
└── resources.md              ← curated reading, by stage
```

---

## About

Written by [Nathan Chen](https://github.com/NathanChen-Analyst), a business data scientist, as the map I wanted when I started and the one I now use to explain the job to others. The framework is a synthesis of established ideas; the matrix, the phase paths, the AI treatment, and the worked example are my own. If the material is useful, the best thing you can do is tell me what is missing.

## Contributing

Contributions are welcome, especially worked interview answers (question, strong answer, common weak answers), anonymised real-world examples at any stage, and adaptations that teams have made for onboarding. Please open an issue before a large pull request, and keep the section structure of the workflow page for new stage content.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) for the text. Code samples are MIT.

---

*Related: [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference) · [awesome-datascience](https://github.com/academic/awesome-datascience) · [awesome-data-analysis](https://github.com/PavelGrigoryevDS/awesome-data-analysis) · [roadmap.sh/data-analyst](https://roadmap.sh/data-analyst)*
