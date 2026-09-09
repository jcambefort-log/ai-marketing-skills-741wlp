---
name: 741-sales-playbook
description: Provider-neutral value-based sales playbook for pre-call preparation, discovery, tiered pricing, objection handling, call review, upsell strategy, and pattern learning. Use for B2B sales preparation, proposal design, pricing conversations, call analysis, and commercial coaching in ChatGPT or Claude.
---

# 741 Sales Playbook

## Purpose

Help a commercial team prepare, conduct, review, and improve value-based B2B sales conversations without depending on a specific CRM, SEO platform, LLM provider, or call-recording platform.

## Core workflow

1. **Pre-call research**
   - company profile
   - market/geography
   - likely needs and pain points
   - current relationship/history
   - known competitors or alternatives
   - relevant commercial triggers
   - evidence and source dates

2. **Value hypothesis**
   Build an explainable hypothesis connecting the prospect's problem to measurable value. Distinguish facts from assumptions.

3. **Discovery plan**
   Prepare questions covering:
   - business objective
   - operational pain
   - current process/provider
   - financial/commercial impact
   - decision process
   - urgency/timeline
   - authority and stakeholders
   - constraints and risks

4. **Offer architecture**
   Create 3-4 clearly differentiated packages when tiered packaging is appropriate. Tie scope and price to business value, complexity, risk, service level, volume, and expected outcome.

5. **Pricing logic**
   Use value-based pricing as one input, but do not invent ROI or force a high-anchor tactic when evidence does not support it. Pricing may combine:
   - fixed fees
   - transactional rates
   - storage/handling rates
   - retainers
   - project fees
   - performance components where suitable
   - minimum commitments
   - volume tiers

6. **Objection handling**
   Classify objections such as price, timing, trust, incumbent provider, internal approval, service fit, risk, technical integration, or capacity. Respond with evidence, clarification, and next steps rather than pressure tactics.

7. **Post-call analysis**
   Score the conversation on:
   - discovery quality
   - pain/value clarity
   - stakeholder mapping
   - next-step clarity
   - evidence quality
   - pricing/packaging fit
   - objection handling
   - commitments captured

8. **Upsell / expansion**
   For existing customers, identify adjacent needs from current usage, service gaps, new geographies, new SKUs, new lanes, increased volume, fulfillment complexity, or additional value-added services.

9. **Pattern learning**
   Learn from won/lost opportunities and user feedback. Recommend updates to questions, packages, pricing patterns, and objection playbooks. Do not silently rewrite commercial policy.

## Output schema

```yaml
account: ""
meeting_goal: ""
known_facts: []
assumptions_to_validate: []
value_hypothesis: ""
discovery_questions: []
stakeholders: []
recommended_packages: []
pricing_logic: []
likely_objections: []
proof_needed: []
next_step_target: ""
confidence: low|medium|high
```

## Capability contracts

Read:
- `crm.search_contacts`
- `crm.search_companies`
- `crm.search_deals`
- `company.research`
- `market.research`
- `competitor.research`
- `meeting.read_transcript`
- `files.read`
- `spreadsheet.read`

Draft/write when authorized:
- `document.create`
- `email.create_draft`
- `crm.add_note`
- `crm.update_deal`
- `calendar.create_event`

## Approval and truthfulness rules

- Never fabricate prospect metrics, competitor performance, freight volumes, savings, or ROI.
- Label assumptions and estimates clearly.
- External research must be current enough for the decision.
- A proposed price is a recommendation, not authorization to send a commercial offer.
- Sending proposals, changing CRM stages, or committing commercial terms follows `741/core/policies/ACTION_APPROVAL_POLICY.md`.

## WLP specialization hook

WLP-specific service catalogs, tariff rules, minimum charges, margin floors, warehouse capacity, trade-lane priorities, customer segments, proposal templates, and approval thresholds belong under `741/knowledge/wlp/`.

## Portability

Use the same core in ChatGPT and Claude. Provider-specific tools and APIs stay in adapters/connectors.
