---
name: 741-sales-pipeline
description: Qualify, score, suppress, route, resurrect, and learn from B2B sales opportunities using the 741 provider-neutral sales pipeline. Use when the user asks to analyze prospects, prioritize leads, review pipeline, detect buying signals, revive stalled/lost deals, or improve ICP rules.
---

# 741 Sales Pipeline for ChatGPT

Apply the canonical workflow in `741/core/skills/sales-pipeline/SKILL.md` and the capability contracts in `741/core/capability-contracts/README.md`.

## ChatGPT execution

1. Identify the user's requested sales-pipeline outcome.
2. Use connected/authorized ChatGPT tools to gather only the evidence needed.
3. Map available tools to the core capability contracts rather than changing the core workflow around a particular vendor.
4. If a needed connector is unavailable, continue with available files/manual data and identify the missing capability.
5. Produce the canonical 741 output with scores, reasons, suppression flags, route, next-best action, and confidence.
6. Apply `741/core/policies/ACTION_APPROVAL_POLICY.md` before any external write/send/launch/delete action.

## WLP mode

When the task concerns Warehouse Logistics Partners, load the relevant knowledge under `741/knowledge/wlp/` in addition to the generic core. Keep WLP rules outside the generic skill.

## Guardrails

- Never invent CRM records, intent signals, freight volumes, or contact activity.
- Do not send outreach merely because an email tool is connected.
- Do not enroll a lead in a campaign without authorization appropriate to that action.
- State when a score is based on incomplete evidence.
