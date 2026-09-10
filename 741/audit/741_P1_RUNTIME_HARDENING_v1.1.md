# 741 P1 Runtime Hardening Audit v1.1

## Trigger

Claude installed-runtime validation exposed three portability/hardening issues after the initial P1 repository validation:

1. Growth Engine had no formal result state for planned/running experiments that have not yet been evaluated.
2. Content Quality did not explicitly require detection of unsupported prevalence/generalization language such as `many`, `most`, `often`, or equivalent wording.
3. Deck Builder needed stronger provenance controls for network memberships, relationships, channel commitments, and commercial-policy claims.

## Changes

### 741 Growth Engine

- Added `not_evaluated` to the formal result enum.
- Added lifecycle rules:
  - planned → `not_evaluated`
  - running without final evidence → `not_evaluated`
  - completed → evaluable result only when observed evidence exists
  - invalid → `invalid_test`
- Added rule not to state `experiments completed = 0` unless an authoritative source establishes zero.
- Added equivalent ChatGPT and Claude adapter instructions.

### 741 Content Quality

- Added unsupported quantifiers/generalizations to factual-integrity checks.
- Added evidence-neutral rewrite guidance.
- Added equivalent ChatGPT and Claude adapter instructions.

### 741 Deck Builder

- Added material-claim provenance gate.
- Added explicit controls for memberships, network relationships, channel commitments, exclusivity, reciprocity, agent protection, customer ownership, and other commercial-policy claims.
- Added WLP Commercial Partner handoff for unsupported commercial conventions.
- Added equivalent ChatGPT and Claude adapter instructions.

## Authority checks

- Sales Pipeline scoring authority unchanged.
- Outbound readiness/authorization authority unchanged.
- Revenue Intelligence authority over observed revenue/GP/attribution unchanged.
- Financial Sentinel authority unchanged.
- Brand Expert authority unchanged.
- Commercial Partner authority strengthened for commercial-policy claims.
- UNKNOWN preservation unchanged.
- External action approval boundaries unchanged.

## Status

`HARDENED — RUNTIME RETEST REQUIRED`

Required retest:

1. Claude: Growth Engine must return `result: not_evaluated` for a planned experiment.
2. Claude: Content Quality must flag or neutralize unsupported prevalence language such as `many freight forwarders...` when no evidence supports prevalence.
3. Claude: Deck Builder must omit or mark `VERIFY BEFORE USE` for memberships/commercial-policy claims without current authorized provenance.
4. ChatGPT: short regression test for the same three controls.

Do not merge this hardening branch into `741-portable-skills` until the targeted runtime retests pass.
