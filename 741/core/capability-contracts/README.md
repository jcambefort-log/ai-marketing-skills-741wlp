# 741 Capability Contracts

Capability contracts describe **what a skill needs to do**, not which product must do it.

## Core capability namespaces

### CRM
- `crm.search_contacts`
- `crm.get_contact`
- `crm.search_companies`
- `crm.search_deals`
- `crm.get_deal`
- `crm.create_lead`
- `crm.update_contact`
- `crm.update_deal`
- `crm.add_note`

Possible providers: HubSpot, Salesforce, Microsoft Dynamics, Zoho, Pipedrive, spreadsheets, databases, custom systems.

### Email / Messaging
- `email.search`
- `email.read`
- `email.create_draft`
- `email.send`
- `email.reply`
- `messaging.create_draft`
- `messaging.send`

Possible providers: Gmail, Outlook/Microsoft 365, cold-email platforms, approved messaging systems.

### Search / Research
- `web.search`
- `web.fetch`
- `company.research`
- `market.research`
- `competitor.research`
- `signals.search`

Possible providers: native web research, search APIs, SEO platforms, business databases and specialist data providers.

### Files / Documents / Spreadsheets
- `files.search`
- `files.read`
- `files.write`
- `spreadsheet.read`
- `spreadsheet.analyze`
- `document.create`
- `presentation.create`

Possible providers: local files, SharePoint, OneDrive, Google Drive, Dropbox, document/spreadsheet services.

### Analytics
- `analytics.get_web_metrics`
- `analytics.get_campaign_metrics`
- `analytics.get_pipeline_metrics`
- `analytics.get_content_metrics`
- `analytics.compare_periods`

Possible providers: GA4, Search Console, CRM analytics, email platforms, SEO platforms, BI systems.

### Calendar / Meetings
- `calendar.search`
- `calendar.check_availability`
- `calendar.create_event`
- `meeting.read_transcript`
- `meeting.extract_actions`

### Database
- `database.query`
- `database.read_records`
- `database.write_records`

Possible providers: PostgreSQL, SQL Server, MySQL, cloud databases, approved data warehouses.

### Media
- `media.transcribe`
- `media.inspect_video`
- `media.extract_moments`
- `media.render_image`
- `media.render_video`

### Publishing / Campaign Execution
- `campaign.create_draft`
- `campaign.update_draft`
- `campaign.launch`
- `social.create_draft`
- `social.publish`
- `cms.create_draft`
- `cms.publish`

These capabilities have stronger approval requirements than read-only capabilities.

## Resolution order

When a skill requests a capability:

1. Use an already-authorized native or connected tool when available and appropriate.
2. Use an installed/approved connector implementing the capability.
3. Accept a file/manual input that provides equivalent data.
4. Recommend compatible products or integration approaches if the capability is unavailable.
5. Never pretend a connector exists or that an external action occurred when it did not.

## Portability requirement

ChatGPT and Claude adapters map their available tools to these same contracts. Platform-specific tool names stay in adapters/connectors, not in core skill logic.
