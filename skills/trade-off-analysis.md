---
type: skill
id: trade-off-analysis
title: Trade-off Analysis
description: "Analysing trade-offs between competing priorities and constraints to surface key tensions and inform decision-making"
tags: [Production, Tested, planning:product, optimisation:prioritisation]
connections:
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "5-8 minutes"
  avg_tokens: 2500
  trigger: manual
---

## Trade-off Analysis

This skill enables rigorous analysis of the tensions between competing product priorities. Rather than pretending all good ideas can be pursued simultaneously, it surfaces the real trade-offs that product leaders must navigate and provides structured frameworks for resolving them.

### Core Capabilities

#### Identifying Trade-off Dimensions

Product prioritisation typically involves tensions across several dimensions:

- **Speed vs. quality** — shipping fast with known rough edges vs. polishing before release
- **Customer value vs. technical investment** — building features users want now vs. reducing technical debt that enables future velocity
- **Revenue vs. retention** — new features that attract customers vs. improvements that keep existing ones
- **Breadth vs. depth** — serving more use cases superficially vs. serving fewer use cases exceptionally well
- **Quick wins vs. strategic bets** — items with guaranteed small returns vs. items with uncertain but potentially large returns
- **Internal vs. external** — tooling and infrastructure improvements vs. customer-facing features

For each pair of competing items, identify which dimension(s) the tension falls on. This reframes "which feature should we build?" into "what kind of company do we want to be this quarter?"

#### Cross-Framework Comparison

When multiple scoring frameworks have been applied to the same backlog:

1. **Identify consensus items** — items that rank in the top quartile across all frameworks. These are strong candidates regardless of methodology preference.
2. **Identify divergent items** — items that rank highly on one framework but poorly on another. These are where the interesting decisions live.
3. **Analyse why divergence occurs** — typically because frameworks weight different things. RICE favours high-reach items; ICE favours easy wins; MoSCoW favours business-critical items. The divergence tells you something about the item's characteristics.
4. **Map divergence to strategy** — if your current strategic priority is growth, lean towards RICE rankings. If it is execution velocity, lean towards ICE. If it is risk reduction, lean towards MoSCoW Must Haves.

#### Constraint Analysis

Beyond scoring, real prioritisation must account for hard constraints:

- **Regulatory deadlines** — items with compliance deadlines override scoring
- **Contractual commitments** — items promised to key accounts may need prioritisation regardless of general scoring
- **Technical dependencies** — some items cannot proceed until prerequisite work is complete, regardless of their priority score
- **Resource availability** — the highest-priority item is irrelevant if the team with the required skills is fully committed elsewhere

Surface these constraints explicitly. A prioritised list that ignores constraints is a wish list, not a plan.

#### Constructing Recommendations

When presenting trade-off analysis:

1. State the trade-off clearly: "Choosing A means deferring B"
2. Quantify the cost of deferral where possible: "Deferring B by one quarter means approximately X in delayed revenue"
3. Present the recommendation with explicit reasoning: "We recommend A because the strategic alignment with OKR-2 outweighs the short-term revenue from B"
4. Identify reversibility: "This decision is easily reversible next quarter" vs. "This creates a path dependency that constrains future options"

### Constraints

- Never hide trade-offs — surfacing tension is the entire purpose of this skill
- Present trade-offs neutrally before making recommendations
- Always acknowledge what is being sacrificed, not just what is being gained
- Distinguish between reversible and irreversible decisions
