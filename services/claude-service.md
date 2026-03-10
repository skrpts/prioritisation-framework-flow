---
type: service
id: claude-service
title: Claude Service
description: "How this skrpt uses Claude for prioritisation framework analysis, scoring, and report generation"
tags: [Production, Tested]
connections:
  - target: prioritisation-framework-flow
    type: runs_on
metadata:
  provider: "anthropic"
  model: "claude-sonnet"
  estimated_tokens_per_run: 12000
---

## Claude Service — Prioritisation Framework Flow

This skrpt uses Anthropic Claude as its primary AI service for all prioritisation analysis tasks.

### Usage Pattern

Claude is invoked at each stage of the prioritisation pipeline:

1. **Backlog normalisation** — parsing unstructured backlog data into consistent format
2. **RICE scoring** — applying quantitative reach, impact, confidence, and effort assessments
3. **ICE scoring** — applying impact, confidence, and ease assessments
4. **MoSCoW classification** — categorical prioritisation with rationale
5. **Trade-off analysis** — identifying and articulating tensions between competing priorities
6. **Report generation** — synthesising all framework outputs into a stakeholder-ready document

### Model Requirements

- **Reasoning capability:** The scoring and trade-off analysis stages require structured analytical reasoning across multiple dimensions simultaneously
- **Consistency:** Scoring must remain calibrated across items within a single run — the model must maintain internal consistency when evaluating 10-30 backlog items sequentially
- **Structured output:** All stages produce structured tables and formatted reports; the model must reliably produce clean markdown tables

### Token Budget

- Typical full pipeline run: 10,000-15,000 tokens
- Individual framework stage: 2,000-3,000 tokens
- Report generation stage: 3,000-4,000 tokens

### Configuration

- Temperature: 0.3 (low temperature for consistent, analytical output)
- System prompt should emphasise analytical rigour and consistency over creativity
- For scoring stages, include calibration anchors in the context to maintain consistency
