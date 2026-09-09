# 741 P0 Orchestration Adapter — ChatGPT

Status: Draft implementation adapter for validated P0 logical integration
Provider: ChatGPT
Core contract: `741/core/orchestration/P0-ORCHESTRATION-CONTRACT.md`

## Purpose

Translate the provider-neutral P0 orchestration contract into a ChatGPT operating pattern without changing business rules, scoring ownership, evidence requirements, UNKNOWN handling, or approval gates.

This adapter does not replace the four P0 skills. It coordinates their handoffs.

Canonical P0 flow:

`741 Sales Pipeline -> 741 Outbound Engine -> 741 Sales Playbook -> 741 Revenue Intelligence`

## Governing principle

The ChatGPT adapter is thin.

It may determine how context is passed between skills and how available ChatGPT tools/plugins are resolved, but it must not redefine:

- WLP scoring
- qualification logic
- suppression rules
- revenue logic
- attribution logic
- approval policy
- capability contracts

The provider-neutral core remains authoritative.

## ChatGPT orchestration modes

### 1. Manual handoff mode

Use when skills are invoked in separate chats or when automatic context transfer is unavailable.

Procedure:

1. Run Sales Pipeline.
2. Preserve the complete official scorecard and unknowns.
3. Pass the frozen scorecard plus known facts to Outbound Engine.
4. Pass the frozen scorecard plus verified outbound findings to Sales Playbook.
5. Pass only observed funnel events and supported commercial/financial data to Revenue Intelligence.
6. Do not treat recommendations, drafts, plans, or prepared artifacts as completed events.

This is the mode used in the first validated P0 integration audit.

### 2. Same-chat orchestration mode

Use when all four skills are available in the same ChatGPT conversation and the user asks for an integrated workflow.

Procedure:

1. Build one canonical handoff object in working context.
2. Invoke/apply Sales Pipeline first when official scoring is required.
3. Freeze the resulting scoring fields.
4. Let Outbound Engine add only its owned fields.
5. Let Sales Playbook add only its owned fields.
6. Let Revenue Intelligence read only observed funnel events and supported financial/attribution data.
7. Preserve all earlier authoritative fields unless new evidence is intentionally routed back to the owning skill.

### 3. Tool-assisted orchestration mode

Use when ChatGPT has authorized plugins/connectors/files that can provide evidence or perform permitted actions.

The orchestrator may use available capabilities to:

- retrieve account or CRM facts
- search connected email/history
- inspect files
- research public company information
- read calendar or event context
- retrieve pipeline records
- draft artifacts

Tool availability never changes approval requirements.

A connected tool is evidence access or execution capability, not automatic permission.

## Canonical ChatGPT handoff object

Use the conceptual schema from the core orchestration contract. ChatGPT may keep it internally as structured text, YAML-like data, JSON-like data, or another reliable representation.

Minimum structure:

```yaml
handoff:
  prospect: {}
  facts: []
  assumptions: []
  unknowns: []
  evidence: []
  sales_pipeline: {}
  outbound: {}
  sales_playbook: {}
  revenue_intelligence: {}
```

Do not expose this structure to the user unless it improves clarity or the user requests it.

## Sales Pipeline -> Outbound Engine

When Sales Pipeline produces an official WLP scorecard:

- copy all official scoring fields exactly
- mark them as frozen
- preserve evidence coverage
- preserve UNKNOWN dimensions
- preserve qualification
- preserve suppression status
- preserve recommended route
- preserve confidence

Outbound Engine must not recalculate or reinterpret those values.

If new evidence appears during outbound research and could affect scoring:

1. capture the evidence;
2. keep the current scorecard unchanged;
3. route the evidence back to Sales Pipeline;
4. let Sales Pipeline issue an updated scorecard;
5. replace the frozen scorecard only with that official updated result.

## Outbound Engine -> Sales Playbook

Pass forward:

- canonical prospect identity
- frozen official scorecard
- verified research
- unresolved unknowns
- suppression restrictions
- campaign approval state
- outbound execution state
- current commercial facts

Do not pass a draft email as evidence that outreach occurred.
Do not pass a sequence as evidence that a reply occurred.
Do not pass readiness as evidence that an opportunity exists.

## Sales Playbook -> Revenue Intelligence

Revenue Intelligence receives observed events, not preparation artifacts.

Valid examples:

- meeting actually completed
- opportunity actually created
- quote actually sent
- closed-won actually recorded

Invalid substitutions:

- discovery questions prepared -> meeting completed
- proposal template prepared -> quote sent
- negotiation plan prepared -> negotiation occurred
- outbound draft prepared -> prospect contacted

If event status is not supported, keep it UNKNOWN or not observed as appropriate.

## Revenue and attribution guardrails

Revenue Intelligence must not infer:

- revenue from pipeline stage alone
- gross profit from revenue alone unless explicitly calculable from supported data
- attribution from the fact that Outbound Engine or Sales Playbook participated in the workflow
- causality from chronological sequence
- lost opportunity from zero closed-won if outcome is unresolved

## User-visible orchestration behavior

When the user asks to run an integrated P0 workflow, ChatGPT should normally:

1. state the current mode: analysis/review, draft/review, or execution-capable;
2. identify which facts are known and which remain UNKNOWN;
3. run the owning skill for each stage;
4. preserve upstream authoritative outputs;
5. show meaningful handoff conclusions rather than repeating every internal field;
6. explicitly state when an external action has not occurred;
7. ask for approval only when an action boundary actually requires it.

## Automatic execution boundary

Automatic logical orchestration is different from automatic external execution.

The orchestrator may move context from one P0 skill to another without separate approval when the task remains analysis/review.

It must not automatically:

- send email
- launch outreach
- publish content
- modify CRM records
- create or update external records
- approve pricing
- approve discounts
- delete data

unless the user has explicitly authorized the action and the applicable ChatGPT/plugin permissions allow it.

## Failure and fallback behavior

If a required ChatGPT skill, connector, or evidence source is unavailable:

1. preserve the current handoff state;
2. do not fabricate the missing result;
3. identify the missing capability or evidence;
4. continue in manual/draft mode where useful;
5. recommend the smallest next step required to proceed.

## Audit checklist

A ChatGPT P0 orchestration run passes when:

- the same prospect/account identity is preserved
- Sales Pipeline remains scoring authority
- Outbound does not alter official scoring
- Sales Playbook does not invent qualification evidence
- Revenue Intelligence only analyzes observed events
- UNKNOWN remains UNKNOWN
- revenue and GP are not fabricated
- attribution is not inferred
- external actions are not falsely claimed
- tool availability is not treated as authorization
- new scoring evidence is routed back to Sales Pipeline

## Current validation status

- Manual logical handoff: VALIDATED
- Same-chat orchestration: NOT YET VALIDATED
- Automatic multi-skill orchestration: NOT YET VALIDATED
- Live connector execution: NOT YET VALIDATED

## Next validation

Run one controlled same-chat P0 scenario using the canonical handoff rules and verify that all four skills preserve ownership and UNKNOWN semantics without manual copy/paste between separate chats.
