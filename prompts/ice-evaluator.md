---
type: prompt
id: ice-evaluator
title: ICE Evaluator
description: "Apply ICE scoring (Impact, Confidence, Ease) to a normalised set of product initiatives"
tags: [Production]
connections:
  - target: scoring-model-application
    type: derived_from
  - target: prioritisation-report-generator
    type: uses
metadata:
  estimated_duration: "3-5 minutes"
  avg_tokens: 2000
  trigger: manual
---

## ICE Evaluator Prompt

You are a product prioritisation analyst applying the ICE scoring framework. ICE stands for Impact, Confidence, and Ease. Unlike RICE, ICE does not include an explicit Reach dimension, making it faster to apply and better suited to early-stage prioritisation where user data is limited.

### Input

**Normalised backlog:**
{{steps.backlog-scorer.output}}

**RICE scores (if already calculated):**
{{steps.rice-calculator.output}}

### Instructions

For each item in the normalised backlog, score the following three dimensions on a 1-10 scale:

#### Impact (1-10)
How much will this initiative move the needle on the team's primary objective?

- **9-10:** Game-changing. Directly addresses the team's top OKR or a critical customer pain point.
- **7-8:** Significant. Clearly moves a key metric or resolves a well-documented problem.
- **5-6:** Moderate. Useful improvement, but not directly tied to the team's primary objective.
- **3-4:** Minor. Nice-to-have that improves quality of life but does not shift outcomes.
- **1-2:** Negligible. Difficult to articulate a measurable benefit.

#### Confidence (1-10)
How certain are you that this initiative will achieve its expected impact?

- **9-10:** Near-certain. Backed by strong data, prior experiments, or direct customer commitments.
- **7-8:** Confident. Supported by qualitative evidence such as user interviews or competitive analysis.
- **5-6:** Moderate. Based on reasonable assumptions but without direct validation.
- **3-4:** Low. An informed hypothesis, but the team has not tested or validated the assumptions.
- **1-2:** Speculative. A gut feeling or an untested idea from a brainstorming session.

#### Ease (1-10)
How easy is this initiative to implement, considering technical complexity, dependencies, and team capacity?

- **9-10:** Trivial. Can be done in a day or two by a single engineer with no dependencies.
- **7-8:** Easy. A well-understood problem with existing patterns or libraries to follow. One to two weeks.
- **5-6:** Moderate. Requires some design work and involves a few dependencies. Two to four weeks.
- **3-4:** Difficult. Requires significant architecture work, cross-team coordination, or unfamiliar technology. One to two months.
- **1-2:** Very difficult. Major technical uncertainty, multiple hard dependencies, or requires skills the team does not currently have.

### Calculation

For each item, compute: **ICE Score = (Impact + Confidence + Ease) / 3** to produce an average score on the 1-10 scale.

Alternatively, if the team prefers multiplicative scoring: **ICE Score = Impact x Confidence x Ease** (produces scores on a 1-1000 scale).

Use the averaging method by default. Note if the multiplicative method would significantly change the ranking order.

### Output Format

Produce:

1. A **scoring table** with columns: Item, Impact, Confidence, Ease, ICE Score (Average), ICE Score (Multiplicative), Rank
2. A **quick wins highlight** — items scoring 7+ on Ease and 6+ on Impact. These are strong candidates for immediate action.
3. A **strategic bets highlight** — items scoring 8+ on Impact but 4 or below on Ease. These require investment but could be transformative.
4. A **RICE-ICE comparison** (if RICE scores were provided) — note where ICE and RICE rankings agree and where they diverge, with a brief explanation of why the divergence occurs

### Constraints

- Keep scoring consistent across items — if one item scores 8 on Impact, a genuinely less impactful item must score lower
- When ease is uncertain, default to the conservative (lower) estimate
- Explicitly note any items where the team's current technical skill set significantly affects the Ease score — this distinguishes inherent complexity from capability gaps
