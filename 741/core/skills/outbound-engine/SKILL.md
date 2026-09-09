---
name: 741-outbound-engine
description: Provider-neutral B2B outbound strategy and sequence engine. Builds ICP-based campaigns, research briefs, messaging, quality scoring, deliverability review, capacity plans, and execution plans without requiring a specific data or sending platform.
---

# 741 Outbound Engine

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

5. **Score targets**
   Score:
   - ICP fit
   - trigger strength
   - personalization evidence
   - likely need
   - relationship/network relevance
   - contact relevance
   - timing

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
   Ensure campaign volume is compatible with human follow-up capacity. A campaign that produces more replies than the team can handle is not well designed.

11. **Human review gate**
   Present campaign, sample contacts, sequence, assumptions, exclusions, and expected actions before any external launch/write unless autonomous execution for that exact workflow has been deliberately authorized.

12. **Launch through connector**
   Use an approved campaign/email/messaging connector only after the required approval state.

13. **Readback and learning**
   Track delivery, positive replies, meetings, qualification, opportunities and revenue when data is available. Separate list quality, copy quality, offer quality and sales follow-up effects.

## Output schema

```yaml
campaign_name: ""
objective: ""
icp: {}
exclusions: []
targets:
  - company: ""
    contact: ""
    fit_score: 0
    trigger_score: 0
    evidence: []
    confidence: low|medium|high
sequence:
  - touch: 1
    channel: email|linkedin|other
    objective: ""
    delay_days: 0
    draft: ""
quality_score: 0
risks: []
approval_state: draft|review_required|approved_for_launch
success_metrics: []
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

## Connector examples

Target data/enrichment may come from Apollo, Clay, LeadMagic, ZoomInfo, Crunchbase, network directories, web research, CRM exports or other approved sources.

Sending may be provided by Instantly, Smartlead, HubSpot, Salesforce, Gmail, Outlook/Microsoft 365 or another approved platform.

LinkedIn execution may be manual or use an approved integration. The core never assumes automated LinkedIn outreach is available or authorized.

## Fallback behavior

Without execution connectors, produce:
- target-list specification
- research plan
- campaign brief
- sequence drafts
- scoring table
- implementation instructions

The skill remains useful in draft-only mode.

## Approval policy

Follow `741/core/policies/ACTION_APPROVAL_POLICY.md`. Drafting and launching are separate permissions.

## WLP specialization hook

WLP-specific freight-forwarder ICPs, trade lanes, service propositions, Colón Free Zone positioning, network relationships, target countries, qualification criteria and sales voice belong in `741/knowledge/wlp/`.

## Portability

ChatGPT and Claude use this same core. Provider-specific tools and installation metadata live only in their adapters.
