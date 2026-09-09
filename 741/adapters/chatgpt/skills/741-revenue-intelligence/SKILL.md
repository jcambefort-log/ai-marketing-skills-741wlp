---
name: 741-revenue-intelligence
description: Use for cross-source revenue analysis, pipeline health, conversation intelligence, attribution, anomaly detection, forecast evidence, and executive commercial recommendations in ChatGPT.
---

# 741 Revenue Intelligence for ChatGPT

Use `741/core/skills/revenue-intelligence/SKILL.md` as the canonical workflow.

## ChatGPT execution rules

1. Discover available CRM, email, analytics, files, meeting/transcript, finance, and web sources.
2. Normalize metrics before comparing systems or periods.
3. Label evidence quality and missing data.
4. Separate observation, inference, recommendation, and forecast.
5. Never fabricate attribution, pipeline values, conversion rates, or buyer quotes.
6. External writes/actions follow the 741 approval policy.

## Useful capability contracts

- `analytics.get_pipeline_metrics`
- `analytics.get_campaign_metrics`
- `analytics.get_web_metrics`
- `analytics.compare_periods`
- `crm.search_deals`
- `meeting.read_transcript`
- `email.search`
- `spreadsheet.read`
- `database.query`
- `web.search`

## WLP context

For WLP, prioritize revenue by service line, client type, geography/trade lane, quote-to-win conversion, lost reasons, margin quality when available, warehouse/3PL opportunities, freight-forwarder agent relationships, customer concentration, pipeline coverage, and progress against management revenue targets.
