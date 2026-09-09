---
name: 741-outbound-engine
description: Provider-neutral B2B outbound prospecting, ICP research, sequencing, copy generation, deliverability review, capacity planning, and approved campaign handoff for Claude.
---

# 741 Outbound Engine for Claude

Apply the canonical workflow in `741/core/skills/outbound-engine/SKILL.md`.

Resolve capabilities through Claude's available project tools, Agent Skills, MCP integrations, files, web/search capabilities, APIs, or manual inputs. Keep CRM, enrichment, email, and sequencing vendors outside the core logic.

Do not send email, enroll prospects, launch sequences, or mutate external systems without the required authorization under `741/core/policies/ACTION_APPROVAL_POLICY.md`.

For WLP tasks, load the WLP knowledge layer and evaluate freight-forwarder, bonded-warehouse, 3PL, fulfillment, distribution-hub, and regional trade-lane fit before generating outreach.

## Evidence and draft guardrails

- Consume the official Sales Pipeline scorecard as frozen input when provided. Do not recalculate, reinterpret, or replace its official WLP scoring fields.
- Never insert a sender name, signature, title, phone number, email address, or other sender identity unless that identity is explicitly supplied by the user or available in approved session/context evidence for the requested draft.
- Never present a logistics-network membership, shared network, referral path, prior relationship, or agent-to-agent relationship as a fact without explicit supporting evidence.
- Network names may be used as discovery examples only when clearly labeled as examples, not as known facts about the prospect or WLP relationship.
- If prospect identity is unresolved, drafts may remain generic and non-sendable. Do not fill missing personalization fields by inference.
- A connected tool does not authorize sending, launching, publishing, or CRM mutation.
- If the user requests an exact number of drafts, return exactly that number unless safety or evidence constraints prevent it.
