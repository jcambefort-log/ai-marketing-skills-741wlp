---
name: 741-deck-builder
description: Provider-neutral presentation enablement skill for turning approved evidence and business objectives into structured sales, management, strategy and client decks while keeping narrative ownership separate from brand execution and slide-rendering vendors.
---

# 741 Deck Builder

## Purpose

Create the narrative architecture, slide plan, evidence map and production brief for professional presentations without depending on Google Slides, PowerPoint, Canva, Gemini, Imagen or another specific vendor.

Use for:
- company profiles
- client proposals
- sales decks
- management reviews
- conference presentations
- strategic plans
- warehouse expansion cases
- partner presentations
- commercial enablement

## Core workflow

1. **Define audience and decision**
   - who is the audience?
   - what do they need to understand, believe or decide?
   - what is in/out of scope?

2. **Ingest approved evidence**
   Capture:
   - facts
   - metrics
   - claims
   - sources
   - dates
   - unknowns

3. **Build narrative arc**
   Choose the minimum structure required. Common patterns:
   - context → problem → solution → proof → next step
   - objective → evidence → options → recommendation → decision
   - current state → gap → plan → economics → risks → ask

4. **Create slide architecture**
   For each slide define:
   - purpose
   - title
   - key message
   - supporting evidence
   - recommended visual
   - speaker note / implication when useful

5. **Run evidence gate**
   Do not place unsupported figures, customer claims, projections, market shares, savings, capacity or ROI in a deck as fact.

6. **Brand handoff**
   Deck Builder owns narrative and slide logic. A brand authority owns visual identity, typography, logo use, color, imagery and verbal brand rules.

7. **Production handoff**
   Map the plan to available capabilities:
   - presentation.create
   - image.generate
   - chart.create
   - document.read
   - spreadsheet.read

8. **Review**
   Use Content Quality when a formal quality gate is needed.

## WLP-specific rules

When creating WLP decks:
- current warehouse = approximately 2,800 m² unless newer authorized evidence is supplied
- 3,500–4,000 m² is a relocation target, not current capacity
- WLP Brand Expert owns brand execution
- WLP Financial Sentinel owns financial policy/pricing protection
- 741 Revenue Intelligence owns observed commercial metrics and attribution
- 741 Sales Pipeline owns official prospect scoring
- do not invent client names, network relationships, service volumes or financial projections

## Output schema

```yaml
deck_title: ""
audience: ""
decision_goal: ""
source_evidence: []
unknowns: []
narrative_arc: []
slides:
  - number: 1
    purpose: ""
    title: ""
    key_message: ""
    evidence: []
    visual_brief: ""
    speaker_note: ""
brand_handoff: []
production_requirements: []
quality_gate_required: false
residual_risks: []
```

## Capability contracts

Read:
- `files.read`
- `document.read`
- `spreadsheet.read`
- `analytics.get_pipeline_metrics`
- `brand.read_rules`

Create when authorized:
- `presentation.create`
- `image.generate`
- `chart.create`
- `document.create`

## Approval rules

- A draft deck is not authorization to send or publish it.
- A proposed commercial price or investment figure is not approved merely because it appears in a slide.
- External distribution follows `741/core/policies/ACTION_APPROVAL_POLICY.md`.

## Portability

Presentation rendering, image generation and file formats belong in adapters. The narrative model and evidence discipline remain shared across ChatGPT, Claude and other compatible harnesses.
