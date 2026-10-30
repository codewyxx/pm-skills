# Artifact Contract

## Directory layout

Use one folder per feature:

```text
docs/delivery/<feature-slug>/
├── 00-route.md
├── 01-brief.md
├── 02-prd.md
├── 03-ux-flow.md
├── 04-solution-design.md
├── 05-test-design.md
├── 06-delivery-plan.md
├── 07-launch-readiness.md
└── adr/
    ├── ADR-001-<decision>.md
    └── ADR-002-<decision>.md
```

Only create files required by the route. Use `not-applicable` in the route plan when a file is intentionally omitted; do not leave a silent gap.

## Artifact metadata

Every artifact starts with:

```yaml
---
artifact: brief | prd | ux-flow | solution-design | test-design | delivery-plan | launch-readiness
feature: FEAT-001
status: draft | review | approved | blocked
owner: {name}
reviewers:
  - product
  - ux
  - engineering
  - qa
  - ops
upstream:
  - path/to/previous-artifact.md
last_updated: YYYY-MM-DD
---
```

## Identifier scheme

| Prefix | Use |
|---|---|
| `FEAT-*` | Feature or change |
| `REQ-*` | Testable requirement |
| `UX-*` | Flow, state, or interaction requirement |
| `DES-*` | Technical design element |
| `TEST-*` | Test scenario |
| `TASK-*` | Delivery task |
| `RISK-*` | Risk |
| `ADR-*` | Architecture decision |

## Traceability matrix

The final plan must include or generate a matrix:

| Requirement | UX | Design | Test | Task | Status |
|---|---|---|---|---|---|
| REQ-001 | UX-001 | DES-001 | TEST-001 | TASK-001 | covered |

Rules:

- Every applicable `REQ-*` maps to at least one `DES-*` and one `TEST-*`.
- Every `TEST-*` maps back to a requirement or an explicit risk.
- Every `TASK-*` maps to a design element or test scenario.
- A gap is either fixed or recorded as an accepted risk with an owner.

## Handoff package

A stage handoff must include:

1. artifact path and status;
2. decisions made;
3. assumptions still in force;
4. open questions and owners;
5. risks introduced or retired;
6. next skill and expected output;
7. gate verdict.

## Fallback minimums when a future skill is unavailable

### Technical design fallback

At minimum document:

- components and responsibilities;
- interfaces and data model;
- state/permission impact;
- failure, retry, idempotency, and concurrency behavior;
- security/privacy, observability, performance, migration, rollout, and rollback;
- alternatives and ADRs.

### Test design fallback

At minimum document:

- scope and risks;
- requirement-to-test traceability;
- normal, boundary, negative, permission, state, concurrency, idempotency, async, and export scenarios;
- test data and environment needs;
- automation boundaries;
- entry/exit and regression criteria.

### Delivery plan fallback

At minimum document:

- dev/test/environment/release tasks;
- dependencies and owners;
- critical path and risks;
- milestones and review gates;
- monitoring, rollback, and post-release verification.

A fallback artifact keeps the gate open until it is reviewed. It is not automatically `approved`.