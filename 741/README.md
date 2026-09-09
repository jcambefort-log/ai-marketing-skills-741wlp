# 741 AI Skills

Provider-neutral business skill architecture for WLP and related projects.

## Goal

Keep business logic portable across ChatGPT/OpenAI and Claude/Anthropic. Product-specific tools are adapters and connectors, not the skill itself.

## Structure

- `core/skills/` shared business workflows
- `core/shared/` reusable reasoning modules
- `core/capability-contracts/` capabilities requested by skills
- `core/policies/` safety, approval and data-handling rules
- `core/orchestration/` cross-skill authority and routing contracts
- `adapters/chatgpt/` ChatGPT-specific packaging/instructions
- `adapters/claude/` Claude-specific packaging/instructions
- `connectors/` optional product/platform integrations
- `knowledge/wlp/` WLP-specific knowledge and operating context
- `audit/` validation and compatibility records

## Design rules

1. Core skills must not require a specific vendor unless the business function itself is vendor-specific.
2. Skills request capabilities such as `crm.search_deals` or `email.create_draft` rather than naming HubSpot, Salesforce, Outlook, Gmail, Instantly, etc.
3. A connector may implement one or more capability contracts.
4. Missing connectors must not destroy the workflow. The skill should fall back to manual/file input or recommend compatible platforms when useful.
5. External writes, sends, publishing and destructive actions require an approval policy.
6. Secrets and credentials never live in skill instructions or committed configuration.
7. Shared core behavior should remain functionally equivalent in ChatGPT and Claude unless a platform capability makes exact parity impossible.
8. Upstream telemetry is not part of 741 core.
9. UNKNOWN remains UNKNOWN when evidence is missing.
10. Domain authorities must remain separate; downstream skills may consume authoritative outputs but may not silently rewrite them.

## P0 Commercial Core

Validated commercial core:

1. `741-sales-pipeline`
2. `741-outbound-engine`
3. `741-sales-playbook`
4. `741-revenue-intelligence`

## P1 Growth & Marketing Core

New provider-neutral P1 layer:

5. `741-growth-engine`
6. `741-content-quality`
7. `741-seo-intelligence`
8. `741-conversion-intelligence`
9. `741-deck-builder`

See `core/orchestration/P1-GROWTH-MARKETING-CONTRACT.md` for ownership and cross-skill routing.

## WLP domain specialists

WLP-specific domain authority remains outside the generic 741 core where appropriate:

- WLP Financial Sentinel
- WLP Commercial Partner
- WLP Org Guardian
- WLP Brand Expert
- Double Loop Personal WLP

These specialists may consume or supply evidence to 741 workflows without losing their domain authority.

## Upstream audit policy

The upstream `ericosiu/ai-marketing-skills` catalog is an idea and implementation source, not an authority. Upstream skills are audited before adoption and classified as:

- convert
- absorb selectively
- overlap
- defer
- no priority

Do not copy vendor-specific scripts, telemetry, credentials, scoring assumptions or automated actions into 741 core without review.
