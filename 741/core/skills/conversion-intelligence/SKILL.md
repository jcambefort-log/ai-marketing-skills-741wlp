---
name: 741-conversion-intelligence
description: Provider-neutral conversion intelligence for diagnosing B2B website and landing-page friction, scoring conversion readiness, prioritizing fixes, segmenting survey evidence, and defining measurable conversion tests without relying on one CRO platform.
---

# 741 Conversion Intelligence

## Purpose

Evaluate how effectively a website, landing page, form, or campaign destination converts qualified attention into the next desired business action.

Use for:
- landing-page audits
- website conversion reviews
- RFQ/contact-form friction
- CTA clarity
- trust and proof gaps
- survey segmentation
- lead-magnet opportunity analysis
- pre-launch conversion review
- post-change readback

## Core workflow

1. **Define the conversion objective**
   Examples:
   - RFQ submission
   - contact request
   - meeting request
   - qualified inquiry
   - download
   - newsletter signup

2. **Identify audience and intent**
   Do not judge conversion quality without knowing who the page is for and what they are trying to accomplish.

3. **Evaluate page evidence**
   Suggested B2B dimensions:
   - value proposition clarity
   - service clarity
   - audience relevance
   - CTA clarity
   - trust / proof
   - operational credibility
   - differentiation
   - form friction
   - information scent
   - mobile usability
   - speed / technical friction

4. **Separate heuristic findings from observed behavior**
   A page can score poorly on heuristics yet convert well, or vice versa. Treat analytics as observed evidence and heuristic scores as diagnostic judgments.

5. **Prioritize fixes**
   Rank by:
   - expected impact
   - evidence strength
   - implementation effort
   - risk
   - dependency on other teams/systems

6. **Prepare test plan**
   For material changes, define the test or readback before implementation.

7. **Measure result**
   Use 741 Growth Engine for controlled experiments and 741 Revenue Intelligence for downstream pipeline/revenue evidence where appropriate.

## WLP-specific conversion lens

For WLP, prioritize:
- immediate understanding of Panama / Colón Free Zone positioning
- clarity between freight forwarding and 3PL/warehouse services
- regional redistribution value
- operational proof
- service boundaries
- trust indicators
- ease of requesting an RFQ or commercial conversation
- friction caused by excessive form fields
- mobile usability for international agents and prospects

Do not force consumer-style scarcity, countdowns, fake urgency or aggressive persuasion tactics into logistics B2B pages without a valid business reason.

## Survey / voice-of-customer mode

When survey or interview data is supplied:
- preserve respondent wording when useful
- group recurring pain points
- separate frequency from commercial importance
- do not invent segment size when data is incomplete
- propose content or lead-magnet ideas as hypotheses, not proven demand

## Relationship with other skills

### 741 SEO Intelligence
Owns search opportunity discovery. Conversion Intelligence evaluates what happens after traffic reaches the page.

### 741 Content Quality
Reviews copy/artifact quality.

### 741 Growth Engine
Owns controlled experiment design and promotion of tested changes.

### 741 Revenue Intelligence
Owns observed funnel and revenue outcomes.

### WLP Brand Expert
Owns visual/verbal brand compliance.

## Output schema

```yaml
page_or_asset: ""
objective: ""
audience: ""
observed_data: []
heuristic_dimensions: {}
overall_readiness: low|medium|high
critical_friction: []
trust_gaps: []
proof_gaps: []
form_friction: []
technical_friction: []
recommended_fixes:
  - action: ""
    evidence: ""
    expected_impact: low|medium|high
    effort: low|medium|high
    confidence: low|medium|high
measurement_plan: {}
missing_data: []
```

## Capability contracts

Read:
- `web.fetch`
- `analytics.get_web_metrics`
- `analytics.get_conversion_metrics`
- `files.read`
- `survey.read`
- `cms.read`

Optional draft/write:
- `document.create`
- `cms.create_draft`
- `analytics.create_experiment_record`

Publishing or production changes require appropriate approval.

## Portability

The core does not depend on GA4, Hotjar, Clarity, Optimizely, VWO, HubSpot, Webflow, WordPress or another specific vendor. Connectors implement capabilities.
