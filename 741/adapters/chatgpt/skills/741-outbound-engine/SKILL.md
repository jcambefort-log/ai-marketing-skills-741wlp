---
name: 741-outbound-engine
description: Use for provider-neutral B2B outbound prospecting, ICP research, sequencing, copy generation, deliverability review, capacity planning, and approved campaign handoff. Works with ChatGPT skills plus connected apps/tools when available.
---

# 741 Outbound Engine for ChatGPT

Use the canonical workflow from `741/core/skills/outbound-engine/SKILL.md`.

## ChatGPT execution rules

1. Resolve available capabilities through connected apps, plugins, files, web research, or manual inputs.
2. Keep CRM, email, prospecting, enrichment, and sequencing vendors interchangeable.
3. Do not enroll prospects, send email, launch sequences, or mutate external systems unless the user's intent clearly authorizes that action under `741/core/policies/ACTION_APPROVAL_POLICY.md`.
4. When data is missing, continue with a clearly labeled draft or research plan instead of pretending enrichment occurred.
5. Preserve source evidence for ICP fit, personalization claims, and buying signals.

## Useful capability contracts

- `crm.search_contacts`
- `crm.search_companies`
- `email.search`
- `email.create_draft`
- `company.research`
- `signals.search`
- `web.search`
- `analytics.get_campaign_metrics`
- `campaign.create_draft`
- `campaign.launch`

## WLP context

When the task concerns Warehouse Logistics Partners, load the WLP knowledge layer and evaluate freight-forwarder, bonded-warehouse, 3PL, fulfillment, distribution-hub, and regional-trade-lane relevance before drafting outreach.
