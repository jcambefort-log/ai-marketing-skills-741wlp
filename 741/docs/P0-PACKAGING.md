# 741 P0 Packaging and Installation Plan

## P0 skill set

- 741-sales-pipeline
- 741-outbound-engine
- 741-sales-playbook
- 741-revenue-intelligence

## Canonical source

Business logic lives in `741/core/skills/`. Platform adapter packages live in `741/adapters/chatgpt/skills/` and `741/adapters/claude/skills/`.

## Package contract

Each distributable skill directory must contain a valid `SKILL.md` at its root. Supporting references, templates, scripts, and assets stay inside the same directory when needed. No secrets are packaged.

## ChatGPT package

Package each selected directory from:

`741/adapters/chatgpt/skills/<skill-name>/`

The adapter is intentionally thin. Before release, include/copy any references from the core and WLP knowledge that the deployed skill must access without repository-relative paths.

### ChatGPT installation path

On ChatGPT surfaces that expose custom Skills, use the Skills management area to create/upload the skill package. In managed workspaces, admins/owners may control whether skills can be created or installed. Plugins can also bundle skills with apps/connectors where an integrated distribution package is appropriate.

GitHub repository access by itself does not install the skill into ChatGPT.

## Claude package

Package each selected directory from:

`741/adapters/claude/skills/<skill-name>/`

For Claude Code project-scoped discovery, materialize the final packages under:

`.claude/skills/<skill-name>/SKILL.md`

with supporting files in the same skill directory. Other Claude surfaces that support custom Agent Skills can use equivalent uploaded skill directories/packages.

## Validation gates before installation

1. YAML frontmatter parses.
2. Skill name matches package directory.
3. Description clearly states when the skill should trigger.
4. No API keys, tokens, passwords, personal credentials, or hidden secrets.
5. No automatic upstream telemetry/version-check startup behavior.
6. No hard dependency on one CRM/email/search/database vendor in core logic.
7. External write/send/publish/launch actions honor the 741 approval policy.
8. Repository-relative references required at runtime are bundled or rewritten for the target package.
9. ChatGPT and Claude packages produce materially equivalent business decisions from the same test fixture.
10. WLP-specific knowledge is included only where the deployed skill is intended for WLP use.

## Test fixtures for P0

Create representative fixtures for:

- new freight-forwarder prospect
- regional 3PL/warehouse prospect
- suppressed/duplicate prospect
- stalled/lost opportunity eligible for resurrection
- account-prep scenario
- pricing objection
- post-meeting follow-up
- revenue/pipeline weekly review
- missing-data scenario
- connector-unavailable scenario

Expected behavior should be defined once and tested against both platform adapters.

## Installation status

Repository packaging: IN PROGRESS.

ChatGPT installed: NOT YET CONFIRMED.

Claude installed: NOT YET CONFIRMED.

Do not mark either platform installed until the relevant product surface confirms installation.
