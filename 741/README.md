# 741 AI Skills

Provider-neutral business skill architecture for WLP and related projects.

## Goal

Keep business logic portable across ChatGPT/OpenAI and Claude/Anthropic. Product-specific tools are adapters and connectors, not the skill itself.

## Structure

- `core/skills/` shared business workflows
- `core/shared/` reusable reasoning modules
- `core/capability-contracts/` capabilities requested by skills
- `core/policies/` safety, approval and data-handling rules
- `core/orchestration/` cross-skill authority and handoff contracts
- `adapters/chatgpt/` ChatGPT-specific packaging/instructions
- `adapters/claude/` Claude-specific packaging/instructions
- `connectors/` optional product/platform integrations
- `knowledge/wlp/` WLP-specific knowledge and operating context
- `audit/` build and validation records

## Design rules

1. Core skills must not require a specific vendor unless the business function itself is vendor-specific.
2. Skills request capabilities such as `crm.search_deals` or `email.create_draft` rather than naming HubSpot, Salesforce, Outlook, Gmail, Instantly, etc.
3. A connector may implement one or more capability contracts.
4. Missing connectors must not destroy the workflow. The skill should fall back to manual/file input or recommend compatible platforms when useful.
5. External writes, sends, publishing and destructive actions require an approval policy.
6. Secrets and credentials never live in skill instructions or committed configuration.
7. Shared core behavior should remain functionally equivalent in ChatGPT and Claude unless a platform capability makes exact parity impossible.
8. Upstream telemetry is not part of 741 core.
9. UNKNOWN remains UNKNOWN unless evidence resolves it.
10. Domain authorities may be consumed by downstream skills but not silently rewritten.

## 741 skill portfolio

### P0 Commercial Core — validated

1. `sales-pipeline`
2. `outbound-engine`
3. `sales-playbook`
4. `revenue-intelligence`

### P1 Growth & Marketing — functionally validated at repository level

5. `growth-engine`
6. `content-quality`
7. `seo-intelligence`
8. `conversion-intelligence`
9. `deck-builder`

P1 authority and orchestration rules live in `741/core/orchestration/P1-GROWTH-MARKETING-CONTRACT.md`.
Repository-level validation is documented in `741/audit/741_P1_GROWTH_MARKETING_FUNCTIONAL_VALIDATION_v1.0.md`.
Live connector execution and separate Claude.ai installed-runtime validation remain outside that repository-level validation.

## WLP domain-authority boundaries

The 741 layer does not replace WLP domain-specialist skills where those exist.

- WLP Financial Sentinel: WLP pricing/financial protection and policy
- WLP Commercial Partner: WLP commercial voice and communication conventions
- WLP Org Guardian: organizational coherence and sequencing
- WLP Brand Expert: WLP brand execution
- Double Loop Personal WLP: strategic hypothesis/decision learning

741 Sales Pipeline remains the authority for official WLP prospect scoring.
741 Revenue Intelligence remains the authority for observed revenue, GP, pipeline and attribution analysis.
