---
name: 741-outbound-engine
description: Provider-neutral B2B outbound strategy and sequence engine. Builds ICP-based campaigns, research briefs, messaging, quality reviews, deliverability reviews, capacity plans, and approved execution plans without requiring a specific data or sending platform.
---

# 741 Outbound Engine v1.1

## Purpose

Design high-quality B2B outbound campaigns from ICP to qualified conversation while separating strategy and copy from list providers, enrichment vendors, CRMs, email senders, LinkedIn tools, and automation platforms.

## Workflow

1. **Define campaign objective**
   - target segment
   - geography
   - offer/service
   - desired commercial action
   - success metric
   - campaign constraints

2. **Define ICP and exclusions**
   Specify firmographic, geographic, operational and buying-context criteria. Also define who should not be contacted.

3. **Build or ingest target list**
   Sources may include CRM, spreadsheet, business database, web research, network directories, conference lists, referrals, approved enrichment providers, or manual input.

4. **Research each account/contact**
   Separate facts from inference. Capture source and freshness for important personalization claims.

5. **Evaluate outbound readiness**
   Evaluate only dimensions explicitly supported by this skill or an approved referenced scoring model. Possible outbound-readiness dimensions include:
   - ICP relevance
   - trigger evidence
   - personalization evidence
   - likely need
   - relationship/network relevance
   - contact relevance
   - timing

   Do not invent tiers, eligibility states, hidden aggregate formulas, acronyms, or score thresholds.

6. **Choose sequence strategy**
   Define channels, number of touches, spacing, objective per touch, stop conditions and handoff criteria.

7. **Generate messaging**
   Messaging should be specific to the target and business problem. Avoid fabricated facts and unsupported personalization.

8. **Quality review**
   Evaluate:
   - relevance
   - clarity
   - credibility
   - differentiation
   - personalization
   - CTA friction
   - spamminess
   - factual support

9. **Deliverability / reputation review**
   Keep deliverability controls distinct from persuasive copy. Flag risky volume, poor list quality, misleading identity, unsupported claims, or overly aggressive cadence.

10. **Capacity plan**
   Ensure campaign volume is compatible with human follow-up capacity. Do not invent daily/weekly sending limits, operational capacity, or team workload assumptions.

11. **Human review gate**
   Present campaign, sample contacts, sequence, assumptions, exclusions, and expected actions before any external launch/write unless autonomous execution for that exact workflow has been deliberately authorized.

12. **Launch through connector**
   Use an approved campaign/email/messaging connector only after the required approval state.

13. **Readback and learning**
   Track delivery, positive replies, meetings, qualification, opportunities and revenue when data is available. Separate list quality, copy quality, offer quality and sales follow-up effects.

## Output completeness rule

When the user explicitly requests a number of outputs, examples, emails, messages, variants, targets, or sequence steps, return exactly that number unless a safety, evidence, or capability constraint prevents it. If unable, state which requested item could not be produced and why.

Example: if the user requests 3 sample email drafts, return 3 complete sample email drafts.

## Methodology integrity rules

- Do not claim that “741 requires”, “741 establishes”, or “the framework defines” a rule unless that rule is present in this skill or an approved bundled reference.
- Do not introduce unexplained concepts such as tiers, IMS, eligibility classes, maturity states, or proprietary acronyms.
- Do not import terminology from an upstream/original skill unless it has been explicitly adopted into the 741 core or WLP knowledge layer.
- Do not invent scoring weights, thresholds, or formulas.
- Unknown is not zero.
- Network membership is evidence of network membership only. It is not proof of buying intent, need, relationship with WLP, or commercial priority.
- Named networks, companies, contacts, buying signals, volumes and relationships must come from user-provided information, approved WLP knowledge, or verifiable research evidence.

## Relationship with 741 Sales Pipeline

Outbound Engine and Sales Pipeline are separate skills with a defined handoff:

- **Outbound Engine** designs target specifications, research requirements, sequence strategy, copy, deliverability review, capacity review, and campaign execution plan.
- **Sales Pipeline** owns WLP prospect qualification and priority scoring when the approved WLP Scoring Model is being used.

Outbound Engine may consume an already-produced Sales Pipeline scorecard or request that scoring be performed using the approved WLP model. It must not recreate, modify, substitute, or extend the Sales Pipeline scoring formula.

If no Sales Pipeline scorecard is available, Outbound Engine may evaluate qualitative outbound readiness using evidence, but must not present that as the official WLP Priority Score.

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
outbound_readiness_criteria: []
sequence_strategy: []
sample_drafts: []
deliverability_risks: []
capacity_considerations: []
approval_state: draft|review_required|approved_for_launch
success_metrics: []
missing_data: []
next_best_action: ""
```

## Capability contracts

Read/research:
- `crm.search_contacts`
- `crm.search_companies`
- `crm.search_deals`
- `web.search`
- `company.research`
- `signals.search`
- `spreadsheet.read`
- `analytics.get_campaign_metrics`

Draft/execution:
- `email.create_draft`
- `campaign.create_draft`
- `campaign.update_draft`
- `campaign.launch`
- `messaging.create_draft`
- `messaging.send`
- `crm.create_lead`
- `crm.add_note`

## Connector behavior

Target data/enrichment may come from any approved compatible source. Sending may be provided by any approved compatible email/campaign platform. LinkedIn execution may be manual or use an approved integration.

A connected tool does not imply authorization to send, enroll, launch, mutate CRM data, or publish.

## Fallback behavior

Without execution connectors, produce:
- target-list specification
- research plan
- campaign brief
- sequence drafts
- qualitative readiness criteria
- implementation instructions

The skill remains fully useful in draft-only mode.

## Approval policy

Follow the 741 Action Approval Policy. Drafting and launching are separate permissions.

## WLP specialization hook

For WLP tasks, use only approved WLP knowledge for freight-forwarder ICPs, services, Colón Free Zone positioning, known network relationships, target countries, qualification criteria and sales voice.

Do not assume membership in a named logistics network or a relationship with WLP unless supported by approved knowledge or evidence.

## Portability

ChatGPT and Claude use this same core business logic. Provider-specific tools and installation metadata live only in their adapters.
