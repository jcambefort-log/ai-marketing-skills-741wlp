# 741 P1 Growth & Marketing Build Audit v1.0

Date: 2026-09-09

## Scope

This audit records the initial construction of the P1 Growth & Marketing layer derived from the upstream `ericosiu/ai-marketing-skills` catalog and adapted to the 741 provider-neutral architecture.

## Built skills

1. `741-growth-engine`
2. `741-content-quality`
3. `741-seo-intelligence`
4. `741-conversion-intelligence`
5. `741-deck-builder`

Each skill has:
- provider-neutral core logic under `741/core/skills/`
- ChatGPT adapter under `741/adapters/chatgpt/skills/`
- Claude adapter under `741/adapters/claude/skills/`

Cross-skill authority is defined in `741/core/orchestration/P1-GROWTH-MARKETING-CONTRACT.md`.

## Upstream adaptation decisions

### Growth Engine
Converted. Retained hypothesis-driven experimentation and evidence-based learning. Removed upstream telemetry and hard-coded API assumptions. Real observed outcomes are separated from simulated scoring.

### Content Ops
Converted selectively as `741-content-quality`. Retained reusable quality-gate and rubric concepts. Removed the claim that simulated expert personas constitute real expert validation and removed a universal 90+ quality requirement.

### SEO Ops
Converted as `741-seo-intelligence`. Retained search opportunity, decay, competitor-gap and readback concepts. Replaced Ahrefs/GSC/Brave hard dependencies with capability contracts.

### Conversion Ops
Converted as `741-conversion-intelligence`. Retained landing-page/CRO diagnostics and survey insight concepts. Reworked dimensions for B2B logistics and separated heuristic scores from observed conversion data.

### Deck Generator
Converted as `741-deck-builder`. Retained narrative/slide-generation workflow while removing Gemini/Imagen/Google Slides dependency from core. Brand and rendering remain separate authorities/capabilities.

## Explicit non-adoptions

- Finance Ops is not a separate 741 skill because it overlaps WLP Financial Sentinel. Useful analytical methods should be absorbed selectively later.
- Team Ops is not converted wholesale; meeting intelligence may be evaluated separately in P2.
- Personal Strategic Signal Intelligence overlaps Double Loop Personal WLP.
- Autoresearch is deferred to P2 due overlap with Content Quality + Growth Engine.
- Content OS Portable Starter is treated as architecture reference, not a new skill.
- Video/YouTube/shortform/podcast skills are deferred.

## Authority checks

PASS at design level:
- Sales Pipeline remains official WLP prospect-scoring authority.
- Revenue Intelligence remains observed revenue/GP/attribution authority.
- Financial Sentinel remains WLP pricing/financial-policy authority.
- Brand Expert remains WLP brand authority.
- Commercial Partner remains WLP commercial voice authority.
- Org Guardian remains organizational authority.
- Double Loop remains strategic hypothesis/decision-learning authority.

## Safety / truthfulness checks

PASS at design level:
- UNKNOWN preserved.
- Plans and simulated evaluations are not observed events.
- Connected tools do not imply authorization.
- Publishing/sending/launching/writes remain approval-gated.
- Vendor-specific API keys, secrets and telemetry are excluded from 741 core.

## Validation status

`BUILT — NOT YET FUNCTIONALLY VALIDATED`

Required next phase for each skill:

`install → functional test → audit → correct if materially needed → retest → approve`

The five P1 skills must not be labeled VALIDATED until that process is completed in ChatGPT and Claude and a cross-skill integration test passes.
