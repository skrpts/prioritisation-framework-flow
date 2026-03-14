---
type: skill
id: scoring-model-application
title: Scoring Model Application
description: "Applying quantitative scoring models (RICE, ICE) to backlog items with consistent methodology and calibrated scoring"
tags: [Production, Tested]
connections:
  - target: llm-service
    type: runs_on
  - target: prioritisation-frameworks-reference
    type: references
metadata:
  estimated_duration: "5-10 minutes per framework"
  avg_tokens: 3000
  trigger: manual
---

## Scoring Model Application

This skill enables the systematic application of quantitative prioritisation frameworks to product backlog items. It covers RICE (Reach, Impact, Confidence, Effort), ICE (Impact, Confidence, Ease), and supports adaptation to custom scoring models.

### Core Capabilities

#### Consistent Scoring Calibration

When scoring backlog items, maintain consistency by establishing anchor points before scoring begins. For each dimension:

- **Define the scale explicitly** — a 1-5 scale where 1 means "minimal" and 5 means "transformative" is more useful than an undefined numeric range
- **Set anchor examples** — identify one item that clearly represents a "1" and one that represents a "5" for each dimension, then score remaining items relative to these anchors
- **Score all items on one dimension before moving to the next** — this prevents halo effects where a generally-liked feature scores high on every dimension

#### RICE Scoring Methodology

RICE scores are calculated as: **(Reach x Impact x Confidence) / Effort**

- **Reach:** How many users or customers will this affect in a defined time period? Express as a number (e.g., "500 users per quarter"). If exact numbers are unavailable, use order-of-magnitude estimates: tens, hundreds, thousands, tens of thousands.
- **Impact:** How significantly will this affect each user reached? Use a standardised scale: 3 = massive, 2 = high, 1 = medium, 0.5 = low, 0.25 = minimal.
- **Confidence:** How certain are you about the Reach and Impact estimates? Express as a percentage: 100% = high confidence backed by data, 80% = reasonable estimate, 50% = educated guess, 20% = speculation.
- **Effort:** How many person-months will this require? Include design, development, testing, and rollout. Round to the nearest 0.5 person-months.

#### ICE Scoring Methodology

ICE scores are calculated as: **Impact x Confidence x Ease**

- **Impact:** Same scale as RICE (1-5 or the 3/2/1/0.5/0.25 scale)
- **Confidence:** Same percentage scale as RICE
- **Ease:** Inverse of effort — how easy is this to implement? 1 = very difficult, 5 = trivial. Consider technical complexity, dependencies, and team familiarity.

#### Handling Ambiguity

When backlog items lack sufficient detail for confident scoring:

1. Assign a confidence score of 50% or below
2. Note specifically what information is missing
3. Provide a scoring range rather than a single number (e.g., "RICE score: 15-45 depending on actual reach data")
4. Flag the item for further research before committing resources

#### Output Standards

All scoring output must include:

- A summary table with all items ranked by composite score
- Individual item scorecards showing each dimension's value and rationale
- Confidence indicators highlighting which scores are data-backed vs. estimated
- A "scoring assumptions" section documenting any assumptions made during the process

### Constraints

- Never present scores as objective truth — they are structured estimates
- Always surface uncertainty rather than hiding it behind precise-looking numbers
- When frameworks disagree on priority order, highlight the disagreement rather than averaging scores across frameworks
- Scoring models are tools for structured thinking, not replacements for product judgement
