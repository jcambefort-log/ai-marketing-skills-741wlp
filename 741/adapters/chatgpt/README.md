# 741 ChatGPT Adapter

## Purpose

Map the provider-neutral 741 core into ChatGPT Skills and available ChatGPT/Plugin tools without embedding ChatGPT-specific tool names inside core business logic.

## Current ChatGPT model

As of September 2026, ChatGPT Skills are reusable workflows that may include instructions, examples, code, and supporting resources. They are surfaced under Plugins > Skills on eligible accounts/workspaces. A plugin may include skills, connected apps, or both.

This adapter therefore treats a 741 skill as two layers:

1. **741 core skill**: business workflow and capability requirements.
2. **ChatGPT skill package**: ChatGPT-facing instructions plus references to supported resources and connected apps/tools.

## Packaging rule

For each portable skill, create a ChatGPT package under:

```text
741/adapters/chatgpt/skills/<skill-name>/
├── SKILL.md
├── references/
├── templates/
└── scripts/        # only when the ChatGPT skill/runtime supports and needs them
```

The ChatGPT package should remain thin. Do not duplicate business rules unnecessarily. It should point back conceptually to the canonical 741 core and translate capability contracts into ChatGPT-accessible tools.

## Invocation behavior

The ChatGPT adapter should:

1. detect when a 741 skill is relevant;
2. load/apply the matching core workflow;
3. resolve required capability contracts against tools available in the current ChatGPT session;
4. prefer already-connected and authorized tools;
5. fall back to files/manual input when needed;
6. recommend a compatible plugin/app only when the required capability is genuinely missing;
7. never claim an external action occurred unless a tool result confirms it.

## Capability mapping examples

| 741 capability | ChatGPT resolution examples |
|---|---|
| `crm.search_deals` | connected CRM plugin/app, authorized database/spreadsheet, manual export |
| `email.search` | connected Gmail/Outlook capability |
| `email.create_draft` | connected email tool supporting drafts |
| `web.search` | native web research |
| `calendar.create_event` | connected calendar tool |
| `files.read` | conversation/library file tools |
| `spreadsheet.analyze` | spreadsheet/data-analysis capability |
| `document.create` | document artifact capability |
| `presentation.create` | presentation artifact capability |

The table is illustrative, not a promise that every connector is installed.

## Action policy mapping

ChatGPT tool/app permissions and the 741 action policy both apply. If the platform or plugin requires confirmation, that requirement remains. 741 must never weaken a provider's authorization boundary.

Keep these permissions distinct:
- read
- analyze
- draft
- write
- send
- publish
- launch
- delete

## Install / creation workflow

For eligible ChatGPT accounts/workspaces, Skills are managed from Plugins > Skills. ChatGPT supports creating with chat/editor and uploading a skill from the user's computer. Uploaded skills are analyzed before becoming available and may require review or be blocked.

The repository is the source of truth for 741 development. A release process should export the desired `741/adapters/chatgpt/skills/<skill-name>/` directory into an uploadable package rather than manually rewriting the skill in the ChatGPT UI.

## Plugin relationship

A 741 ChatGPT skill does not itself guarantee access to external software. Connected apps remain separate integrations and authorization layers. When a plugin bundles a skill with an app, the app still requires its own permitted connection.

## Initial ChatGPT skill set

P0:
- 741-sales-pipeline
- 741-outbound-engine
- 741-sales-playbook
- 741-revenue-intelligence

P1:
- 741-finance-ops
- 741-content-ops
- 741-seo-ops
- 741-conversion-ops
- 741-growth-engine

## Source of truth

Canonical business behavior lives in:

```text
741/core/skills/
741/core/capability-contracts/
741/core/policies/
741/knowledge/
```

This adapter contains only ChatGPT-specific packaging and tool-resolution guidance.
