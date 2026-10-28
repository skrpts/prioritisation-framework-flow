---
type: skill
id: moscow-classification
title: MoSCoW Classification
description: "Classifies backlog items as Must, Should, Could or Won't Have"
tags: [Product, Prioritisation]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Classifies each backlog item into Must Have, Should Have, Could Have or Won't Have with rationale, then cross-references the classifications against quantitative rankings and highlights Must Haves that scored poorly — which commonly indicates a political mandate rather than a data-driven priority.

## When to Use

- Committing to a release scope with stakeholders
- Separating genuine obligations from strongly-held preferences
- Exposing where a mandate conflicts with the scoring

## Inputs

Normalised backlog, stakeholder constraints where relevant

## Outputs

MoSCoW classification per item with rationale, plus flagged conflicts against RICE and ICE
