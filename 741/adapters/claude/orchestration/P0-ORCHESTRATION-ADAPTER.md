# 741 P0 Orchestration Adapter — Claude

Status: Validated for P0 manual logical handoff and same-session orchestration
Provider: Claude
Core contract: `741/core/orchestration/P0-ORCHESTRATION-CONTRACT.md`

## Purpose

Translate the provider-neutral P0 orchestration contract into a Claude operating pattern without changing business rules, scoring ownership, evidence requirements, UNKNOWN handling, or approval gates.

This adapter coordinates the four P0 skills while keeping the canonical business logic provider-neutral.

Canonical P0 flow:

`741 Sales Pipeline -> 741 Outbound Engine -> 741 Sales Playbook -> 741 Revenue Intelligence`

## Governing principle

The Claude adapter is thin.

It may determine how context is passed between Claude Agent Skills, project files, MCP/connectors, or other authorized Claude capabilities, but it must not redefine:

- WLP scoring
- qualification logic
- suppression rules
- revenue logic
- attribution logic
- approval policy
- capability contracts

The provider-neutral core remains authoritative.

## Canonical-source precedence

For WLP scoring, Claude must read and apply `741/knowledge/wlp/ICP.md` exactly, including deterministic calibration anchors and confidence precedence rules.

When the WLP specialization provides an explicit anchor for the evidence at hand, that anchor overrides free-form model judgment.

Examples for the canonical P0 test scenario:

- freight forwarder + Guatemala + explicit Panama-partner need + FCL/LCL + consolidation + Colón Free Zone warehousing + regional redistribution -> use the explicit WLP anchors in `ICP.md`;
- unresolved company identity -> confidence `low`, even when evidence coverage falls in the nominal medium range.

Claude must not substitute its own 0-10 interpretation when an explicit WLP anchor applies.

## Exact-output-count compliance

If the user requests a specific number of outputs, Claude must return exactly that number unless prevented by safety or missing evidence.

Examples:

- `3 sample emails` -> exactly 3 complete draft emails;
- `10 discovery questions` -> exactly 10 discovery questions.

Do not silently reduce requested counts because the prospect is unresolved. Use generic, clearly labeled drafts/questions that preserve UNKNOWNs rather than omitting requested outputs.

This rule applies across the full integrated P0 run.

## Claude orchestration modes

### 1. Manual handoff mode

Use when skills are invoked separately or automatic context transfer is unavailable.

Procedure:

1. Run Sales Pipeline.
2. Preserve the complete official scorecard and unknowns.
3. Pass the frozen scorecard plus known facts to Outbound Engine.
4. Pass the frozen scorecard plus verified outbound findings to Sales Playbook.
5. Pass only observed funnel events and supported commercial/financial data to Revenue Intelligence.
6. Do not treat recommendations, drafts, plans, or prepared artifacts as completed events.

### 2. Same-session orchestration mode

Use when the relevant skills are available in the same Claude session/project and the user requests an integrated workflow.

Procedure:

1. Maintain one canonical handoff object in session/project context.
2. Apply Sales Pipeline first when official scoring is required.
3. Freeze the official scorecard fields.
4. Allow Outbound Engine to add only its owned fields.
5. Allow Sales Playbook to add only its owned fields.
6. Allow Revenue Intelligence to read only observed funnel events and supported financial/attribution evidence.
7. Preserve prior authoritative values unless new evidence is routed back to the owning skill.
8. Before finalizing, verify exact requested output counts and official WLP scoring/calibration conformance.

### 3. Tool-assisted orchestration mode

Use when Claude has authorized MCP servers, connectors, files, APIs, or project data that can provide evidence or perform permitted actions.

The orchestrator may use available capabilities to:

- retrieve CRM/account facts
- inspect email/history
- inspect local/project files
- research public company information
- retrieve pipeline records
- read operational or commercial artifacts
- create drafts

Tool availability does not equal permission to mutate or send.

## Canonical Claude handoff object

Use the conceptual schema from the core orchestration contract. Claude may represent it as YAML, JSON, structured Markdown, project state, or another reliable structure.

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

Do not expose this structure unless useful to the user or required for debugging/audit.

## Sales Pipeline -> Outbound Engine

When Sales Pipeline produces an official WLP scorecard:

- preserve all official scoring fields exactly
- mark them as frozen
- preserve evidence coverage
- preserve UNKNOWN dimensions
- preserve qualification
- preserve suppression state
- preserve recommended route
- preserve confidence

Outbound Engine must not recalculate or reinterpret those values.

If outbound research uncovers new evidence that could affect scoring:

1. capture the evidence with source/date when available;
2. keep the existing scorecard unchanged;
3. route the new evidence back to Sales Pipeline;
4. allow Sales Pipeline alone to issue an updated scorecard;
5. replace the frozen scorecard only with that official updated result.

## Outbound Engine -> Sales Playbook

Pass forward:

- canonical prospect identity
- frozen official scorecard
- verified research
- unresolved unknowns
- suppression restrictions
- campaign approval state
- outbound execution status
- known commercial facts

Do not treat:

- drafted email as sent outreach
- designed sequence as campaign launch
- readiness as evidence of opportunity creation
- possible objections as actual objections

## Sales Playbook -> Revenue Intelligence

Revenue Intelligence receives observed events, not preparation artifacts.

Valid examples:

- meeting actually completed
- opportunity actually created
- quote actually sent
- closed-won actually recorded

Invalid substitutions:

- discovery plan -> completed meeting
- proposal structure -> sent quote
- negotiation preparation -> negotiation event
- outbound draft -> contact event

Unsupported event status remains UNKNOWN or not observed as appropriate.

## Revenue and attribution guardrails

Revenue Intelligence must not infer:

- revenue from stage alone
- gross profit without supported financial inputs
- attribution merely because another 741 skill participated
- causality from chronological order
- loss from zero closed-won when outcome is unresolved
- benchmarks or targets not supplied by approved sources

## Claude-specific skill resolution

When the P0 skills are installed under Claude Code, expected project locations may be:

```text
.claude/skills/741-sales-pipeline/
.claude/skills/741-outbound-engine/
.claude/skills/741-sales-playbook/
.claude/skills/741-revenue-intelligence/
```

The orchestration adapter should coordinate these skills conceptually while leaving each skill's own `SKILL.md` as the authority for its business workflow.

For Claude.ai or other Claude surfaces, use the equivalent installed custom skills where supported.

## Project-state option

In Claude Code, a project may optionally persist the canonical handoff object in a project file for reproducible workflows.

Example conceptual location:

```text
.741/handoffs/<prospect-id>.yaml
```

This is optional, not required by the core contract.

If persisted:

- do not write secrets unnecessarily
- do not fabricate missing fields
- preserve source/evidence lineage
- preserve UNKNOWN explicitly
- distinguish observed events from plans

## User-visible orchestration behavior

When the user asks for an integrated P0 workflow, Claude should normally:

1. state the current mode: analysis/review, draft/review, or execution-capable;
2. identify known facts and UNKNOWNs;
3. apply the owning skill at each stage;
4. preserve authoritative upstream outputs;
5. summarize meaningful handoffs rather than duplicating all internal state;
6. clearly state when external execution has not occurred;
7. request approval only when an actual external-action boundary requires it;
8. satisfy exact user-requested output counts.

## Automatic execution boundary

Logical orchestration may move context between skills without separate approval while remaining in analysis/review.

It must not automatically:

- send email
- launch campaigns
- publish
- mutate CRM records
- approve prices or discounts
- delete data
- write to external systems

unless the user explicitly authorizes the action and the Claude runtime/MCP/connector permissions support it.

## Failure and fallback behavior

If a required skill, tool, MCP server, connector, or evidence source is unavailable:

1. preserve the current handoff state;
2. do not fabricate the missing result;
3. identify the missing capability or evidence;
4. continue in manual/draft mode where useful;
5. recommend the smallest next step required to proceed.

## Pre-finalization conformance check

Before returning an integrated P0 result, Claude should verify:

1. official WLP scoring matches all applicable deterministic anchors in `741/knowledge/wlp/ICP.md`;
2. unresolved identity forces `confidence: low` when the WLP model says so;
3. requested counts are exact;
4. frozen scorecard values were not changed downstream;
5. UNKNOWN values remain UNKNOWN;
6. drafts/plans were not converted into observed events;
7. revenue, GP, attribution, benchmarks, and causality were not inferred without evidence;
8. no external action was falsely claimed.

If any check fails, correct the output before finalizing rather than reporting PASS.

## Audit checklist

A Claude P0 orchestration run passes when:

- canonical prospect/account identity is preserved
- Sales Pipeline remains the scoring authority
- WLP deterministic scoring anchors are applied when applicable
- WLP confidence precedence is applied correctly
- Outbound does not alter official scoring
- Sales Playbook does not invent qualification evidence
- exact requested output counts are satisfied
- Revenue Intelligence only analyzes observed events
- UNKNOWN remains UNKNOWN
- revenue and GP are not fabricated
- attribution is not inferred
- external actions are not falsely claimed
- MCP/tool availability is not treated as authorization
- scoring-relevant new evidence is routed back to Sales Pipeline

## Current validation status

- Manual logical handoff: VALIDATED conceptually from provider-neutral P0 audit
- Same-session Claude orchestration: VALIDATED
- Automatic multi-skill orchestration: NOT YET VALIDATED
- Live MCP/connector execution: NOT YET VALIDATED

## Validation evidence

A controlled Claude same-session P0 retest passed after Claude reread the updated canonical WLP scoring model and this adapter.

The passing retest demonstrated:

- canonical prospect identity remained unresolved/UNKNOWN consistently across all four skills;
- Sales Pipeline produced the canonical anchored outcome: ICP 100, Intent 100, Priority 100, Priority band REVIEW, confidence LOW;
- Outbound consumed the scorecard frozen and did not recalculate it;
- exactly 3 requested sample emails were returned as generic non-sendable drafts;
- Sales Playbook returned exactly 10 requested discovery questions without inventing qualification evidence;
- Revenue Intelligence analyzed only supplied observed events;
- Revenue, Gross Profit, and Attribution remained UNKNOWN;
- no causal claims were introduced;
- no external action was executed or falsely claimed.

Overall same-session retest result: PASS.

## Historical first-test observation

The first controlled Claude same-session P0 test preserved ownership, UNKNOWN values, revenue/GP/attribution boundaries, and no-execution gates, but did not pass because:

- Claude applied free-form 0-10 scoring instead of the deterministic WLP calibration expected for the canonical scenario;
- unresolved identity was incorrectly reported as medium confidence instead of low;
- 3 requested outbound emails were reduced to 1;
- 10 requested discovery questions were reduced to 7.

Those issues were corrected through canonical deterministic scoring anchors, confidence precedence, exact-output-count compliance, and the pre-finalization conformance check.

## Next validation

The next unvalidated layer is automatic multi-skill orchestration and, separately, live MCP/connector execution. Neither is implied by same-session validation and both require their own controlled tests before being marked validated.
