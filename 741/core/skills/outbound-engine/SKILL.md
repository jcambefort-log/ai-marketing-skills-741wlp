---
name: 741-outbound-engine
description: Provider-neutral B2B outbound strategy and sequence engine for campaign briefs, research requirements, messaging, deliverability, capacity review and approved execution planning.
---

# 741 Outbound Engine

## Purpose

Design high-quality B2B outbound campaigns while keeping CRM, enrichment, sending and sequencing vendors interchangeable.

## Workflow

1. Define campaign objective.
2. Define ICP and exclusions.
3. Build or specify a target list.
4. Research accounts and contacts using evidence with source and freshness.
5. Evaluate qualitative outbound readiness from supported evidence only.
6. Define sequence strategy.
7. Draft factual messaging.
8. Run quality review.
9. Review deliverability.
10. Match campaign volume to real human follow-up capacity.
11. Require human review before external launch unless the exact workflow is explicitly authorized.
12. Launch only through approved capabilities.
13. Read back results when available.

## Output completeness

If the user explicitly requests a specific number of drafts, examples, variants, targets or steps, return exactly that number unless prevented by safety, evidence or capability constraints.

If the user requests 3 sample emails, return exactly 3 complete emails.

## Evidence integrity

- Separate facts, assumptions and unknowns when material.
- Unknown information stays unknown.
- Do not infer negative or positive evidence from missing information.
- Do not invent companies, contacts, volumes, relationships, buying signals, sender infrastructure, capacity, deliverability status, campaign status or execution results.
- Network membership is only evidence of network membership. It does not establish buying intent, need, relationship with WLP or commercial priority.
- Named companies, contacts, networks, signals, volumes and relationships must come from user input, approved WLP knowledge or verifiable research.

## Prospect readiness language

Describe readiness using factual observations only.

Examples:
- identity verified
- contact verified
- suppression check pending
- insufficient evidence for outreach
- sufficient evidence for draft personalization
- manual review recommended

Do not create prospect classes, proprietary stage names, hidden frameworks or unexplained acronyms.

## Methodology presentation

State the applicable instruction directly. Do not present internal package wording, prior versions, repository notes or hidden references as an external authority.

Do not cite internal skill files, package references or repository-only files in normal user-facing answers.

## Relationship with Sales Pipeline

Outbound Engine owns:
- campaign objective
- ICP/exclusions
- target-list specification
- research requirements
- qualitative outbound readiness
- sequence strategy
- messaging
- deliverability review
- capacity review
- campaign execution plan

Sales Pipeline owns:
- official WLP numeric prospect scoring
- official WLP Priority Score and band
- scoring evidence coverage
- scoring-based routing and suppression

Outbound Engine may consume a Sales Pipeline scorecard. It must not recreate, modify or extend the WLP scoring formula.

Without a Sales Pipeline scorecard, official WLP numeric prospect scores remain unknown.

## Campaign authorization states

Use only:
- `draft`
- `review_required`
- `approved_for_launch`

These describe campaign authorization only.

## Output schema

```yaml
campaign_name: ""
objective: ""
facts: []
assumptions: []
unknowns: []
icp: {}
exclusions: []
target_list_specification: {}
research_fields_required: []
outbound_readiness_observations: []
sequence_strategy: []
sample_drafts: []
deliverability_risks: []
capacity_considerations: []
approval_state: draft|review_required|approved_for_launch
success_metrics: []
missing_data: []
next_best_action: ""
```

## Capability resolution

Use `741/core/capability-contracts/README.md` to map required capabilities to connected tools when available.

A connected tool does not authorize sending, launching, publishing or mutating CRM data.

Without execution connectors, remain useful in draft-only mode and produce research specifications, campaign briefs, sequence drafts, qualitative readiness observations and implementation instructions.

## Approval policy

Use `741/core/policies/ACTION_APPROVAL_POLICY.md`.

Drafting and launching are separate permissions.

## WLP mode

Use `741/knowledge/wlp/COMPANY_PROFILE.md` and `741/knowledge/wlp/ICP.md`.

Use only approved WLP facts for services, Colón Free Zone positioning, customer types, target geographies and known relationships.

Do not assume a relationship, network membership, volume, signal or operational fact without supporting evidence.

## Portability

ChatGPT and Claude use this same core business logic. Platform-specific tool invocation belongs in adapters and connectors, not in the core workflow.
