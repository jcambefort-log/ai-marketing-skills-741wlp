# 741 P0 Orchestration Adapter — ChatGPT

Status: Validated for manual handoff and same-chat logical orchestration
Provider: ChatGPT
Core contract: `741/core/orchestration/P0-ORCHESTRATION-CONTRACT.md`

## Purpose

Map the provider-neutral P0 orchestration contract into ChatGPT without changing business rules, scoring ownership, evidence requirements, UNKNOWN handling, or approval gates.

Canonical P0 flow:

`741 Sales Pipeline -> 741 Outbound Engine -> 741 Sales Playbook -> 741 Revenue Intelligence`

## Core rules

1. Sales Pipeline is the sole owner of official WLP scoring.
2. Downstream skills receive the official scorecard as frozen input.
3. UNKNOWN remains UNKNOWN until supported by evidence.
4. Outbound Engine does not recalculate official scoring.
5. Sales Playbook does not invent qualification evidence, pricing, or discounts.
6. Revenue Intelligence analyzes only observed or explicitly provided funnel events and supported financial/attribution data.
7. Drafts and plans are not treated as completed events.
8. Logical orchestration does not itself authorize external execution.
9. New scoring-relevant evidence must be routed back to Sales Pipeline before any scorecard update.
10. The provider-neutral core remains authoritative.

## Orchestration modes

### Manual handoff mode

Use when skills run in separate chats.

Procedure:

1. Run Sales Pipeline.
2. Preserve the complete official scorecard and unknowns.
3. Pass the frozen scorecard plus known facts to Outbound Engine.
4. Pass the frozen scorecard plus verified outbound findings to Sales Playbook.
5. Pass only observed funnel events and supported commercial/financial data to Revenue Intelligence.

Status: VALIDATED.

### Same-chat orchestration mode

Use when all four P0 skills are available in one ChatGPT conversation.

Procedure:

1. Apply Sales Pipeline first when official scoring is required.
2. Freeze the official scoring fields.
3. Let Outbound Engine add only its owned research/readiness/draft fields.
4. Let Sales Playbook add only its owned commercial-preparation fields.
5. Let Revenue Intelligence read only observed funnel events and supported financial/attribution evidence.
6. Preserve authoritative upstream fields unless new evidence is intentionally routed back to the owning skill.

Status: VALIDATED.

## Canonical handoff object

Conceptual minimum structure:

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

ChatGPT may represent this internally in another reliable structured form.

## Ownership boundaries

### Sales Pipeline -> Outbound Engine

Preserve exactly:

- official scores
- evidence coverage
- UNKNOWN dimensions
- qualification
- suppression state
- recommended route
- confidence

If new evidence could change scoring, route it back to Sales Pipeline. Outbound must not self-update the scorecard.

### Outbound Engine -> Sales Playbook

Pass forward:

- canonical prospect identity
- frozen official scorecard
- verified research
- unresolved unknowns
- suppression restrictions
- campaign approval state
- outbound execution state
- current commercial facts

A draft email is not evidence that outreach occurred. A designed sequence is not evidence that a reply occurred.

### Sales Playbook -> Revenue Intelligence

Revenue Intelligence receives observed events, not preparation artifacts.

Examples:

- prepared discovery questions are not a completed meeting
- proposal structure is not a sent quote
- negotiation preparation is not a negotiation event
- outbound drafts are not contact events

## Validation record

A controlled same-chat P0 test was completed using one fictitious Guatemala freight-forwarder scenario and all four skills in sequence.

Validation results:

- prospect identity remained consistent
- official scoring remained frozen downstream
- Sales Pipeline remained scoring owner
- Outbound did not modify official scoring
- Sales Playbook did not invent qualification evidence, pricing, or discounts
- Revenue Intelligence analyzed only explicitly supplied observed events
- UNKNOWN values remained UNKNOWN
- Revenue remained UNKNOWN
- Gross Profit remained UNKNOWN
- Attribution remained UNKNOWN
- no unsupported causal inference was introduced
- drafts were not treated as executed actions
- plans were not treated as completed events
- no external action was executed

Validation verdict: `PASS`

## Current validation status

- Manual logical handoff: VALIDATED
- Same-chat orchestration: VALIDATED
- Automatic multi-skill orchestration: NOT YET VALIDATED
- Live connector execution: NOT YET VALIDATED

## Next validation

Validate automatic multi-skill orchestration, followed by tool-assisted/live connector execution under the approved evidence and action policies.
