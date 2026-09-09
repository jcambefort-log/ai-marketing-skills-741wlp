# 741 P0 Validation Report

Status: release-preparation
Branch: `741-portable-skills`

## Scope

Validated P0 business capabilities:

1. `741-sales-pipeline`
2. `741-outbound-engine`
3. `741-sales-playbook`
4. `741-revenue-intelligence`

Platforms:
- ChatGPT / OpenAI Skills
- Claude / Anthropic Agent Skills

## Validation findings

### PASS: provider-neutral core

The four P0 cores use business capabilities rather than requiring one named CRM, email provider, database, analytics product, or outreach platform.

### PASS: action separation

Analysis, drafting, external writes, sending, publishing/launching, and destructive actions are treated as separate permission classes.

### PASS: secrets policy

The 741 layer does not embed API keys, OAuth tokens, passwords, private credentials, or `.env` secrets.

### PASS: upstream telemetry isolation

The 741 P0 core does not inherit the original repository's automatic telemetry/version-check preamble.

### PASS: ChatGPT / Claude semantic parity

Both adapters use the same canonical business logic and differ only in discovery, tool resolution, packaging, and platform-specific execution mechanics.

### PASS: SKILL.md frontmatter

P0 skill names are lowercase/hyphenated and descriptions state what the skill does and when it should be used.

### RELEASE BLOCKER FOUND: repository-relative references

Development adapters currently reference files such as:

- `741/core/skills/...`
- `741/core/capability-contracts/README.md`
- `741/core/policies/ACTION_APPROVAL_POLICY.md`
- `741/knowledge/wlp/...`

These references are valid inside the repository but are not safe assumptions for a standalone uploaded Skill ZIP.

**Resolution:** release packages must be self-contained. Each release skill will contain the instructions and minimum policy/capability material needed to operate without access to the repository checkout.

## Release package requirements

Every release skill must include:

```text
<skill-name>/
├── SKILL.md
└── references/
    ├── ACTION_POLICY.md
    ├── CAPABILITIES.md
    └── WLP_MODE.md
```

Optional folders may be added later:

```text
scripts/
templates/
examples/
```

## Portability requirements

A P0 release package must:

1. be understandable without repository-relative imports;
2. keep vendor names out of required core logic;
3. state when evidence is missing;
4. never claim an external action occurred unless the platform/tool confirms it;
5. preserve explicit approval boundaries;
6. support manual/file fallback when a connector is unavailable;
7. allow WLP specialization without exposing confidential credentials or private customer data.

## Platform verification, September 2026

### ChatGPT

OpenAI documents Skills as reusable workflows that can include instructions, examples, code, and supporting files. Eligible users can create or upload skills from the Skills section of the Plugin Directory. OpenAI Skills follow the Agent Skills open standard, but product availability depends on account/workspace and surface.

### Claude

Anthropic documents custom Agent Skills as directories containing `SKILL.md` with YAML frontmatter. Claude Code discovers project skills from `.claude/skills/<skill-name>/` and personal skills from `~/.claude/skills/<skill-name>/`. Claude.ai can accept custom Skill ZIP uploads on supported plans/settings.

## Current release state

- Core business architecture: PASS
- ChatGPT adapter design: PASS
- Claude adapter design: PASS
- Standalone packaging: IN PROGRESS
- Installation in user's ChatGPT account: NOT YET CONFIRMED
- Installation in user's Claude account: NOT YET CONFIRMED
- Merge to `main`: NOT REQUESTED / NOT PERFORMED
