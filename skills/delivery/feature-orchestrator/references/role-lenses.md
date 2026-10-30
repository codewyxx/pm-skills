# Role Lenses

A single person may hold several roles. Change hats explicitly and record findings for each lens. Do not let one lens approve the work of another without review.

## Product lens

Ask:

- Who has the problem, in what scenario?
- What is the current workaround and its cost?
- What outcome changes for the user or business?
- Why now, and what happens if we do nothing?
- What is the MVP, and what is explicitly out of scope?
- What metric proves success, and what guardrail prevents harm?
- What alternatives exist, including manual process, purchase, or deferral?

Output:

- brief quality verdict;
- missing product decisions;
- metric and scope risks;
- recommendation: go / pilot / defer / reject / needs-discovery.

## UX lens

Ask:

- What is the end-to-end journey before, during, and after the feature?
- What are the entry points, permissions, states, empty states, loading states, errors, and recovery paths?
- What happens in bulk, async, failure, retry, and partial-success cases?
- Is information architecture still coherent?
- Are high-frequency actions efficient and destructive actions safe?
- Is the interface accessible and consistent with existing patterns?

For admin features, load the relevant `admin-product-design` references.

Output:

- missing flows and states;
- interaction risks;
- copy and accessibility concerns;
- UX artifact status.

## Engineering lens

Ask:

- What components, data stores, APIs, events, jobs, and external dependencies change?
- What is the source of truth and ownership boundary?
- What are the failure modes, retries, idempotency, concurrency, and consistency requirements?
- What are the performance, capacity, availability, security, privacy, and observability requirements?
- Is there a migration, compatibility, rollout, or rollback concern?
- What is the simplest viable design, and what alternatives were rejected?
- Which requirements have no design mapping?

Output:

- solution-design artifact;
- ADR list;
- unresolved technical risks;
- design gate verdict.

## QA lens

Ask:

- Which requirements are risky or ambiguous?
- What can fail at boundaries, permissions, state transitions, concurrency, retries, and partial success?
- What must be verified at unit, API, integration, UI, and end-to-end levels?
- What test data, accounts, environments, and service doubles are needed?
- What is automated, what is manual, and what is exploratory?
- What are the entry, exit, regression, and release criteria?
- What evidence proves the feature works?

Output:

- test-design artifact;
- traceability matrix `REQ-*` -> `TEST-*`;
- environment and data readiness;
- test gate verdict.

## Ops / SRE lens

Ask:

- How is the feature deployed, configured, and monitored?
- What are the SLIs, alerts, dashboards, and logs?
- What is the rollback, kill switch, or feature-flag plan?
- Who is on call and who supports users?
- What happens during dependency failure or traffic spikes?
- How will we know the launch succeeded or failed?

Output:

- launch-readiness checklist;
- observability and rollback gaps;
- operational ownership;
- launch gate verdict.

## Self-review rule

When acting alone:

1. Review as Product.
2. Review as UX.
3. Review as Engineering.
4. Review as QA.
5. Review as Ops.

For each lens, write at least one of:

- a blocking finding;
- a non-blocking risk;
- `no findings` with the evidence checked.

A single review cannot silently stand in for all five lenses.