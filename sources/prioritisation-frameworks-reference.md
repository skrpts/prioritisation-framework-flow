---
type: source
id: prioritisation-frameworks-reference
title: Prioritisation Frameworks Reference
description: "Reference guide to RICE, ICE, MoSCoW, and related prioritisation methodologies"
tags: [Production, Customer-Facing, Optimisation, Research]
connections: []
metadata:
  source_type: "reference-material"
  last_updated: "2026-03-10"
---

## Prioritisation Frameworks Reference

### RICE Framework

**Origin:** Developed by Intercom's product team as a systematic approach to product prioritisation.

**Components:**
- **Reach:** The number of people or events affected within a defined time period. Always anchor to a specific timeframe (per quarter, per month) and specify whether you are counting users, accounts, or transactions.
- **Impact:** The degree of effect on each person reached. Intercom's original scale uses: 3 (massive), 2 (high), 1 (medium), 0.5 (low), 0.25 (minimal). This prevents the common mistake of using an unbounded scale where everything clusters around "high."
- **Confidence:** A percentage representing certainty about the estimates. The key insight is that confidence applies to your Reach and Impact estimates jointly, not to the initiative's likelihood of success.
- **Effort:** Person-months of work required. This is total effort, not calendar time — a two-person team working for three months is six person-months.

**Formula:** RICE = (Reach x Impact x Confidence%) / Effort

**Strengths:** Forces quantification of reach and effort; penalises low-confidence estimates; produces continuous scores that enable nuanced ranking.

**Weaknesses:** Reach is difficult to estimate for platform or infrastructure initiatives; the formula can be gamed by inflating reach estimates; it assumes linear scaling of value with reach.

---

### ICE Framework

**Origin:** Popularised by Sean Ellis (GrowthHackers) for rapid experiment prioritisation.

**Components:**
- **Impact:** How much this will move the target metric (1-10 scale)
- **Confidence:** How certain you are about the impact estimate (1-10 scale)
- **Ease:** How easy this is to implement (1-10 scale, inverse of effort)

**Formula:** ICE = Impact x Confidence x Ease (multiplicative) or ICE = (Impact + Confidence + Ease) / 3 (averaging)

**Strengths:** Faster to apply than RICE; good for growth experiments and rapid iteration; the Ease dimension rewards quick wins.

**Weaknesses:** Lacks the Reach dimension, which means it does not distinguish between initiatives affecting 100 users and 100,000 users; the 1-10 scale is subjective and hard to calibrate across teams; multiplicative scoring amplifies small differences.

---

### MoSCoW Method

**Origin:** Created by Dai Clegg in 1994, widely used in DSDM Agile methodology and requirements management.

**Categories:**
- **Must Have:** Non-negotiable requirements. The project fails without them. Apply the literal test: "Is the release useless, unsafe, or illegal without this?"
- **Should Have:** Important requirements that are painful to omit but the project remains viable without them. They will be included if at all possible.
- **Could Have:** Desirable requirements with smaller impact than Should Haves. Included only if time and resources permit.
- **Won't Have (this time):** Acknowledged requirements explicitly deferred to a future release. Not rejected — parked.

**Capacity guideline:** Must Haves should consume no more than 60% of available effort. This ensures buffer for overruns and allows Should Haves to be delivered.

**Strengths:** Forces categorical, binary decisions rather than ambiguous rankings; excellent for scope management and stakeholder communication; the "Won't Have" category makes deferrals explicit and dignified.

**Weaknesses:** Does not produce a rank order within categories; the Must Have category tends to bloat under stakeholder pressure; it is a classification tool, not a sequencing tool.

---

### When to Use Each Framework

| Scenario | Recommended Framework |
|----------|----------------------|
| Large backlog (20+ items) needing rank ordering | RICE |
| Growth experiments and rapid iteration | ICE |
| Release scoping and scope negotiation | MoSCoW |
| Stakeholder alignment on what is in/out | MoSCoW |
| Data-rich environment with analytics | RICE |
| Early-stage product with limited data | ICE |
| Combining multiple perspectives | All three in parallel |

### Common Pitfalls

1. **Scoring inflation:** Teams tend to score everything as "high impact." Use anchoring (identify one clear high and one clear low before scoring the rest).
2. **Effort underestimation:** Effort estimates are systematically optimistic. Consider applying a 1.5x multiplier to all effort estimates.
3. **Must Have bloat:** If more than 60% of items are Must Have, the team is not being rigorous enough. Apply the strict test: "Does the release fail without this?"
4. **Framework shopping:** Selecting whichever framework supports a pre-existing preference. Commit to a framework before seeing the results.
5. **Ignoring confidence:** Low-confidence high-scoring items are lottery tickets, not safe bets. Surface confidence prominently.
