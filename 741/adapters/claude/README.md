# 741 Claude Adapter

## Purpose

Map the provider-neutral 741 core into Anthropic Agent Skills / Claude Code while preserving the same business logic, capability contracts, and approval policies used by the ChatGPT adapter.

## Current Claude skill model

As of September 2026, Claude Agent Skills use directories containing a `SKILL.md` file with YAML frontmatter. In Claude Code, project skills are discovered from `.claude/skills/<skill-name>/SKILL.md`; personal skills can live under `~/.claude/skills/`. Claude.ai also supports custom skills, while API/managed-agent workflows may use uploaded skill packages depending on the product surface.

## Packaging rule

The repository adapter source lives under:

```text
741/adapters/claude/skills/<skill-name>/
├── SKILL.md
├── references/
├── templates/
└── scripts/
```

For a Claude Code project release, materialize/copy each chosen package to exactly:

```text
.claude/skills/<skill-name>/SKILL.md
```

with its supporting files under the same skill directory.

Do not nest the skill another level below `.claude/skills/<skill-name>/` when project-start discovery is required.

## SKILL.md requirements

Each Claude package must begin with YAML frontmatter including:

```yaml
---
name: 741-sales-pipeline
description: Clear description of what the skill does and when to use it.
---
```

Names should remain lowercase/hyphenated and avoid provider-reserved wording.

## Invocation behavior

The Claude adapter should:

1. determine the relevant 741 skill from the user's task;
2. apply the canonical core workflow;
3. resolve requested capability contracts against tools/MCP connectors/files available in the Claude environment;
4. use manual/file inputs when direct integration is unavailable;
5. separate analysis/drafting from external mutations;
6. preserve evidence, uncertainty, and approval state;
7. never treat an available connector as blanket authorization.

## Capability resolution

Examples:

| 741 capability | Claude resolution examples |
|---|---|
| `crm.search_deals` | configured MCP/connector, API tool, database/file export |
| `email.search` | configured email connector/MCP or exported messages |
| `web.search` | available web/search tool in the current Claude surface |
| `database.query` | configured DB tool/MCP or local approved data |
| `files.read` | Claude Code filesystem/project context or uploaded file |
| `media.inspect_video` | available media capability or approved external adapter |

Exact tool names stay outside the core because they differ by Claude product and user environment.

## Action policy mapping

Apply `741/core/policies/ACTION_APPROVAL_POLICY.md` in addition to Anthropic/runtime permissions.

A skill must not infer:
- send permission from read permission;
- publish permission from draft permission;
- database write permission from database query access;
- CRM mutation permission from CRM visibility.

## Claude Code installation target

For project-scoped use:

```text
.claude/
└── skills/
    ├── 741-sales-pipeline/
    │   └── SKILL.md
    ├── 741-outbound-engine/
    │   └── SKILL.md
    ├── 741-sales-playbook/
    │   └── SKILL.md
    └── 741-revenue-intelligence/
        └── SKILL.md
```

This project-level package can coexist with other Claude Code project instructions.

## Claude.ai / API note

The same skill directory can be packaged for upload where the relevant Claude surface supports custom Agent Skills. Release tooling should create the upload package from this adapter directory rather than creating a second independent version.

## Initial Claude skill set

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

Canonical behavior lives in:

```text
741/core/skills/
741/core/capability-contracts/
741/core/policies/
741/knowledge/
```

The Claude adapter should stay thin and contain only Claude-specific discovery, packaging, and tool-resolution guidance.
