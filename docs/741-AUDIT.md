# 741 AI Skills Audit

Branch: `741-portable-skills`

## Objective

Convert this fork into a provider-neutral business skill library that can be used with both ChatGPT/OpenAI and Claude/Anthropic while preserving the original skill logic and allowing optional integrations with external software, APIs, CRMs, databases, messaging platforms, analytics tools, and automation services.

## Architecture rules

1. Preserve original business logic before changing implementation details.
2. Separate core reasoning/workflow from vendor-specific connectors.
3. Every skill must be classified as Portable, Adaptable, or Vendor-Specific.
4. External products such as HubSpot, Instantly, Brave, QuickBooks, Google, Microsoft, Apollo, Clay, Gong, Gemini, Metricool, etc. are connectors, not the core skill.
5. A skill should know what capability it needs (CRM lookup, search, email send, spreadsheet read, analytics pull, database query, etc.) and be able to recommend compatible products when no connector is available.
6. ChatGPT and Claude adapters must use the same shared core whenever feasible.
7. Writes/actions in third-party systems must include an explicit human approval gate unless the workflow is deliberately configured for autonomous execution.
8. Telemetry/version-check behavior from the upstream project will not be inherited automatically into the 741 core.
9. Secrets/API keys stay outside skill instructions and source files.
10. Original upstream files remain available for comparison and future updates.

## Audit dimensions

Each skill is reviewed for:
- business purpose
- WLP relevance
- core portable logic
- scripts/runtime requirements
- external APIs/services
- data storage requirements
- side effects / writes
- human approval gates
- ChatGPT compatibility
- Claude compatibility
- security/privacy considerations
- recommended 741 implementation

## Repository inventory

Status values: `DEEP REVIEW`, `INITIAL REVIEW`, `PENDING`.

| Skill | Status | Initial 741 view |
|---|---|---|
| growth-engine | INITIAL REVIEW | High portability. Separate statistics/experiment core from CRM/email pacing connectors. |
| sales-pipeline | DEEP REVIEW | High WLP relevance. Separate ICP/scoring/suppression/routing/deal resurrection from HubSpot, Instantly, Brave, PostgreSQL and RB2B webhook plumbing. |
| content-ops | INITIAL REVIEW | Very high portability. Expert-panel and quality-gate logic can be shared across providers. |
| growth-signal-charts | PENDING | Likely portable with rendering/data-source adapters. |
| content-os-portable-starter | PENDING | Likely useful as a portability reference architecture. |
| personal-strategic-signal-intelligence | PENDING | Evaluate private-data boundaries and connector model. |
| outbound-engine | INITIAL REVIEW | Very high WLP relevance. Decouple ICP/copy/scoring/capacity logic from Instantly, Apollo, LeadMagic, HeyReach and sender APIs. |
| seo-ops | PENDING | Likely portable with search/GSC/SEO-provider adapters. |
| finance-ops | INITIAL REVIEW | High WLP relevance. Separate financial analysis/scenario logic from QuickBooks file conventions and current-rate web research. |
| revenue-intelligence | PENDING | Likely portable with call-recording/CRM/attribution adapters. |
| conversion-ops | PENDING | Likely highly portable. |
| podcast-ops | PENDING | Portable content workflow with media/transcript adapters. |
| team-ops | PENDING | Portable reasoning with meeting/calendar/document connectors. |
| sidebar-prioritizer | PENDING | Likely Codex-specific; may need equivalent workflow rather than direct portability. |
| sales-playbook | PENDING | Very high WLP relevance; likely highly portable. |
| autoresearch | PENDING | Portable optimization loop with runtime adapter. |
| deck-generator | PENDING | Needs presentation/image provider adapters. |
| yt-competitive-analysis | PENDING | Needs YouTube/data retrieval adapters. |
| packaging-youtube-thumbnails | PENDING | Needs image/rendering adapters. |
| video-content-engine | PENDING | Portable routing logic; media-analysis capability differs by provider. |
| video-analysis | PENDING | Needs transcript/video inspection adapters. |
| agentic-video-understanding | PENDING | Upstream is Gemini-dependent; core moment-finding logic should be separated from Gemini runtime. |
| show-and-tell-video-slate | PENDING | Likely portable editorial prioritization. |
| shortform-production | PENDING | Needs rendering/delivery adapters and approval gates. |
| shortform-idea-grill | PENDING | Likely highly portable. |
| shortform-format-library | PENDING | Portable knowledge layer with external freshness/research connectors. |
| net-new-video-editor | PENDING | Runtime-heavy; FFmpeg/edit-plan core can be shared, execution adapter required. |
| x-longform-post | PENDING | Highly portable writing/humanizer logic. |
| clone-site | PENDING | Runtime/browser-heavy; requires safety, legal and rendering review. |
| closed-loop-analytics-upgrade | PENDING | Likely architecture/meta-skill; evaluate integration with 741 core. |
| content-eval | PENDING | Likely overlaps with content-ops; evaluate consolidation. |

## Findings so far

### sales-pipeline

Portable core candidates:
- intent scoring
- ICP qualification and learning
- suppression policy
- lead routing policy
- deal resurrection scoring
- buying-signal detection
- review-queue generation

Upstream dependencies/connectors to isolate:
- HubSpot API
- Instantly API
- Brave Search API
- PostgreSQL
- RB2B webhook server
- Python runtime and environment variables

### outbound-engine

Portable core candidates:
- ICP definition
- sequence strategy
- expert-panel scoring
- copy rules
- deliverability review logic
- capacity planning
- implementation planning

Connectors to isolate:
- Instantly
- Apollo
- LeadMagic
- HeyReach or alternative LinkedIn automation
- cold-email sender APIs

Important existing safeguard: upstream already specifies a human review gate before writing to Instantly. Preserve and generalize this rule.

### growth-engine

Portable core candidates:
- experiment definition
- hypothesis/variant model
- experiment logging schema
- statistical scoring
- winner promotion
- living playbook
- next-experiment recommendation

Dependencies/connectors to isolate:
- NumPy/SciPy runtime for statistical calculations
- pipeline/CRM API
- recruiting API
- email platform API
- local experiment data directory

### content-ops

Portable core candidates:
- dynamic expert-panel assembly
- scoring rubric selection
- recursive quality loop
- variant comparison
- feedback-to-source
- learned preference/rejection patterns

This is a strong candidate for a shared 741 quality-control service used by multiple skills.

### finance-ops

Portable core candidates:
- CFO briefing model
- financial KPI/anomaly analysis
- runway and burn analysis
- scenario modeling
- development-cost methodology
- current-market-rate research workflow

Connectors/formats to isolate:
- QuickBooks exports
- file readers for CSV/XLS/XLSX
- web research source
- code repository analysis source

## Proposed 741 target structure

```text
741/
├── core/
│   ├── capability-contracts/
│   ├── policies/
│   ├── shared/
│   └── skills/
├── adapters/
│   ├── chatgpt/
│   └── claude/
├── connectors/
│   ├── crm/
│   ├── email/
│   ├── search/
│   ├── database/
│   ├── files/
│   ├── analytics/
│   └── media/
├── knowledge/
│   └── wlp/
└── docs/
```

## Capability-contract concept

Skills should request capabilities rather than products. Examples:

- `crm.search_contacts`
- `crm.search_deals`
- `crm.update_deal`
- `email.search`
- `email.create_draft`
- `email.send`
- `web.search`
- `database.query`
- `files.read_spreadsheet`
- `analytics.get_campaign_metrics`
- `calendar.create_event`
- `media.transcribe`
- `media.inspect_video`

A product adapter can satisfy one or more capabilities. For example, a CRM capability could be provided by HubSpot, Salesforce, Zoho, Dynamics, Pipedrive, a spreadsheet, or a custom database.

## Next audit work

1. Deep-review every remaining `SKILL.md`.
2. Inventory each skill's scripts, references, agents, requirements and environment variables.
3. Build a dependency/vendor matrix.
4. Identify duplicate/overlapping skills that should share common 741 modules.
5. Define the first reusable capability contracts.
6. Create ChatGPT and Claude adapter specifications.
7. Only after audit sign-off, begin refactoring/copying into the `741/` structure.
