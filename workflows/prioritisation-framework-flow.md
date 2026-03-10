---
type: workflow
id: prioritisation-framework-flow
title: Prioritisation Framework Flow
description: "Multi-stage pipeline that applies RICE, ICE, and MoSCoW scoring frameworks to a product backlog, producing ranked recommendations with detailed rationale"
tags: [Production, Tested]
connections:
  - target: scoring-model-application
    type: uses
  - target: trade-off-analysis
    type: uses
  - target: backlog-scorer
    type: uses
  - target: rice-calculator
    type: uses
  - target: ice-evaluator
    type: uses
  - target: moscow-classifier
    type: uses
  - target: prioritisation-report-generator
    type: uses
  - target: claude-service
    type: runs_on
  - target: prioritisation-frameworks-reference
    type: references
  - target: prioritisation-playbook
    type: references
  - target: scoring-matrix-template
    type: references
metadata:
  estimated_duration: "15-25 minutes"
  avg_tokens: 12000
  trigger: manual
---

## Prioritisation Framework Flow

This workflow takes a raw product backlog and systematically applies multiple prioritisation frameworks to produce a ranked, rationale-backed set of recommendations. It is designed for product managers who need to make defensible prioritisation decisions and communicate them clearly to stakeholders.

### Prerequisites

Before running this workflow, ensure you have:

- A product backlog with at least 5 items, each with a title and brief description
- Context on current business objectives and OKRs (optional but recommended)
- Team capacity information for effort estimation (optional but recommended)
- Stakeholder constraints or mandates that may override scoring (optional)

### Pipeline Stages

#### Stage 1: Backlog Intake and Normalisation

**Node:** `backlog-scorer`

- Accept the raw backlog in any format (list, table, Jira export, plain text)
- Normalise each item into a consistent structure: title, description, estimated scope, requestor, and any existing priority labels
- Validate that each item has sufficient detail for meaningful scoring
- Flag items that need clarification before scoring can proceed
- Output: a normalised backlog ready for framework application

**Error handling:** If fewer than 3 items are provided, warn the user that scoring frameworks provide limited value on very small backlogs and suggest combining with qualitative assessment.

#### Stage 2: Parallel Framework Application

Run the following three sub-stages in parallel. Each applies a different prioritisation framework to the normalised backlog.

##### Stage 2a: RICE Scoring

**Node:** `rice-calculator`
**Skill:** `scoring-model-application`

- Score each backlog item on Reach, Impact, Confidence, and Effort
- Calculate the composite RICE score for each item
- Rank items by RICE score descending
- Flag any items where confidence is below 50% — these need validation

##### Stage 2b: ICE Scoring

**Node:** `ice-evaluator`
**Skill:** `scoring-model-application`

- Score each backlog item on Impact, Confidence, and Ease
- Calculate the composite ICE score for each item
- Rank items by ICE score descending
- Note where ICE and RICE rankings diverge — these divergences are analytically valuable

##### Stage 2c: MoSCoW Classification

**Node:** `moscow-classifier`
**Skill:** `scoring-model-application`

- Classify each backlog item as Must Have, Should Have, Could Have, or Won't Have
- Provide rationale for each classification
- Cross-reference classifications against the RICE and ICE rankings for consistency checks
- Highlight any items classified as "Must Have" that scored poorly on quantitative frameworks — these may indicate political mandates vs. data-driven priorities

**Error handling:** If scoring data is ambiguous or incomplete for any item, the pipeline assigns a default confidence of "Low" and flags the item for human review rather than guessing.

#### Stage 3: Trade-off Analysis

**Node:** `trade-off-analysis` (skill)

- Compare rankings across all three frameworks
- Identify items that rank consistently high across frameworks (strong candidates)
- Identify items with significant ranking divergence (require discussion)
- Analyse trade-offs between competing priorities: quick wins vs. strategic bets, customer-facing vs. internal improvements, revenue-driving vs. cost-saving
- Produce a trade-off matrix summarising the key tensions

#### Stage 4: Report Generation

**Node:** `prioritisation-report-generator`
**References:** `scoring-matrix-template`

- Assemble all scoring data, rankings, and trade-off analysis into a structured report
- Include: executive summary, framework-by-framework results, composite ranking, trade-off analysis, and recommended prioritisation with rationale
- Format the output for stakeholder presentation
- Include a "Decisions Required" section for items where frameworks disagree

### Output

The final output is a comprehensive prioritisation report containing:

1. **Executive summary** — top 3-5 recommended priorities with one-line rationale each
2. **Scoring matrices** — RICE, ICE, and MoSCoW results in tabular format
3. **Composite ranking** — weighted aggregate ranking across frameworks
4. **Trade-off analysis** — key tensions and recommended resolutions
5. **Decisions required** — items needing stakeholder input due to framework disagreement
6. **Methodology notes** — which frameworks were applied and why

### Error Handling

- **Insufficient backlog detail:** Prompt the user for missing information before proceeding
- **Contradictory constraints:** Surface contradictions explicitly rather than silently resolving them
- **Low confidence scores:** Flag items with low confidence across frameworks and recommend further research before committing resources
