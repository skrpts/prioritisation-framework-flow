---
type: prompt
id: backlog-scorer
title: Backlog Scorer
description: "Score a set of backlog items using a specified framework, producing normalised and consistently calibrated scores"
tags: [Production, Agile, Optimisation]
connections:
  - target: scoring-model-application
    type: derived_from
  - target: rice-calculator
    type: uses
  - target: ice-evaluator
    type: uses
  - target: moscow-classifier
    type: uses
metadata:
  estimated_duration: "3-5 minutes"
  avg_tokens: 2500
  trigger: manual
---

## Backlog Scorer Prompt

You are a product prioritisation analyst. Your task is to take a raw product backlog and prepare it for systematic scoring across multiple prioritisation frameworks.

### Input

**Product backlog:**
{{input.backlog_items}}

**Business context (if available):**
{{input.business_context}}

**Current OKRs or strategic priorities (if available):**
Use the business context provided above.

### Instructions

1. **Normalise the backlog.** For each item in the provided backlog, extract or infer the following fields:
   - **Title:** A concise name for the initiative (10 words or fewer)
   - **Description:** A one-paragraph summary of what this initiative involves and what outcome it targets
   - **Scope estimate:** Small (< 2 weeks), Medium (2-6 weeks), Large (6-12 weeks), or XL (> 12 weeks)
   - **Requestor/Source:** Who requested this or where the idea originated (customer feedback, internal team, executive mandate, data insight)
   - **Strategic alignment:** Which OKR or strategic priority this most closely supports (if context was provided)

2. **Validate completeness.** For each item, assess whether there is sufficient information to score it meaningfully. Flag any items where:
   - The scope is unclear and could vary by more than 2x depending on interpretation
   - The target user or customer segment is undefined
   - The expected outcome is vague or unmeasurable

3. **Identify scoring anchors.** From the normalised backlog, select:
   - The item you consider highest-impact (this becomes your "5" anchor for impact scales)
   - The item you consider lowest-effort (this becomes your "5" anchor for ease scales)
   - The item with the clearest, most data-backed rationale (this becomes your 100% confidence anchor)

4. **Output the normalised backlog** in a structured table format, ready for framework-specific scoring in subsequent steps.

### Output Format

Produce:

1. A **normalised backlog table** with columns: Item #, Title, Description, Scope, Requestor, Strategic Alignment, Completeness Flag
2. A **scoring anchors section** identifying the reference points for calibration
3. A **readiness assessment** noting any items that need clarification before meaningful scoring can proceed
4. A **recommendation** on which scoring framework(s) are best suited to this particular backlog, given its size, the available data, and the decision context

### Constraints

- Do not invent information that was not provided or clearly implied
- If business context or OKRs were not provided, note this gap and proceed with scoring based on the backlog items alone
- Maintain a neutral tone — do not pre-judge any item's priority before formal scoring
- If the backlog contains fewer than 3 items, note that quantitative frameworks provide limited comparative value and suggest qualitative assessment alongside scoring
