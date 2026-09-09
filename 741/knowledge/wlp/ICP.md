# WLP ICP and Scoring Model

Status: WLP Scoring Model v1.0. This is an explainable operational model, not a statistically validated predictive model. Changes to weights or thresholds require management review.

## ICP A: Freight Forwarding / Logistics Agents

### Strong-fit signals
- freight forwarder, NVOCC, logistics agency or international transport company
- needs a reliable Panama/Colón Free Zone partner
- serves Central America, Caribbean and/or South America
- needs bonded storage, consolidation, cross-dock, fulfillment or redistribution
- belongs to an international logistics network or has recurring agent-to-agent business
- has customers needing Panama as a regional hub
- has FCL/LCL/air shipments that can connect with WLP services

### Useful research fields
- country
- cities/offices
- network memberships
- main trade lanes
- ocean/air capabilities
- warehousing capabilities
- industries served
- Panama representation/partner status
- named decision makers
- evidence date/source

## ICP B: Brands / Distributors Needing Regional 3PL

### Strong-fit signals
- distributes physical goods across multiple Latin American/Caribbean markets
- needs regional inventory positioning
- needs bonded warehousing before final-country import
- requires order fulfillment, labeling, kitting, QC or inventory reporting
- wants to reduce fragmented country-by-country inventory or improve regional response time

### Useful research fields
- products/category
- markets served
- regional distribution model
- estimated logistics complexity
- current Panama presence
- fulfillment requirements
- compliance/handling requirements
- evidence date/source

# WLP Scoring Model v1.0

## Rule 1: Score only supported evidence

Every scored dimension must be supported by user-provided information or current authorized evidence. Unknown is not zero and must not be treated as negative evidence.

For each dimension assign:
- `0-10` only when enough evidence exists to score it;
- `unknown` when evidence is insufficient.

The model must list the evidence supporting each score.

## ICP Score

ICP Score measures structural fit, independent of current buying urgency.

Dimensions and fixed weights:

1. Service fit: 30%
2. Geographic/regional fit: 20%
3. Customer-type fit: 20%
4. Relationship/network relevance: 10%
5. Commercial potential: 10%
6. Contact/decision-maker fit: 10%

Calculate the score only across known dimensions and normalize the known weights to 100%.

Formula:

`ICP Score = weighted average of known ICP dimensions, normalized to 0-100`

Always report `ICP evidence coverage`, equal to the percentage of total ICP weight that had enough evidence to score.

Do not present a high ICP score as highly certain when evidence coverage is low.

## Intent Score

Intent Score measures evidence that the prospect is actively evaluating, requesting or preparing to use relevant services.

Dimensions and fixed weights:

1. Explicit active need / partner search / RFQ: 35%
2. Need specificity: 20%
3. Timing / urgency: 15%
4. Recent engagement or commercial activity: 10%
5. Trigger event: 10%
6. Project / shipment / implementation evidence: 10%

Calculate only across known dimensions and normalize known weights to 100%.

Always report `Intent evidence coverage`.

Examples of strong intent evidence include an explicit partner search, RFQ, active project, shipment requirement, stated implementation date, recent quote activity, or direct request for WLP-relevant capabilities.

## Relationship / Network Score

This is kept separate from ICP so network proximity can influence prioritization without distorting structural fit.

Score 0-100 when evidence exists using:
- existing relationship with WLP
- relevant logistics-network membership
- referral or warm introduction
- prior quote/opportunity/customer history
- known agent-to-agent relationship

If there is no evidence, mark `unknown`; do not assume zero.

## Commercial Potential Score

Score 0-100 only when there is evidence of likely economic value, such as:
- shipment frequency
- FCL/LCL/air volume
- warehouse volume / pallets / SKUs
- number of markets served
- breadth of required WLP services
- recurring vs one-off need
- authorized historical revenue/margin information

If these inputs are unavailable, mark `unknown`.

## Timing Score

Score 0-100 based on known implementation urgency:
- 90-100: immediate / active RFQ / shipment or implementation imminent
- 70-89: within roughly 30 days or clearly active project
- 50-69: within roughly 31-90 days
- 25-49: later than 90 days but stated initiative exists
- 0-24: no near-term initiative supported by evidence
- unknown: no timing evidence

## Priority Score

Priority is calculated from five components with fixed weights:

- ICP Score: 35%
- Intent Score: 30%
- Relationship / Network Score: 10%
- Commercial Potential Score: 15%
- Timing Score: 10%

Formula:

`Priority Score = weighted average of known components, normalized to 0-100`

A component marked `unknown` is excluded and remaining known weights are normalized. Always report `Priority evidence coverage`, equal to the sum of original component weights with known scores.

Do not silently substitute another formula.

## Priority bands

- `P1 CRITICAL`: 85-100, with Priority evidence coverage >= 70%
- `P2 HIGH`: 70-84
- `P3 MEDIUM`: 50-69
- `P4 LOW`: 0-49
- `REVIEW`: score cannot be relied upon because Priority evidence coverage < 40% or material identity/suppression questions remain
- `DISQUALIFIED`: explicit evidence of no plausible WLP fit or incompatible requirements
- `SUPPRESSED`: contact/action should not proceed because an applicable suppression condition is confirmed

If score is >=85 but evidence coverage is below 70%, label `P2 HIGH - provisional` rather than P1.

## Confidence

Confidence is not another commercial score. It represents evidence completeness and reliability.

Use:
- `high`: >=80% evidence coverage, sources are current and prospect identity is sufficiently resolved
- `medium`: 50-79% evidence coverage or some material fields are unknown
- `low`: <50% evidence coverage, stale/weak evidence, or unresolved identity

Do not invent a numeric confidence percentage unless a future approved model defines one.

## Qualification states

Use one of:
- `qualified`
- `review`
- `disqualified`
- `suppressed`

A high fit score alone does not clear suppression checks.

## Disqualification / review flags

- no plausible need for WLP services
- geography outside strategic scope with no Panama/regional connection
- direct conflict/duplicate ownership in active pipeline
- existing customer already handled by another owner
- explicit do-not-contact/opt-out
- unsupported or stale company information
- requirements WLP cannot currently provide
- prospect identity is not sufficiently resolved for external action

## Suppression checks

Before external outreach, check when data is available:
- existing customer
- active opportunity / ownership
- prior or recent outreach
- duplicate contact/company
- explicit opt-out / do-not-contact
- supplied blocklist/compliance restrictions

Unknown checks must remain `unknown`. Do not convert unknown into `clear` or `suppressed`.

## Learning loop

Periodically compare:
- qualified vs rejected leads
- quotes won vs lost
- opportunity velocity
- service mix
- margin/revenue quality when authorized data is available
- geography
- customer type
- source/network

Recommend changes to weights or thresholds, but require management review before changing this model or qualification rules used for automated routing.
