---
name: 741-seo-intelligence
description: Provider-neutral SEO/AEO/GEO intelligence for keyword opportunity discovery, competitor-gap analysis, content decay detection, search-performance readback and prioritized website growth recommendations without hard-coding one analytics or SEO vendor.
---

# 741 SEO Intelligence

## Purpose

Turn search-performance evidence, website content, competitor signals and topic demand into prioritized SEO/AEO/GEO opportunities.

Use for:
- keyword research
- search-performance analysis
- competitor content gaps
- striking-distance opportunities
- decaying content
- content briefs
- trend relevance
- answer-engine / AI-search visibility
- post-change readback

## Core workflow

1. **Define business objective**
   Clarify which services, markets, geographies, customer segments or conversion goals matter.

2. **Ingest current evidence**
   Possible sources:
   - search console data
   - web analytics
   - ranking tools
   - website pages
   - competitor pages
   - backlinks
   - trend sources
   - AI-search visibility observations

3. **Normalize search concepts**
   For each query/topic capture when available:
   - query/topic
   - intent
   - geography
   - current position
   - impressions
   - clicks
   - CTR
   - volume estimate
   - difficulty estimate
   - conversion relevance
   - freshness
   - source/date

4. **Identify opportunity types**
   - striking distance
   - competitor gap
   - missing service page
   - decaying page
   - weak CTR
   - weak conversion alignment
   - trend opportunity
   - AEO/GEO answer gap

5. **Prioritize**
   Prioritization must use observed inputs. Do not invent traffic, CPC, ranking difficulty or commercial intent scores.

6. **Prepare content/technical brief**
   Separate:
   - content recommendation
   - technical recommendation
   - internal linking
   - proof/evidence needed
   - CTA/conversion dependency

7. **Read back after change**
   Define baseline and candidate windows before judging success.

8. **Decision**
   - `promote`
   - `keep_testing`
   - `rollback`
   - `unproven`

## Evidence rules

- Vendor estimates are estimates, not observed WLP traffic.
- Search volume, keyword difficulty and CPC must retain source/provider context.
- Do not infer a competitor's revenue or lead volume from ranking data.
- Do not claim causality from ranking movement alone.
- Track confounders: seasonality, indexing lag, campaigns, tracking changes, site migrations and unrelated edits.

## WLP specialization

SEO Intelligence may investigate themes such as:
- bonded warehousing in Panama
- Colón Free Zone logistics
- 3PL Panama
- regional distribution hub
- FCL/LCL consolidation
- fulfillment in Panama
- Central America / Caribbean distribution

These are candidate themes, not automatically approved target keywords. Evidence determines priority.

## Relationship with other skills

### 741 Conversion Intelligence
Consumes traffic/page opportunities and evaluates conversion effectiveness.

### 741 Content Quality
Reviews resulting briefs and content drafts for quality and factual integrity.

### WLP Commercial Partner
Owns WLP commercial narrative and messaging conventions.

### WLP Brand Expert
Owns brand execution.

### 741 Growth Engine
Owns real-world experiments on SEO/content changes when structured testing is appropriate.

### 741 Revenue Intelligence
Owns observed pipeline/revenue attribution analysis.

## Output schema

```yaml
objective: ""
market: ""
data_sources: []
search_opportunities:
  - topic: ""
    intent: ""
    evidence: []
    opportunity_type: ""
    priority: ""
    confidence: low|medium|high
content_gaps: []
technical_findings: []
competitor_gaps: []
decay_alerts: []
aeo_geo_findings: []
recommended_actions: []
measurement_plan: {}
missing_data: []
```

## Capability contracts

- `search_console.read`
- `analytics.get_web_metrics`
- `seo.get_rankings`
- `seo.get_keyword_metrics`
- `seo.get_backlinks`
- `web.search`
- `web.fetch`
- `files.read`
- `cms.read`

Optional authorized writes:
- `document.create`
- `cms.create_draft`

Publishing follows the approval policy.

## Portability

Google Search Console, Ahrefs, Semrush, Moz, Bing Webmaster Tools and other providers are interchangeable implementations of capabilities, not hard-coded dependencies.
