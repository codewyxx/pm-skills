# PM Artifact Contract

## Directory layout

Use one folder per product feature or initiative:

```text
docs/product/<feature-slug>/
├── 00-route.md
├── 01-brief.md
├── 02-strategy.md
├── 03-experience.md
├── 04-prd.md
├── 05-metrics.md
└── 06-review.md
```

Only create files required by the route. Use `not-applicable` in the route plan when a file is intentionally omitted; do not leave a silent gap.

## Artifact metadata

Every artifact starts with:

```yaml
---
artifact: route | brief | strategy | experience | prd | metrics | review
feature: FEAT-001
status: draft | review | approved | blocked
owner: {name}
reviewers:
  - problem
  - user-value
  - scope-priority
  - experience-rules
  - measurement
  - stakeholder-handoff
upstream:
  - path/to/previous-artifact.md
last_updated: YYYY-MM-DD
---
```

## Identifier scheme

| Prefix | Use |
|---|---|
| `FEAT-*` | Feature or product initiative |
| `REQ-*` | Testable product requirement |
| `UX-*` | Journey, flow, state, or interaction rule |
| `RULE-*` | Business rule or exception |
| `METRIC-*` | Success metric, guardrail, or instrumentation need |
| `DEC-*` | Product decision |
| `RISK-*` | Product, user, business, or compliance risk |
| `OPEN-*` | Open question |
| `ASSUME-*` | Assumption requiring validation |

## Traceability

The review artifact must contain:

| Requirement | User / outcome | Experience / rule | Metric | Decision | Status |
|---|---|---|---|---|---|
| REQ-001 |  | UX-001 / RULE-001 | METRIC-001 | DEC-001 | covered |

Rules:

- Every `REQ-*` maps to a user outcome and at least one experience or business-rule element.
- Every business rule that changes behavior maps to a requirement.
- Every requirement has an acceptance criterion.
- Every success metric has an owner and review date.
- Every unresolved assumption or question has an owner.
- Any gap is either fixed or recorded as an accepted risk with a decision owner.

## Handoff package

A PM handoff to engineering and testing must include:

1. artifact paths and status;
2. target users, problem, and expected outcome;
3. scope, non-goals, MVP, and priority;
4. end-to-end flows, states, permissions, and business rules;
5. testable acceptance criteria;
6. success metrics and instrumentation needs;
7. assumptions, risks, open questions, and owners;
8. decisions made and alternatives rejected;
9. review verdict and remaining constraints.

The handoff must not include engineering task breakdown, technical architecture, test-case design, or release execution unless the PM has a separate responsibility for them.

## Fallback minimums when a future skill is unavailable

### Product strategy fallback

At minimum document:

- target users and problem;
- value proposition;
- alternatives, including not building;
- priority and trade-offs;
- MVP, non-goals, and success conditions;
- strategic fit and key risks.

### Product experience fallback

At minimum document:

- end-to-end user journey;
- entry points and information architecture;
- key states, permissions, exceptions, empty/loading/error paths;
- business rules and configurable versus fixed behavior;
- acceptance criteria candidates.

### Metrics fallback

At minimum document:

- primary outcome metric;
- leading indicator;
- guardrails;
- baseline, target, timeframe, and data source, or `TBD` with owner;
- instrumentation events;
- post-launch review date.

### Product review fallback

At minimum verify:

- problem and solution are connected;
- scope and non-goals are explicit;
- every requirement is testable;
- states, permissions, exceptions, and edge cases are covered;
- metrics are measurable;
- open questions and risks have owners;
- the handoff is executable without the PM present.

A fallback artifact keeps the gate open until reviewed. It is not automatically `approved`.