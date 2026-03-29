---
type: workflow
id: prioritisation-framework-flow
title: Prioritisation Framework Flow
description: "Multi-stage pipeline that applies RICE, ICE, and MoSCoW scoring frameworks to a product backlog, producing ranked recommendations with detailed rationale"
tags: [Production, Tested, Agile, Optimisation]
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
  - target: risk-assessment
    type: uses
  - target: risk-assessment-prompt
    type: uses
  - target: llm-service
    type: runs_on
  - target: prioritisation-frameworks-reference
    type: references
  - target: company-okrs
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

The final output is a structured prioritisation report containing:

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

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.backlog_items}}` | Yes | The product backlog items to prioritise — in any format (list, table, Jira export, plain text) | "1. Self-service onboarding flow 2. Enterprise SSO integration 3. Mobile push notifications 4. Dashboard redesign 5. API rate limiting" |
| `{{input.business_context}}` | No | Current business objectives, OKRs, or strategic priorities | "Q2 OKR: Increase enterprise ARR by 30%. Q2 OKR: Reduce onboarding drop-off from 60% to 30%." |
| `{{input.team_capacity}}` | No | Team capacity information for effort estimation | "2 backend engineers, 1 frontend engineer, 1 designer. Sprint velocity ~25 story points." |
| `{{input.stakeholder_constraints}}` | No | Stakeholder constraints or mandates that may override scoring | "CEO mandated SSO support by end of Q2. Legal requires GDPR audit trail by April." |

## Outputs

| Name | Description |
|------|-------------|
| Workflow output | Final output generated by this workflow |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customise them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Most stages work with any capable model; stronger models usually improve synthesis, judgement, and writing quality.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Backlog Items: "1. Self-service onboarding flow — reduce onboarding time from 15 min to 5 min
2. Enterprise SSO integration — support Okta and Azure AD for enterprise customers
3. Mobile push notifications — re-engage users who haven't opened the app in 7+ days
4. Dashboard redesign — modernise the main dashboard with customisable widgets
5. API rate limiting — prevent abuse and ensure fair usage across API consumers"

Business Context: "Q2 OKR: Increase enterprise ARR by 30%. Q2 OKR: Reduce onboarding drop-off from 60% to 30%."

Team Capacity: "2 backend engineers, 1 frontend engineer, 1 designer. Sprint velocity ~25 story points."
```

