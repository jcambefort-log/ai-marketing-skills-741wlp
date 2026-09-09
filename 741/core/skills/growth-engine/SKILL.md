---
name: 741-growth-engine
description: Provider-neutral experimentation and growth-learning engine for designing tests, defining metrics, evaluating results, promoting proven playbook changes, and maintaining an evidence-based improvement loop across marketing and commercial workflows.
---

# 741 Growth Engine

## Purpose

Run disciplined growth experiments without tying the workflow to a specific ad platform, CRM, analytics vendor, email tool, or LLM provider.

Use this skill when WLP or another organization wants to test a measurable commercial or marketing hypothesis, compare variants, evaluate observed results, or decide whether a tested change should be promoted into a playbook.

Do not use this skill as a substitute for ordinary reporting, prospect scoring, revenue attribution, pricing approval, or content drafting.

## Core workflow

1. **Define the decision**
   - What behavior, conversion, response, or commercial outcome are we trying to improve?
   - What decision will be made from the experiment?

2. **State the hypothesis**
   - Write a falsifiable hypothesis.
   - Separate the hypothesis from the expected result.
   - Do not present the hypothesis as fact.

3. **Define experiment scope**
   - channel
   - audience / segment
   - unit of analysis
   - baseline or control
   - variants
   - start/end window
   - inclusion/exclusion criteria
   - owner

4. **Define metrics before launch**
   - one primary metric
   - secondary metrics where useful
   - guardrail metrics
   - minimum sample/data requirement when known
   - decision rule

5. **Check experiment validity**
   Review likely confounders such as:
   - audience changes
   - seasonality
   - list quality
   - sender/domain changes
   - pricing changes
   - service availability
   - tracking changes
   - simultaneous campaigns
   - external events

6. **Prepare experiment plan**
   A plan is not evidence that a test ran.

7. **Read observed results**
   Use real measured data from approved sources. Preserve source, date range, definitions, and missing data.

8. **Evaluate result**
   Possible outcomes:
   - `promote`
   - `keep_testing`
   - `discard`
   - `inconclusive`
   - `invalid_test`

9. **Promote learning carefully**
   A local test result becomes a playbook rule only when the evidence supports repeatability. Never silently rewrite another skill's authority.

10. **Suggest next experiment**
    Prioritize the next highest-value uncertainty instead of generating endless variants.

## Statistical integrity

- Prefer observed outcome data over simulated scoring.
- If statistical significance is calculated, state the method and assumptions.
- Do not invent sample sizes, p-values, confidence intervals, lifts, baselines, or variance.
- Do not treat a directional result as statistically proven.
- Small-sample tests may still inform a decision, but must be labeled low-confidence or inconclusive where appropriate.
- Simulated expert scores belong to pre-launch quality evaluation, not empirical experiment evidence.

## Relationship with other 741 skills

### 741 Outbound Engine
Owns campaign design, research readiness, sequence strategy, deliverability/capacity review, and launch authorization.

Growth Engine may define an outbound experiment around an approved campaign, but it does not launch the campaign itself.

### 741 Revenue Intelligence
Owns observed funnel, pipeline, revenue, GP and attribution analysis.

Growth Engine consumes those observed outcomes as experiment evidence. It must not alter Revenue Intelligence findings.

### 741 Content Quality
May evaluate candidate variants before launch. Its scores are quality judgments, not experiment results.

### 741 Sales Pipeline
Owns official prospect scoring and routing. Experimentation must not silently alter WLP scoring weights or thresholds.

## WLP specialization

Suitable WLP experiments may include:
- regional-hub vs warehouse-first positioning
- country-specific outreach angles
- subject line or CTA tests
- landing-page variants
- logistics-network event follow-up formats
- service-bundle positioning
- case-study vs operational-proof content

WLP pricing rules, commercial approvals, financial floors and official prospect scoring remain under their respective authorities.

## Output schema

```yaml
experiment_name: ""
decision_to_inform: ""
hypothesis: ""
status: planned|running|completed|invalid
channel: ""
audience: ""
control: {}
variants: []
primary_metric: ""
secondary_metrics: []
guardrails: []
measurement_window: ""
data_sources: []
confounders: []
observed_results: []
analysis_method: ""
result: promote|keep_testing|discard|inconclusive|invalid_test
confidence: low|medium|high
playbook_change_recommended: ""
next_experiment: ""
missing_data: []
```

## Capability contracts

Read:
- `analytics.get_campaign_metrics`
- `analytics.get_web_metrics`
- `analytics.compare_periods`
- `crm.search_deals`
- `spreadsheet.read`
- `database.query`
- `files.read`

Optional authorized actions:
- `document.create`
- `spreadsheet.write`
- `analytics.create_experiment_record`

External publishing, campaign launch, CRM mutation, or playbook mutation follows `741/core/policies/ACTION_APPROVAL_POLICY.md`.

## Portability

Keep business logic provider-neutral. Platform-specific analytics, experimentation, CRM, email, publishing, and storage integrations belong in adapters/connectors.
