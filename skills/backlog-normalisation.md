---
type: skill
id: backlog-normalisation
title: Backlog Normalisation
description: "Normalising a raw product backlog into a consistent structure ready for scoring, and validating that each item carries enough detail to score"
tags: [Production, Agile, Optimisation]
connections:
  - target: llm-service
    type: runs_on
  - target: prioritisation-playbook
    type: references
metadata:
  estimated_duration: "3-5 minutes"
  avg_tokens: 2500
  trigger: manual
---

## Backlog Normalisation

Scoring frameworks assume a backlog whose items are comparable. Real backlogs are not: they arrive as Jira exports, meeting notes, spreadsheet rows and plain lists, with different fields present on each item and priority labels that mean different things to different teams. This skill is the intake stage that makes the rest of a prioritisation pipeline possible.

### Core Capabilities

#### Structural Normalisation

Reduce every item, whatever its source format, to the same shape:

- **Title** — a short noun phrase naming the change, not the symptom
- **Description** — what the change is, in one or two sentences
- **Estimated scope** — the item's apparent size, expressed in the coarsest terms the input supports
- **Requestor** — who asked for it, where the input records that
- **Existing priority labels** — carried through verbatim rather than translated, because a team's own labels are evidence about intent

Preserve the original wording wherever a field exists. Normalisation is a change of structure, not of content: rewriting an item's description during intake destroys the author's meaning before anyone has scored it.

#### Sufficiency Validation

An item that cannot be scored should be identified before scoring begins, not discovered midway through a framework pass. For each item, judge whether there is enough information to estimate reach, impact and effort at all. Flag an item as needing clarification when:

- it names a solution with no statement of the problem it addresses
- it bundles several independent changes under one title
- it describes a symptom with no indication of scope ("the app is slow")
- its effort could plausibly differ by an order of magnitude depending on an unstated decision

#### Handling Small Backlogs

Scoring frameworks are comparative instruments, and they produce little value on very short lists. Where fewer than three items are supplied, say so plainly and recommend qualitative assessment alongside the scores rather than presenting a ranking of two items as a result.

#### Output Standards

- The normalised backlog, one entry per item, in the structure above
- A separate list of items flagged for clarification, each with the specific question that would unblock scoring
- A note of any item that was split or merged during normalisation, with the reason

### Constraints

- Never invent a missing field. An absent requestor is recorded as absent, not inferred.
- Never drop an item for being poorly specified — flag it and carry it forward, because the decision to exclude work belongs to the team, not to the intake stage.
- Never translate a team's priority labels into another scheme. Carry them through and let the scoring stages compare.
