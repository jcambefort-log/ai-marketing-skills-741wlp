# 741 P0 Orchestration Contract

Status: Draft for validated P0 logical integration
Scope: Sales Pipeline -> Outbound Engine -> Sales Playbook -> Revenue Intelligence
Portability: Provider-neutral core for ChatGPT and Claude

## Purpose

Define the minimum handoff contract between the four validated P0 skills so they can exchange structured context without changing ownership, inventing missing data, or converting UNKNOWN into zero.

The contract governs logical orchestration only. It does not itself authorize outreach, sending, publishing, CRM mutation, pricing approval, or any other external action.

## Global rules

1. Evidence before inference.
2. UNKNOWN remains UNKNOWN until supported by evidence.
3. UNKNOWN must never be converted to zero, false, low, negative, absent, or disqualified by default.
4. Every skill may read upstream outputs but must respect ownership boundaries.
5. A downstream skill must not silently recalculate, reinterpret, or overwrite an upstream official field.
6. Facts, calculations, assumptions, hypotheses, and unknowns must remain distinguishable.
7. No skill may invent company identity, contacts, volumes, budget, timing, relationships, networks, revenue, gross profit, attribution, benchmarks, targets, or causal explanations.
8. Human approval is required before external execution unless explicit authorization exists under the approved action policy.
9. Connected tools or plugins do not themselves constitute authorization to act.
10. The same provider-neutral business logic should be usable in ChatGPT and Claude. Platform-specific adapters may differ only in how tools are invoked.

## Canonical prospect identity

Each handoff should preserve a canonical prospect/account reference.

Minimum fields:

- prospect_id: known identifier or UNKNOWN
- company_name: known value or UNKNOWN
- company_type: known value or UNKNOWN
- country: known value or UNKNOWN
- website: known value or UNKNOWN
- domain: known value or UNKNOWN
- primary_contact_name: known value or UNKNOWN
- primary_contact_role: known value or UNKNOWN
- primary_contact_email: known value or UNKNOWN

If identity is unresolved, downstream skills must preserve that state and may recommend research, but must not fabricate a placeholder identity as if verified.

---

# 1. Sales Pipeline -> Outbound Engine

## Sales Pipeline owns

Sales Pipeline is the sole owner of the official WLP scoring output.

Canonical fields:

- icp_score
- icp_evidence_coverage
- intent_score
- intent_evidence_coverage
- relationship_network_score
- commercial_potential_score
- timing_score
- priority_score
- priority_band
- priority_evidence_coverage
- qualification
- suppression_checks
- recommended_route
- confidence
- scoring_evidence
- scoring_unknowns

## Handoff rule

Outbound Engine must treat the scorecard as frozen input unless the user explicitly sends new evidence back through Sales Pipeline for recalculation.

Outbound Engine may not:

- create a replacement Priority Score
- modify ICP or Intent
- fill unknown scoring dimensions
- invent new official WLP scoring weights, thresholds, bands, or formulas
- reinterpret REVIEW as approved for sending

## Outbound Engine may derive

Using the frozen scorecard plus verified research, Outbound may produce:

- campaign objective
- ICP/exclusions for campaign design
- target-list specification
- research requirements
- qualitative outbound readiness observations
- sequence strategy
- draft messaging
- deliverability risks
- capacity considerations
- campaign approval state
- missing data
- next best action

## Minimum outbound input

- canonical prospect identity
- frozen Sales Pipeline scorecard
- known facts
- assumptions, if any, clearly labeled
- unknowns
- suppression status
- user-requested campaign mode

---

# 2. Outbound Engine -> Sales Playbook

## Outbound Engine owns

- research requirements
- verified research gathered for outbound preparation
- qualitative outbound readiness observations
- sequence strategy
- draft messaging
- deliverability observations
- capacity observations
- campaign approval state
- outbound execution status

## Handoff rule

Sales Playbook receives outbound findings as commercial context, not as a new scoring model.

Sales Playbook must preserve:

- official Sales Pipeline scoring unchanged
- unresolved unknowns
- suppression restrictions
- campaign approval state
- verified vs unverified research distinction

Sales Playbook may not infer that:

- an email was sent merely because a draft exists
- a reply occurred merely because a sequence was designed
- an opportunity exists merely because outbound readiness is high
- a prospect has a budget, urgency, volume, incumbent issue, or buying committee without evidence

## Sales Playbook may produce

- account situation
- known facts
- assumptions
- unknowns
- discovery objectives
- discovery questions
- value proposition
- recommended positioning
- qualification gaps
- possible objections
- objection handling
- recommended commercial approach
- proposal structure
- negotiation considerations
- next best action

## Minimum playbook input

- canonical prospect identity
- frozen scorecard
- verified outbound research
- current qualification state
- current suppression state
- current campaign approval state
- known commercial facts
- unknowns

---

# 3. Sales Playbook -> Revenue Intelligence

## Sales Playbook owns

Commercial preparation artifacts such as:

- discovery plan
- validated discovery findings, when actually obtained
- commercial positioning
- solution design assumptions
- proposal structure
- negotiation considerations
- next commercial action

A plan or recommendation is not evidence that the event occurred.

Examples:

- discovery question prepared != discovery call completed
- proposal structure prepared != proposal sent
- negotiation plan prepared != negotiation occurred
- recommended pilot != pilot launched

## Revenue Intelligence input boundary

Revenue Intelligence should analyze only observed or explicitly provided funnel events and financial/attribution data.

Canonical event fields may include:

- prospect_identified
- prospect_contacted
- response_received
- meeting_completed
- opportunity_created
- quote_sent
- closed_won
- closed_lost
- current_stage
- event_dates
- opportunity_value
- revenue
- gross_profit
- attribution_source
- attribution_evidence
- owner
- loss_or_stall_reason

Any event not explicitly supported remains UNKNOWN or not observed, as appropriate.

## Revenue Intelligence may calculate

When inputs support it:

- stage-to-stage conversion rates
- cumulative funnel conversion
- pipeline counts
- pipeline value
- revenue metrics
- gross profit metrics
- stage velocity
- aging
- attribution analysis

It must not calculate a metric whose required inputs are UNKNOWN.

## Revenue Intelligence may not infer

- revenue = 0 from zero closed deals unless revenue is explicitly zero
- gross profit = 0 from zero closed deals unless explicitly zero
- attribution from sequence design, email copy, networking, salesperson, source, or channel without evidence
- causality from temporal sequence alone
- benchmark performance without an approved benchmark
- target performance without an approved target
- loss from quote-to-close = 0 if opportunity status is unresolved

---

# 4. Canonical handoff object

A provider-neutral handoff can use this conceptual structure:

```yaml
handoff:
  prospect:
    prospect_id: UNKNOWN
    company_name: UNKNOWN
    company_type: UNKNOWN
    country: UNKNOWN
    website: UNKNOWN
    domain: UNKNOWN
    contact_name: UNKNOWN
    contact_role: UNKNOWN
    contact_email: UNKNOWN

  facts: []
  assumptions: []
  unknowns: []
  evidence: []

  sales_pipeline:
    icp_score: UNKNOWN
    icp_evidence_coverage: UNKNOWN
    intent_score: UNKNOWN
    intent_evidence_coverage: UNKNOWN
    relationship_network_score: UNKNOWN
    commercial_potential_score: UNKNOWN
    timing_score: UNKNOWN
    priority_score: UNKNOWN
    priority_band: UNKNOWN
    priority_evidence_coverage: UNKNOWN
    qualification: UNKNOWN
    suppression_checks: {}
    recommended_route: UNKNOWN
    confidence: UNKNOWN

  outbound:
    research_status: UNKNOWN
    outbound_readiness_observations: []
    campaign_approval_state: UNKNOWN
    deliverability_status: UNKNOWN
    capacity_status: UNKNOWN
    execution_status: UNKNOWN

  sales_playbook:
    discovery_status: UNKNOWN
    qualification_gaps: []
    proposal_readiness: UNKNOWN
    negotiation_readiness: UNKNOWN
    next_best_action: UNKNOWN

  revenue_intelligence:
    funnel_events: {}
    event_dates: {}
    opportunity_value: UNKNOWN
    revenue: UNKNOWN
    gross_profit: UNKNOWN
    attribution: UNKNOWN
    current_stage: UNKNOWN
    outcome: UNKNOWN
```

This is a logical schema, not a requirement that every platform use YAML internally.

---

# 5. Update and re-scoring loop

When downstream work uncovers new evidence that could change scoring:

1. Capture the new evidence with source and date.
2. Send the evidence back to Sales Pipeline.
3. Sales Pipeline alone recalculates the official WLP scorecard.
4. Produce a new frozen scorecard version.
5. Downstream skills consume the updated version.

Outbound Engine and Sales Playbook must not self-update official WLP scores.

---

# 6. Execution gate

Logical readiness does not equal execution authorization.

Before any external action, the responsible skill must verify:

- identity resolved to required level
- required suppression checks complete
- required contact data legitimately obtained and verified
- campaign or action approval state permits execution
- user authorization exists where required
- connector/tool capability exists
- operational/commercial capacity concerns have been reviewed where material

If any required gate is unresolved, the system should remain in draft, review, manual, hold, or another approved non-execution state appropriate to the owning skill.

---

# 7. Audit rules

An integrated P0 run passes when:

- the same prospect identity is preserved across all skills
- Sales Pipeline scoring remains authoritative
- Outbound does not recalculate official scoring
- Sales Playbook does not invent qualification evidence
- Revenue Intelligence analyzes only observed funnel events
- UNKNOWN values remain UNKNOWN
- revenue and GP are not fabricated
- attribution is not inferred
- causal claims are not presented without evidence
- external actions remain gated by approval
- provider-neutral behavior is preserved

## Current validated logical flow

Sales Pipeline -> Outbound Engine -> Sales Playbook -> Revenue Intelligence

Current status:

- Individual P0 skills: functionally validated
- Cross-skill logical handoff: validated
- Automatic orchestration: not yet validated
- Live connector execution: not part of this contract

## Next phase

Build provider-specific orchestration adapters that map this contract to ChatGPT and Claude while keeping the core business rules unchanged.
