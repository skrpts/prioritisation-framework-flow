---
type: skill
id: risk-assessment
title: Risk Assessment
description: "Identifying, categorising, and evaluating risks to product initiatives with mitigation strategies"
tags: [Production, Tested, Planning, Risk]
context_params:
  initiative_context:
    label: "Initiative Context"
    description: "Context for the initiative — timeline, resources, constraints"
    default: ""
    required: true
connections:
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "4 minutes"
  avg_tokens: 3000
  trigger: manual
---

## Risk Assessment

This skill identifies risks to a product initiative, evaluates their likelihood and impact, and produces mitigation strategies. It covers technical, market, operational, and strategic risk categories.

### Core Capability

Given a product initiative description and its context (timeline, resources, dependencies), this skill produces a structured risk register with severity ratings and actionable mitigation plans.

### Risk Identification

Scan the initiative across four categories:

**1. Technical Risks**
Risks related to building and operating the product.
- Can we build it with current skills and technology?
- Are there unproven technologies or integrations?
- What happens if a critical dependency changes or breaks?
- Are there performance, scalability, or security concerns?

**2. Market Risks**
Risks related to whether the product meets a real need.
- Is the problem validated with real users, or assumed?
- Could the market shift before we deliver?
- Are competitors building the same thing faster?
- Is the pricing model tested?

**3. Operational Risks**
Risks related to delivering and supporting the product.
- Do we have enough people with the right skills?
- Are there single points of failure in the team?
- Can support handle the expected volume?
- Are there regulatory or compliance requirements that could delay launch?

**4. Strategic Risks**
Risks related to the initiative's alignment with broader goals.
- Does this initiative compete with other priorities for the same resources?
- Could success in this area create problems elsewhere (cannibalisation, support burden)?
- Is leadership aligned on the strategic importance?
- What happens if we do nothing?

### Risk Evaluation

For each identified risk, assess:

| Attribute | Scale | Description |
|-----------|-------|-------------|
| **Likelihood** | Low / Medium / High | How probable is this risk materialising? |
| **Impact** | Low / Medium / High | How severe would the consequences be? |
| **Detectability** | Early / Late / After-the-fact | When would we notice this risk materialising? |
| **Velocity** | Gradual / Rapid / Instant | How quickly would the impact be felt? |

### Severity Matrix

| | Low Impact | Medium Impact | High Impact |
|---|-----------|---------------|-------------|
| **High Likelihood** | Monitor | Mitigate | Avoid or transfer |
| **Medium Likelihood** | Accept | Mitigate | Mitigate urgently |
| **Low Likelihood** | Accept | Monitor | Contingency plan |

### Mitigation Strategies

For each risk requiring action:

- **Avoid:** Change the plan to eliminate the risk entirely
- **Mitigate:** Reduce the likelihood or impact through specific actions
- **Transfer:** Shift the risk to a third party (vendor, insurance, partner)
- **Accept:** Acknowledge the risk and prepare a contingency plan
- **Contingency:** Define a trigger condition and a response plan that activates if the risk materialises

### Output Structure

The risk assessment produces:
- A risk register table (ID, category, description, likelihood, impact, severity, owner, mitigation strategy)
- Top 5 risks with detailed mitigation plans
- A risk map visualisation (likelihood vs impact plot, narrative description)
- Monitoring triggers (early warning indicators for each high-severity risk)
