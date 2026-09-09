---
name: 741-revenue-intelligence
description: Provider-neutral revenue intelligence for extracting sales-call insights, detecting buying signals and objections, mapping commercial activity to pipeline and revenue, identifying anomalies, and producing management reporting. Use with ChatGPT or Claude across CRM, analytics, call-transcript, spreadsheet, and BI data sources.
---

# 741 Revenue Intelligence

## Purpose

Turn sales conversations, CRM activity, marketing data, quotes, opportunities, and revenue records into actionable commercial intelligence without requiring Gong, HubSpot, GA4, Ahrefs, or another single vendor.

## Core workflows

### 1. Conversation intelligence
From transcripts, notes, or recordings where authorized, extract:
- objections
- buying signals
- pricing discussions
- competitor mentions
- service requirements
- promised next steps
- decision criteria
- stakeholders
- urgency/timeline
- follow-up opportunities

Do not invent quotes or timestamps. Mark paraphrases as paraphrases.

### 2. Pipeline intelligence
Analyze:
- opportunities created
- stage movement
- time in stage
- conversion rates
- win/loss reasons
- pipeline value
- weighted pipeline
- stalled opportunities
- speed-to-lead
- source/channel
- account/segment/market performance

### 3. Revenue attribution
When data supports it, evaluate first-touch, last-touch, linear, time-decay, or organization-specific attribution. Attribution is a model, not proof of causality. State data gaps and assumptions.

### 4. Commercial anomaly detection
Flag material changes such as:
- unusual drop in qualified opportunities
- sudden loss-rate increase
- slower follow-up
- concentration in one client or source
- margin deterioration when margin data is supplied
- pipeline aging
- abnormal quote-to-win changes
- declining repeat business

### 5. Buyer-language feedback loop
Aggregate recurring pains, objections, desired outcomes, vocabulary, and questions from real prospect/customer interactions. Feed approved patterns into:
- sales playbook
- outbound messaging
- content operations
- website/CRO
- ICP learning

### 6. Management reporting
Produce a concise executive view:
- what changed
- why it may have changed
- evidence
- risks
- opportunities
- recommended actions
- owner / next step when available

### 7. Readback and learning
For important commercial changes, define baseline and candidate windows, primary metric, confounders, and decision rule before judging impact. Outcomes: promote, keep testing, rollback, or unproven.

## Core output schema

```yaml
period: ""
sources: []
executive_summary: []
pipeline:
  created: null
  moved: null
  won: null
  lost: null
  value: null
  weighted_value: null
signals: []
objections: []
competitor_mentions: []
anomalies: []
attribution_findings: []
buyer_language_patterns: []
risks: []
opportunities: []
recommended_actions: []
data_gaps: []
confidence: low|medium|high
```

## Capability contracts

- `meeting.read_transcript`
- `media.transcribe`
- `crm.search_contacts`
- `crm.search_companies`
- `crm.search_deals`
- `analytics.get_pipeline_metrics`
- `analytics.get_campaign_metrics`
- `analytics.get_web_metrics`
- `analytics.compare_periods`
- `spreadsheet.read`
- `database.query`
- `files.read`
- `document.create`
- `presentation.create`

Optional approved writes:
- `crm.add_note`
- `crm.update_deal`
- `email.create_draft`

## Data rules

- Preserve source provenance and date range.
- Do not combine incompatible definitions without warning, such as leads vs qualified opportunities.
- Separate observed facts from inferred explanations.
- Do not claim causal ROI when only attribution/correlation is available.
- Minimize private transcript/customer data in outputs.
- Follow `741/core/policies/ACTION_APPROVAL_POLICY.md` for writes.

## WLP specialization hook

WLP can extend this core with logistics-specific metrics such as quotation volume, TEUs/CBM/shipments where available, warehouse occupancy, handling volumes, gross margin, revenue by service, country/agent, trade lane, customer retention, and quote-to-book conversion. Definitions belong in `741/knowledge/wlp/`.

## Portability

ChatGPT and Claude use the same reasoning model and output schema. Platform-specific retrieval, connector invocation, and artifact generation live in adapters.
