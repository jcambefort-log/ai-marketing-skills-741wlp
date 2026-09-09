# Install 741 P0 Skills in ChatGPT

Last verified: September 2026

## Product availability

OpenAI currently documents Personal Skills as generally available to eligible ChatGPT Business, Enterprise, Healthcare, and Edu users, subject to workspace settings and product availability. Availability and synchronization can differ between ChatGPT surfaces.

Do not assume that seeing Plugins means Personal Skill upload is enabled for a particular account.

## Supported installation route

When the Skills interface is available:

1. Open ChatGPT.
2. In the sidebar, open **Plugins**.
3. Open the **Skills** tab.
4. Select **Create**.
5. Select **Upload from computer**.
6. Upload one self-contained 741 Skill package.
7. Allow ChatGPT to analyze the package.
8. Review the detected instructions/resources before enabling it.
9. Test it with a read-only prompt before authorizing any external write/send action.

## P0 install order

Install in this order:

1. `741-sales-pipeline`
2. `741-outbound-engine`
3. `741-sales-playbook`
4. `741-revenue-intelligence`

## First validation prompts

### Sales Pipeline

`Use 741 Sales Pipeline to evaluate these prospects. Do not write to any CRM and do not send outreach. Show ICP score, intent score, suppression flags, reasons, next-best action, and confidence.`

### Outbound Engine

`Use 741 Outbound Engine to build a draft outreach sequence for this ICP. Research only with authorized sources. Do not enroll anyone or send anything.`

### Sales Playbook

`Use 741 Sales Playbook to prepare discovery questions, objection handling, and follow-up structure for this opportunity. Separate verified facts from hypotheses.`

### Revenue Intelligence

`Use 741 Revenue Intelligence to analyze these sales notes/transcripts and identify objections, buying signals, next steps, and revenue risks. Do not modify CRM records.`

## Connected apps

Skills and apps are separate concepts. A Skill can define the workflow while connected apps provide external data/actions.

Examples:
- GitHub can provide repository access.
- Gmail or Outlook can provide email capabilities when connected and authorized.
- Calendar, CRM, analytics, file, or database apps can satisfy other capability contracts.

A missing app must not break the core workflow. The skill should fall back to uploaded/manual data or explain which capability is unavailable.

## Safety check

Before any live use, verify:
- no credentials are inside the package;
- no upstream telemetry runs automatically;
- send/publish/launch actions remain approval-gated;
- bulk writes are not implied by read access;
- WLP internal data included in the package is appropriate for the package's sharing scope.

## If the Skills tab is not available

Do not force a workaround or claim the Skill is installed. Keep the package ready and use the same 741 workflow from the repository/chat until the account or workspace exposes Skill upload, or use a supported OpenAI surface where Skills are enabled.
