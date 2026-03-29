---
type: document
id: prioritisation-playbook
title: Prioritisation Playbook
description: "Playbook for running prioritisation sessions with teams and stakeholders"
tags: [Production, Customer-Facing, planning:product, optimisation:prioritisation]
connections:
  - target: prioritisation-frameworks-reference
    type: references
metadata:
  document_type: "playbook"
  last_updated: "2026-03-10"
---

## Prioritisation Playbook

### Purpose

This playbook guides product managers through running effective prioritisation sessions. It covers preparation, facilitation, and follow-through for both solo prioritisation work and collaborative sessions with stakeholders.

### Before the Session

#### 1. Gather the Backlog (1-2 days before)

- Collect all candidate items from Jira, Linear, Notion, spreadsheets, Slack threads, and meeting notes
- Remove duplicates and merge related items
- Ensure each item has at minimum: a title, a one-line description, and an indication of who requested it
- Aim for 10-30 items. Fewer than 10 limits framework utility; more than 30 makes the session unwieldy

#### 2. Set the Context

- Confirm the planning window (quarter, half, sprint)
- Identify the active OKRs or strategic priorities that should guide scoring
- Note any hard constraints: regulatory deadlines, contractual commitments, resource limitations, technical dependencies
- Clarify the decision authority: is this session advisory (informing a decision-maker) or decisive (the group makes the call)?

#### 3. Choose Your Framework(s)

- **RICE** if you have good data on user reach and want a quantitative ranking
- **ICE** if you need a fast, intuitive prioritisation pass or are evaluating experiments
- **MoSCoW** if the primary goal is scope management and stakeholder alignment
- **All three** if the backlog is significant and the decision is high-stakes

#### 4. Prepare the Room

- Share the backlog with participants 24 hours in advance
- Ask participants to review items and bring their perspective on impact and effort
- Prepare a shared scoring sheet (use the scoring matrix template from this skrpt)
- Set a timer — prioritisation sessions should not exceed 90 minutes

### During the Session

#### Opening (5 minutes)

State the purpose: "We are here to prioritise [X items] for [planning window]. We will use [framework(s)] and aim to leave with a ranked list and clear next steps."

Confirm the constraints and decision authority.

#### Calibration (10 minutes)

Before scoring, calibrate the group:

1. Present two items that represent opposite ends of the impact spectrum
2. Score these two items together to establish anchors
3. Confirm the scoring scales and ensure everyone understands each dimension

This step prevents the most common failure mode: different people using different mental models for the same scale.

#### Scoring (30-45 minutes)

- Score all items on one dimension at a time (all Impact scores, then all Confidence scores, etc.)
- For group sessions, use silent individual scoring followed by discussion of divergent scores
- Flag items where the group cannot reach consensus — these often reveal hidden assumptions or information gaps
- Time-box discussion per item: 2-3 minutes maximum. If consensus cannot be reached, record the range and move on.

#### Analysis (15-20 minutes)

- Calculate composite scores and produce the ranking
- Identify the top 5 and bottom 5 — do these feel right to the group?
- Run the "newspaper test": if this priority list were published externally, would it be defensible?
- Identify items where scoring and intuition diverge — these are the most valuable discussion points

#### Decision (10 minutes)

- Confirm the top priorities
- Explicitly state what is being deferred and why
- Assign owners and next steps for the top items
- Set a date for the next re-prioritisation (typically quarterly)

### After the Session

#### Immediate (same day)

- Distribute the scoring results and final ranking to all participants
- Update the project management tool (Jira, Linear, etc.) with priority labels
- Send a brief summary to stakeholders who were not in the session

#### Within One Week

- Ensure top-priority items have assigned owners and target dates
- Validate any low-confidence items flagged during scoring — commission research or spike work as needed
- Archive the scoring data for future reference (it is useful to see how priorities shift over time)

#### Ongoing

- Re-prioritise quarterly or when significant new information emerges (major customer feedback, competitive moves, strategic shifts)
- Track whether the priorities set in the session were actually executed — if the team consistently works on items not in the top priorities, the process needs improvement
- Review scoring accuracy retrospectively: did high-impact items actually deliver high impact?

### Common Failure Modes

| Failure Mode | Symptom | Remedy |
|-------------|---------|--------|
| HiPPO effect | The highest-paid person's opinion overrides scoring | Use silent individual scoring before group discussion |
| Must Have bloat | Everything is classified as Must Have | Apply the strict test; cap Must Haves at 60% of capacity |
| Analysis paralysis | The session runs long without decisions | Time-box mercilessly; imperfect decisions now beat perfect decisions later |
| Scoring theatre | The team scores items but ignores the ranking | Tie prioritisation to resource allocation decisions; make the ranking consequential |
| Stale backlog | Items on the list are outdated or irrelevant | Prune the backlog before the session; remove items older than 6 months that no one has championed |
