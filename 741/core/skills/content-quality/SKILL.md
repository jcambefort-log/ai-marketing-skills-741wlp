---
name: 741-content-quality
description: Provider-neutral quality-gate skill for evaluating and improving commercial, marketing, web, proposal, presentation and strategy content with explicit rubrics, evidence checks, brand handoffs and honest scoring.
---

# 741 Content Quality

## Purpose

Provide a reusable quality gate for content and commercial artifacts without pretending simulated reviewers are real people or treating subjective scores as empirical performance evidence.

Use for:
- outreach drafts
- landing-page copy
- website content
- proposals
- presentations
- social posts
- email sequences
- strategy documents
- sales enablement material

## Core workflow

1. **Identify the artifact**
   - content type
   - intended audience
   - objective
   - channel
   - source skill if applicable

2. **Separate evidence from claims**
   Flag:
   - unsupported numbers
   - unsupported quantifiers or prevalence claims such as `many`, `most`, `leading`, `often`, `typically`, `commonly`, or equivalent language unless evidence supports them
   - invented customer facts
   - invented relationships or memberships
   - unverified performance claims
   - stale facts
   - claims requiring current research

   Rephrase unsupported generalizations into evidence-neutral language when possible. Example: replace `Many freight forwarders need...` with `For freight forwarders that need...` unless current evidence supports the prevalence claim.

3. **Select an explicit rubric**
   Choose dimensions appropriate to the artifact. Typical dimensions:
   - factual integrity
   - clarity
   - relevance
   - differentiation
   - credibility
   - audience fit
   - action clarity
   - readability
   - consistency
   - compliance / risk

4. **Brand handoff**
   Brand compliance is not owned by this skill. When a brand authority exists, consume its rules and report brand compliance separately.

5. **Score honestly**
   Scores are evaluation judgments, not market outcomes. Explain the rubric and the reasons for material deductions.

6. **Revise**
   Fix the highest-impact weaknesses first. Do not optimize wording at the expense of factual integrity.

7. **Re-score**
   Maximum three revision rounds unless the user asks otherwise.

8. **Return a quality decision**
   - `ready_for_review`
   - `needs_revision`
   - `blocked_by_missing_evidence`

## Scoring rules

- Default score range: 0–100.
- A score is only meaningful relative to the stated rubric.
- Do not fabricate a universal 90+ quality standard.
- Do not present simulated panel agreement as real expert validation.
- Do not convert subjective quality scores into predicted reply rate, conversion rate, revenue, or ROI.
- If evidence is missing for a central claim, factual-integrity deductions take precedence over persuasive polish.
- Unsupported prevalence/generalization language is a factual-integrity issue even when no explicit number is present.

## Suggested default rubric

For general B2B commercial content:

```yaml
factual_integrity: 25
clarity: 15
audience_relevance: 15
credibility: 10
differentiation: 10
value_clarity: 10
action_clarity: 5
readability: 5
consistency: 5
```

Weights may be adapted to content type, but the chosen rubric must be shown or explainable.

## Relationship with WLP authorities

### WLP Commercial Partner
Owns WLP commercial voice and communication conventions.

### WLP Brand Expert
Owns WLP visual/verbal brand rules. Content Quality consumes those rules; it does not replace them.

### 741 Outbound Engine
Owns outbound sequence strategy and campaign authorization. Content Quality may review drafts from Outbound Engine.

### 741 Growth Engine
Owns real-world experimentation. Content Quality scores are pre-launch judgments only.

### 741 Deck Builder
Owns presentation narrative/assembly. Content Quality may quality-check the resulting content.

## WLP-specific checks

When working in WLP mode, pay special attention to:
- current vs target warehouse capacity
- Colón Free Zone / bonded positioning
- service claims
- geographic claims
- network membership claims
- client logos or testimonials
- pricing language
- operational proof
- freight volumes and savings claims
- unsupported prevalence/generalization language about forwarders, customers, routes, markets, or industry behavior

UNKNOWN remains UNKNOWN.

## Output schema

```yaml
artifact: ""
content_type: ""
objective: ""
audience: ""
rubric: {}
claim_issues: []
brand_authority_required: false
rounds:
  - round: 1
    score: null
    dimension_scores: {}
    top_weaknesses: []
    changes_made: []
final_score: null
quality_state: ready_for_review|needs_revision|blocked_by_missing_evidence
residual_risks: []
source_skill_feedback: []
```

## Capability contracts

Read:
- `files.read`
- `web.search`
- `brand.read_rules`
- `company.research`

Draft:
- `document.create`
- `document.revise`

Publishing or sending follows the action approval policy.

## Portability

Rubrics and reasoning are provider-neutral. Model-specific evaluation calls, document editors, CMS, email and publishing systems belong in adapters/connectors.
