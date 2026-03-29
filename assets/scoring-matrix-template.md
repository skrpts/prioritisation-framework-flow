---
type: asset
id: scoring-matrix-template
title: Scoring Matrix Template
description: "Template for scoring matrices used in RICE, ICE, and MoSCoW prioritisation exercises"
tags: [Production, Customer-Facing, planning:product, optimisation:prioritisation]
connections: []
metadata:
  asset_type: "template"
  format: "markdown"
---

## Scoring Matrix Template

### RICE Scoring Matrix

| # | Item | Reach (users/qtr) | Impact (0.25-3) | Confidence (%) | Effort (person-months) | RICE Score | Rank |
|---|------|--------------------|------------------|-----------------|------------------------|------------|------|
| 1 | {{item_1_title}} | | | | | | |
| 2 | {{item_2_title}} | | | | | | |
| 3 | {{item_3_title}} | | | | | | |
| 4 | {{item_4_title}} | | | | | | |
| 5 | {{item_5_title}} | | | | | | |

**RICE Formula:** (Reach x Impact x Confidence%) / Effort

**Scoring Anchors:**
- Highest-reach item: _______________
- Highest-impact item: _______________
- Lowest-effort item: _______________

---

### ICE Scoring Matrix

| # | Item | Impact (1-10) | Confidence (1-10) | Ease (1-10) | ICE Average | ICE Multiplicative | Rank |
|---|------|---------------|--------------------|--------------|--------------|--------------------|------|
| 1 | {{item_1_title}} | | | | | | |
| 2 | {{item_2_title}} | | | | | | |
| 3 | {{item_3_title}} | | | | | | |
| 4 | {{item_4_title}} | | | | | | |
| 5 | {{item_5_title}} | | | | | | |

**ICE Average Formula:** (Impact + Confidence + Ease) / 3
**ICE Multiplicative Formula:** Impact x Confidence x Ease

**Quick Wins:** Items with Ease >= 7 and Impact >= 6
**Strategic Bets:** Items with Impact >= 8 and Ease <= 4

---

### MoSCoW Classification Matrix

| # | Item | Classification | Rationale | Effort Estimate | Capacity % |
|---|------|----------------|-----------|-----------------|------------|
| 1 | {{item_1_title}} | Must / Should / Could / Won't | | | |
| 2 | {{item_2_title}} | Must / Should / Could / Won't | | | |
| 3 | {{item_3_title}} | Must / Should / Could / Won't | | | |
| 4 | {{item_4_title}} | Must / Should / Could / Won't | | | |
| 5 | {{item_5_title}} | Must / Should / Could / Won't | | | |

**Capacity Summary:**
- Must Haves: ___% of total capacity (target: <= 60%)
- Should Haves: ___%
- Could Haves: ___%
- Won't Haves: N/A (deferred)

---

### Composite Ranking

| Rank | Item | RICE Rank | ICE Rank | MoSCoW | Composite Confidence | Recommendation |
|------|------|-----------|----------|--------|----------------------|----------------|
| 1 | | | | | High / Medium / Low | |
| 2 | | | | | High / Medium / Low | |
| 3 | | | | | High / Medium / Low | |
| 4 | | | | | High / Medium / Low | |
| 5 | | | | | High / Medium / Low | |

**Composite Confidence Key:**
- **High:** All three frameworks agree on relative priority (within 2 rank positions)
- **Medium:** Two of three frameworks agree
- **Low:** All three frameworks disagree significantly

---

### Trade-off Register

| Trade-off | Option A | Option B | Recommendation | Reversible? |
|-----------|----------|----------|----------------|-------------|
| | | | | Yes / No |
| | | | | Yes / No |
| | | | | Yes / No |

---

### Session Metadata

- **Date:** {{session_date}}
- **Participants:** {{participants}}
- **Planning window:** {{planning_window}}
- **Active OKRs:** {{okrs}}
- **Total backlog items scored:** {{total_items}}
- **Frameworks applied:** RICE / ICE / MoSCoW
- **Next re-prioritisation date:** {{next_review_date}}
