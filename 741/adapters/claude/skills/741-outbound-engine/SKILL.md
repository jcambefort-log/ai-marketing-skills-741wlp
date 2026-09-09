---
name: 741-outbound-engine
description: Provider-neutral B2B outbound prospecting, ICP research, sequencing, copy generation, deliverability review, capacity planning, and approved campaign handoff for Claude.
---

# 741 Outbound Engine for Claude

Apply the canonical workflow in `741/core/skills/outbound-engine/SKILL.md`.

Resolve capabilities through Claude's available project tools, Agent Skills, MCP integrations, files, web/search capabilities, APIs, or manual inputs. Keep CRM, enrichment, email, and sequencing vendors outside the core logic.

Do not send email, enroll prospects, launch sequences, or mutate external systems without the required authorization under `741/core/policies/ACTION_APPROVAL_POLICY.md`.

For WLP tasks, load the WLP knowledge layer and evaluate freight-forwarder, bonded-warehouse, 3PL, fulfillment, distribution-hub, and regional trade-lane fit before generating outreach.
