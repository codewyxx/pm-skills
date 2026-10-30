# Product Brief Quality Gate

## Gate outcome

Return exactly one status:

| Status | Meaning | Next action |
|---|---|---|
| `ready-for-prd` | The brief is specific enough to expand into a PRD. | Hand off to `prd`. |
| `needs-clarification` | A missing answer changes value, scope, risk, or acceptance. | Ask at most 3 questions. |
| `needs-discovery` | The problem, user, or evidence is too weak to justify a solution. | Propose a discovery or validation step. |
| `deferred` | The value is real but timing, dependency, or cost makes now the wrong time. | State revisit trigger. |
| `rejected` | The request does not solve a meaningful problem, or a simpler option is clearly better. | Explain the alternative. |

## Required checks

### Problem

- [ ] The problem statement describes a user, situation, and consequence.
- [ ] It does not smuggle in a predetermined feature.
- [ ] The cost of inaction is stated.
- [ ] Facts and assumptions are separated.

### User and value

- [ ] The target role or segment is concrete.
- [ ] The scenario can be observed or described end to end.
- [ ] The desired outcome is business or user value, not an output.
- [ ] At least one option other than building software was considered.

### Scope

- [ ] `In scope` is explicit.
- [ ] `Out of scope` is explicit.
- [ ] MVP is the smallest outcome that delivers value.
- [ ] Deferred items are intentional, not missing.

### Success

- [ ] At least one primary outcome metric exists.
- [ ] A leading indicator or early signal is proposed.
- [ ] Guardrails state what must not get worse.
- [ ] Unknown baseline or target is marked `TBD` with an owner.

### Risk and readiness

- [ ] Dependencies have owners.
- [ ] Major risks have impact and mitigation.
- [ ] Critical assumptions have a validation method.
- [ ] The recommendation is one of `go`, `pilot`, `defer`, `reject`, or `needs-discovery`.
- [ ] The next skill is named.

## Non-PM safety rules

- If the requester cannot answer a question, propose a default and label it as an assumption.
- Never invent a baseline, target, market fact, or legal requirement.
- If the request is actually a bug, incident, or compliance obligation, route to the correct process instead of forcing a product brief.
- A brief may be approved with open questions only when they do not change the MVP, risk, or acceptance criteria.

## Handoff package

The handoff to `prd` must contain:

- `FEAT-*` and `REQ-*` identifiers;
- problem statement;
- target users and scenarios;
- MVP and non-goals;
- success metrics and guardrails;
- assumptions and open questions;
- decision and recommendation.

If a required field is blank, mark the brief `needs-clarification`; do not silently fill it.