# PM Routing and Gates

## 1. Product-work size

Assess product impact, not implementation effort.

| Dimension | S | M | L |
|---|---|---|---|
| User impact | One role, one local workflow | Multiple roles or a new end-to-end flow | Many segments, external users, or a new product |
| Business rules | No change | New rules, exceptions, or approvals | Business model, pricing, policy, or multi-party rules |
| Permissions | No change | New role, visibility, or data scope | Permission model or governance redesign |
| Measurement | Existing metrics suffice | New success metric or event plan | New metric system or strategic outcome |
| Strategic impact | Local optimization | Supports a product goal or OKR | New market, product line, or major strategic bet |
| Uncertainty | Known solution | Some discovery and trade-offs needed | Problem or market materially uncertain |
| Coordination | One team | Two or three teams or functions | Multiple teams, partners, or leadership decisions |

### Size rules

- `S`: low product risk, one workflow, reversible, no material business-rule or permission change.
- `M`: a real feature or cross-role workflow with meaningful product choices.
- `L`: new product, new business model, high uncertainty, or major strategic/business impact.

If uncertain, choose the higher size. If the requester wants a smaller path, record the decision and accepted product risk.

## 2. Required product artifacts

| Artifact | S | M | L | Owner |
|---|---|---|---|---|
| Route plan `00-route.md` | Required | Required | Required | PM role |
| Product brief `01-brief.md` | Lean | Full | Full | PM role |
| Product strategy `02-strategy.md` | Optional | Strategy-lite | Required | PM role |
| Experience definition `03-experience.md` | Optional | Required if journeys/rules change | Required | PM role |
| PRD `04-prd.md` | Short PRD | Required | Required | PM role |
| Metrics plan `05-metrics.md` | Optional | Lightweight | Required | PM role |
| Product review `06-review.md` | Checklist | Required | Required | PM role |

An optional artifact may be marked `not-applicable` only with a one-line reason. Absence without a reason is a gap.

## 3. Product gates

### G0 — Intake

Pass when:

- the request is recorded in the requester's own words;
- the affected users, roles, and business context are identified;
- the initial product-work size and owner are known;
- existing documents and evidence have been checked;
- urgent constraints or incidents are identified.

### G1 — Problem and value

Pass when:

- the problem statement describes a user, scenario, and consequence;
- the cost of inaction is stated;
- facts and assumptions are separated;
- at least one non-build option has been considered;
- the recommendation is `go`, `pilot`, `defer`, `reject`, or `needs-discovery`.

### G2 — Product choice and priority

Pass when:

- the target users and outcomes are explicit;
- the product has a stated value proposition;
- alternatives were compared;
- priority and trade-offs are justified;
- MVP, non-goals, and deferred scope are explicit;
- the decision is consistent with the product goal or OKR.

For `S`, this may be captured inside the brief.

### G3 — Experience and business rules

Pass when:

- the end-to-end user journey is defined;
- information architecture and entry points are clear;
- states, permissions, empty/loading/error paths, and recovery are defined where relevant;
- business exceptions and approval rules are explicit;
- admin/back-office requirements have loaded `admin-product-design`;
- acceptance criteria are observable and testable.

### G4 — PRD quality

Pass when:

- every requirement has an ID and can be tested;
- user stories, functional rules, and edge cases are covered;
- scope and non-goals are explicit;
- dependencies and open questions have owners;
- no requirement relies on hidden logic or unstated assumptions;
- the PRD is sufficient for engineering and testing to work independently.

### G5 — Measurement

Pass when:

- at least one primary outcome metric exists;
- leading indicators and guardrails are defined;
- event/instrumentation needs are listed;
- the review date and decision owner are known;
- unknown baselines or targets are marked `TBD` with an owner.

For `S`, an existing dashboard or manual review may be sufficient.

### G6 — Review and handoff

Pass when:

- brief, strategy, experience, PRD, and metrics are internally consistent;
- open questions and risks are visible;
- product review findings are resolved or accepted;
- the handoff package contains all required product inputs;
- engineering and testing can start without asking the PM basic product questions.

## 4. Gate status rules

| Status | Meaning |
|---|---|
| `not-started` | No artifact exists. |
| `in-progress` | Artifact exists but is incomplete. |
| `blocked` | A required decision, input, or skill is missing. |
| `approved` | Required checks pass and the PM role has accepted it. |
| `not-applicable` | The artifact is genuinely unnecessary; record why. |

Never mark a gate `approved` for a document that only contains headings or for a review that was not performed.

## 5. Lean PM path

Use for `S` changes:

1. Lean product brief;
2. Short PRD with acceptance criteria;
3. Product review checklist;
4. Handoff package.

Use the full path when the change introduces:

- a new user journey;
- new business rules or exceptions;
- a new role or permission;
- a new success metric;
- meaningful strategic trade-offs.

## 6. Re-route triggers

Reassess the product path when:

- a new user segment or business model appears;
- a new permission, money, policy, or compliance rule appears;
- evidence contradicts the original problem statement;
- the MVP grows beyond the original outcome;
- leadership changes priority or timeline;
- a dependency invalidates the product choice.

## 7. Out of scope

This routing covers product-manager work only. It does not define:

- architecture, APIs, data models, or technical design;
- test strategy, test cases, or quality gates;
- deployment, monitoring, or rollback execution;
- engineering task breakdown or sprint management.

The handoff package must be clear enough for those activities, but the PM orchestrator does not manage them.