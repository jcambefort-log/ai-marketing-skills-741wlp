# Install 741 P0 Skills in Claude

Last verified: September 2026

## Claude Code

Anthropic documents custom Agent Skills as filesystem-based directories containing a required `SKILL.md` file.

### Project-scoped installation

Place each skill at:

```text
.claude/skills/<skill-name>/SKILL.md
```

Example:

```text
.claude/
└── skills/
    ├── 741-sales-pipeline/
    │   ├── SKILL.md
    │   └── references/
    ├── 741-outbound-engine/
    │   ├── SKILL.md
    │   └── references/
    ├── 741-sales-playbook/
    │   ├── SKILL.md
    │   └── references/
    └── 741-revenue-intelligence/
        ├── SKILL.md
        └── references/
```

### Personal installation

For skills available across projects, use:

```text
~/.claude/skills/<skill-name>/SKILL.md
```

Claude discovers applicable skills automatically and Claude Code can also invoke a skill directly by its skill name.

## Claude.ai

Anthropic documents custom Skill uploads as ZIP packages on supported plans/settings with code execution enabled.

Use the standalone 741 release ZIP for the chosen skill rather than uploading the repository development adapter by itself.

## P0 install order

1. `741-sales-pipeline`
2. `741-outbound-engine`
3. `741-sales-playbook`
4. `741-revenue-intelligence`

## First validation prompts

Use the same read-only validation prompts documented in `INSTALL-CHATGPT.md`. Expected business behavior should remain equivalent across platforms.

## MCP / connector behavior

Claude tools, MCP servers, APIs, files, and other approved integrations act as capability providers. They do not replace the core skill logic.

Examples:
- CRM connector/MCP -> CRM capability contracts
- email connector/MCP -> email capability contracts
- database tool -> database capability contracts
- web/search tool -> research capability contracts

Never infer send/write/delete permission merely because a connector is available.

## Safety check

Before live use, verify:
- no API credentials are bundled;
- no automatic upstream telemetry is inherited;
- all required support files are inside the skill package;
- no repository-relative path is required at runtime;
- external actions follow the 741 action approval policy;
- WLP-specific knowledge is appropriate for the package's sharing scope.
