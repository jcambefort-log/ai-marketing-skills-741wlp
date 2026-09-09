---
name: 741-sales-pipeline
description: Provider-neutral sales pipeline intelligence for qualification, scoring, suppression, routing, deal resurrection, buying-signal detection, and ICP learning. Designed to work with ChatGPT or Claude and any compatible CRM, email, search, database, spreadsheet, or manual data source.
---

# 741 Sales Pipeline

## Purpose

Turn raw prospects, companies, website visitors, leads, and historical opportunities into an ordered commercial pipeline without requiring a specific CRM or outreach platform.

The core workflow is product-neutral. HubSpot, Salesforce, Dynamics, Zoho, Pipedrive, Instantly, Apollo, spreadsheets, databases, and other systems are optional connectors.

## Core workflow

1. **Ingest evidence**
   - Accept leads from CRM, files, spreadsheets, forms, web signals, manual input, website identification tools, databases, or approved connectors.
   - Preserve source and timestamp for each material data point.

2. **Normalize the prospect/company**
   - Company
   - person/contact
   - role/seniority
   - geography
   - industry
   - company size
   - known trade lanes or markets when relevant
   - source
   - prior relationship
   - engagement or intent signals

3. **Score ICP fit**
   Evaluate fit against the configured ICP. Keep the scoring model explainable and editable.

4. **Score intent / buying signal**
   Use available evidence such as relevant page visits, RFQ activity, hiring, expansion, funding, new market entry, partner searches, shipment/logistics needs, previous quotes, or recent engagement.

5. **Run suppression checks**
   Check for reasons not to contact or not to route automatically, including:
   - existing active customer relationship
   - active opportunity already owned
   - recent outreach / duplicate sequence
   - explicit opt-out / do-not-contact
   - incompatible geography or segment
   - duplicate company/contact
   - insufficient evidence
   - legal/compliance restriction supplied by the organization

6. **Route the lead**
   Assign a recommended route based on fit, intent, relationship, geography, service need, urgency, and ownership rules.

7. **Generate next-best action**
   Examples:
   - research further
   - qualify manually
   - create email draft
   - schedule sales follow-up
   - add to review queue
   - create opportunity
   - resurrect prior deal
   - suppress / do not contact

8. **Deal resurrection**
   Evaluate lost/stalled deals using age, loss reason, relationship strength, new triggers, champion movement, service changes, new geography, and present-day fit.

9. **ICP learning**
   Compare approved/rejected leads and won/lost opportunities to propose changes to ICP weights or filters. Do not silently rewrite ICP rules. Return recommendations for review.

## Core output schema

For each prospect/company, return:

```yaml
company: ""
contact: ""
source: ""
icp_score: 0
intent_score: 0
priority_score: 0
qualification: qualified|review|disqualified|suppressed
reasons:
  - ""
suppression_flags:
  - ""
recommended_route: ""
next_best_action: ""
required_capabilities:
  - ""
confidence: low|medium|high
```

## Capability contracts

Use these when available:

### Read capabilities
- `crm.search_contacts`
- `crm.search_companies`
- `crm.search_deals`
- `email.search`
- `web.search`
- `company.research`
- `signals.search`
- `database.query`
- `spreadsheet.read`
- `analytics.get_pipeline_metrics`

### Draft / write capabilities
- `email.create_draft`
- `crm.create_lead`
- `crm.update_contact`
- `crm.update_deal`
- `crm.add_note`
- `calendar.create_event`

Read-only analysis should continue even when write capabilities are unavailable.

## Connector behavior

Do not hard-code one platform into the core.

Examples:
- CRM: HubSpot, Salesforce, Dynamics, Zoho, Pipedrive, spreadsheet, custom DB
- Email: Gmail, Outlook/Microsoft 365, approved outreach platform
- Search/signals: native web research, Brave, Google, data providers, SEO tools
- Database: PostgreSQL, SQL Server, MySQL, warehouse, spreadsheet

If no connector is available:
1. accept manual/file input;
2. explain which capability is missing;
3. recommend compatible integration options when useful.

## Approval gates

Follow `741/core/policies/ACTION_APPROVAL_POLICY.md`.

In particular:
- analysis does not authorize CRM mutation;
- creating an email draft does not authorize sending it;
- adding a lead to an outreach sequence is a launch/write action and requires appropriate user intent/approval;
- bulk changes require explicit scope confirmation.

## WLP specialization hook

WLP-specific ICP, services, trade lanes, geography, customer types, qualification thresholds, exclusions, value proposition, and routing rules belong in `741/knowledge/wlp/`, not in this generic core file.

## Portability

The same workflow must be usable by ChatGPT and Claude. Platform-specific tool invocation belongs in `741/adapters/chatgpt/` and `741/adapters/claude/`.
