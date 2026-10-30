# Routing and Gates

## 1. Change-size classification

Score each dimension. Any high-risk dimension forces at least `M`; two or more force `L`.

| Dimension | S | M | L |
|---|---|---|---|
| Users / roles | One role, one workflow | Two or three roles or a new workflow | Many roles, external users, or cross-organization |
| Systems | One component | Two or three systems or a new API | Many systems, shared platform, or external dependencies |
| Data | No schema change | New fields, indexes, or a bounded migration | Destructive migration, backfill, or cross-system consistency |
| Permissions | No permission change | New role or permission point | Permission model redesign or cross-tenant data |
| Money / security / compliance | None | Limited exposure | Funds, personal data, audit, regulatory, or irreversible action |
| Reversibility | Easy rollback | Rollback needs a written plan | Hard or impossible rollback |
| Uncertainty | Known solution | Some discovery needed | Problem or solution materially uncertain |
| Delivery | Days, one team | Weeks, one or two teams | Multi-week, multiple teams, staged rollout |

### Size rules

- `S`: one team, low risk, reversible, no data/permission/finance/security impact.
- `M`: new feature or meaningful change with some cross-system, role, data, or UX impact.
- `L`: high uncertainty, high risk, migration, cross-team dependency, or launch-critical change.

If uncertain, choose the higher size. If the user insists on a smaller path, record the decision and accepted risk in the route plan.

## 2. Required artifact matrix

| Artifact | S | M | L | Owner |
|---|---|---|---|---|
| Route plan `00-route.md` | Required | Required | Required | Request owner |
| Product brief `01-brief.md` | Lean | Full | Full | Product lens |
| PRD `02-prd.md` | Optional | Required | Required | Product lens |
| UX flow `03-ux-flow.md` | Optional | Required if UI | Required | UX lens |
| Technical design `04-solution-design.md` | Optional | Required | Required | Engineering lens |
| Test design `05-test-design.md` | Test notes | Required | Required | QA lens |
| Delivery plan `06-delivery-plan.md` | Release notes | Required | Required | Delivery owner |
| Launch readiness `07-launch-readiness.md` | Checklist | Checklist | Full review | Ops lens |
| ADR `adr/` | Not needed | When a material choice exists | Required for major choices | Engineering lens |
| Migration / rollback | Not needed | When data changes | Required | Engineering + Ops |

For `S`, combine artifacts into the Lean Brief where possible. Do not create ceremony without risk.

## 3. Gates

### G0 — Intake

Pass when:

- the request is stated in the requester's own words;
- the affected users and business context are known;
- initial size is recorded;
- the owner and target timeframe are known;
- urgent constraints or incidents are identified.

### G1 — Brief

Pass when:

- the problem, user, scenario, and cost of inaction are clear;
- MVP, non-goals, metrics, and guardrails exist;
- alternatives include not building;
- assumptions and open questions are labeled;
- the recommendation is explicit.

### G2 — Product / UX design

Pass when:

- requirements have stable `REQ-*` identifiers;
- user journeys and edge states are defined;
- permissions, state transitions, empty/loading/error states, and accessibility considerations are defined where relevant;
- acceptance criteria are observable and testable;
- admin/back-office features have loaded `admin-product-design`.

### G3 — Technical design

Pass when:

- components, interfaces, data model, and ownership are defined;
- failure modes, idempotency, concurrency, and retry behavior are defined where relevant;
- security, privacy, observability, performance, and capacity are addressed;
- migration, compatibility, rollout, and rollback are defined when needed;
- key decisions have ADRs;
- every applicable requirement maps to a design element.

### G4 — Test design

Pass when:

- test scope and risk priorities are defined;
- every `REQ-*` maps to at least one `TEST-*`;
- state, permission, boundary, negative, concurrency, idempotency, async, and export cases are covered where relevant;
- test data and environments are defined;
- automation boundaries and manual checks are explicit;
- entry and exit criteria are defined.

### G5 — Delivery plan

Pass when:

- development, test, environment, and release tasks are sequenced;
- owners, dependencies, and critical path are known;
- risks and buffers are recorded;
- rollback, monitoring, and post-release verification are planned;
- the plan is detailed enough for `writing-plans` to create task-level steps.

### G6 — Launch readiness

Pass when:

- monitoring and alerting are live;
- rollback or kill switch is tested;
- support and on-call ownership are defined;
- user-facing documentation or communication exists;
- success metrics and review date are scheduled;
- known limitations and follow-up work are documented.

## 4. Gate status rules

| Status | Meaning |
|---|---|
| `not-started` | No artifact exists. |
| `in-progress` | Artifact exists but is incomplete. |
| `blocked` | A required input, decision, or skill is missing. |
| `approved` | Required checks pass and owner has accepted it. |
| `not-applicable` | The artifact is genuinely unnecessary for this change; record why. |

Do not use `approved` for a document that only contains headings or for a gate whose required checks were skipped.

## 5. Fast path

A hotfix may use a compressed path:

1. record the incident and immediate risk;
2. define the rollback trigger;
3. implement the smallest safe fix;
4. run targeted regression and monitoring;
5. create a retrospective brief and follow-up test coverage.

The fast path never authorizes a high-risk data, permission, or financial change without the relevant design gate.