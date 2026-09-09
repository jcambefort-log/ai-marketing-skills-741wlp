---
name: 741-sales-pipeline
description: Qualify, score, suppress, route, resurrect, and learn from B2B sales opportunities using the 741 provider-neutral sales pipeline. Use for prospect qualification, lead prioritization, pipeline review, buying-signal detection, deal resurrection, and ICP learning.
---

# 741 Sales Pipeline for Claude

Apply the canonical workflow in `741/core/skills/sales-pipeline/SKILL.md` and capability contracts in `741/core/capability-contracts/README.md`.

## Claude execution

1. Identify the requested sales-pipeline outcome.
2. Resolve needed capability contracts against tools, MCP connectors, APIs, project files, or user-provided data available in the current Claude environment.
3. Keep vendor-specific tool names and authentication outside the core workflow.
4. If a connector is unavailable, continue with available files/manual data and identify the missing capability.
5. Return the canonical 741 scoring/routing output and confidence.
6. Apply `741/core/policies/ACTION_APPROVAL_POLICY.md` before external writes, sends, launches, or destructive actions.

## WLP mode

For Warehouse Logistics Partners work, use `741/knowledge/wlp/ICP.md` as the authoritative WLP scoring model and the relevant approved WLP knowledge under `741/knowledge/wlp/`.

### Display precedence

When `741/knowledge/wlp/ICP.md` says that a material identity or suppression question remains, the user-visible `priority_band` must be `REVIEW`.

Do not display `P2 HIGH - provisional`, `P1 CRITICAL`, or another numeric band as the operative priority band when `REVIEW` precedence applies. A numeric-band counterfactual may be mentioned only as explanatory context, clearly subordinate to the official displayed band.

If company identity is materially unresolved, apply the WLP confidence-precedence rule and return `confidence: low` even when evidence coverage falls in the nominal medium range.

## Evidence discipline

- Never invent CRM records, intent signals, freight volumes, contact activity, company identity, relationship history, network membership, sender identity, or source verification.
- Network names or memberships may be scored or stated as facts only when supported by user input, approved WLP knowledge, or verified research for the prospect.
- Tool availability is not blanket authorization.
- Do not send or enroll outreach without appropriate user authorization.
- State when scoring relies on incomplete evidence.
- Unknown is not zero and unknown suppression checks are not clear.
