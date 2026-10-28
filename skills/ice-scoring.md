---
type: skill
id: ice-scoring
title: ICE Scoring
description: "Scores backlog items on Impact, Confidence and Ease"
tags: [Product, Prioritisation]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Applies the ICE framework to a normalised backlog: scores each item on Impact, Confidence and Ease, computes the composite, and ranks descending. Notes where ICE and RICE rankings diverge, because those divergences are the analytically interesting cases.

## When to Use

- Sanity-checking a RICE ranking with a lighter-weight framework
- Prioritising when effort estimates are too uncertain for RICE
- Surfacing items whose ranking depends on which framework is used

## Inputs

Normalised backlog, stakeholder constraints where relevant

## Outputs

ICE scores per item with composite and rank, and notes on divergence from RICE
