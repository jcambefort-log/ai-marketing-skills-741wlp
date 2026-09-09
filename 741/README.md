# 741 AI Skills

Provider-neutral business skill architecture for WLP and related projects.

## Goal

Keep business logic portable across ChatGPT/OpenAI and Claude/Anthropic. Product-specific tools are adapters and connectors, not the skill itself.

## Structure

- `core/skills/` shared business workflows
- `core/shared/` reusable reasoning modules
- `core/capability-contracts/` capabilities requested by skills
- `core/policies/` safety, approval and data-handling rules
- `adapters/chatgpt/` ChatGPT-specific packaging/instructions
- `adapters/claude/` Claude-specific packaging/instructions
- `connectors/` optional product/platform integrations
- `knowledge/wlp/` WLP-specific knowledge and operating context

## Design rules

1. Core skills must not require a specific vendor unless the business function itself is vendor-specific.
2. Skills request capabilities such as `crm.search_deals` or `email.create_draft` rather than naming HubSpot, Salesforce, Outlook, Gmail, Instantly, etc.
3. A connector may implement one or more capability contracts.
4. Missing connectors must not destroy the workflow. The skill should fall back to manual/file input or recommend compatible platforms when useful.
5. External writes, sends, publishing and destructive actions require an approval policy.
6. Secrets and credentials never live in skill instructions or committed configuration.
7. Shared core behavior should remain functionally equivalent in ChatGPT and Claude unless a platform capability makes exact parity impossible.
8. Upstream telemetry is not part of 741 core.

## Initial WLP priority

1. sales-pipeline
2. outbound-engine
3. sales-playbook
4. revenue-intelligence
5. finance-ops
6. content-ops
7. seo-ops
8. conversion-ops
9. growth-engine

All upstream skills will still be audited and classified.
