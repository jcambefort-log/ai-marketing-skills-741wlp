# 741 Action Approval Policy

## Principle

Access to a system is not permission to perform every action in that system.

## Action classes

### A. Read / Analyze
Examples: search, retrieve, inspect, calculate, compare, summarize.

Default: may proceed when the user request authorizes the relevant data access and the platform/tool permits it.

### B. Create Draft / Preview
Examples: email draft, proposal draft, campaign draft, CMS draft, social draft, edit plan.

Default: may create a reversible draft when requested. Creating a draft does not authorize sending or publishing it.

### C. External Write
Examples: update CRM fields, create a record, add a note, modify campaign configuration, upload approved content.

Default: require clear user intent for the write. Verify result after execution when possible.

### D. Send / Publish / Launch
Examples: send email, publish social content, publish CMS page, launch campaign, send outreach sequence.

Default: require explicit approval unless the user has deliberately configured that exact workflow for autonomous execution.

### E. Destructive / High-impact Mutation
Examples: delete records, overwrite source data, cancel campaigns, bulk modify contacts, revoke access.

Default: require explicit approval and confirmation of scope. Prefer reversible alternatives.

## Separation of permissions

The following are separate permissions and must not be inferred from one another:

- read
- analyze
- draft
- write
- send
- publish
- launch
- delete

## Fail-closed conditions

Do not execute a mutation when:

- target identity is ambiguous
- authorization is unclear
- required connector is unavailable
- authentication is unhealthy
- source data is materially stale for the requested decision
- action scope is broader than requested
- a required human approval gate has not been satisfied

## Auditability

For consequential workflows, preserve enough information to identify:

- requested action
- source data used
- capability/connector used
- approval state
- resulting action/status
- failures or unresolved uncertainty
