# PM Lenses

A single person may perform all PM work. Change hats explicitly and record findings for each lens. Do not let one lens silently substitute for another.

## Problem lens

Ask:

- What is the original request, and what underlying problem does it represent?
- Who experiences the problem, in what situation?
- What happens today, and what does the workaround cost?
- Why now? What happens if we do nothing?
- Is this a problem, a solution proposal, a compliance obligation, or a bug?
- Which facts are confirmed and which are assumptions?

Output:

- problem statement quality;
- missing evidence;
- cost of inaction;
- recommendation: go / pilot / defer / reject / needs-discovery.

## User and value lens

Ask:

- Which user roles or segments are affected?
- What outcome does each role need?
- Which user gains the most value, and which users may be harmed?
- What is the value proposition for the user and the business?
- Is the request solving a high-frequency, high-cost, or high-risk problem?
- What alternative exists, including manual process, purchase, or no change?

Output:

- target users and scenarios;
- value hypotheses;
- disconfirmed or weak assumptions;
- open questions for users or business owners.

## Scope and priority lens

Ask:

- What is the smallest outcome that delivers real value?
- What is explicitly out of scope?
- Which requirements are must-have, should-have, or later?
- What are the trade-offs between value, effort, risk, and time?
- Why is this more important than competing requests?
- What would make us stop or defer the work?

Output:

- MVP and non-goals;
- priority rationale;
- scope risks;
- deferred decisions with revisit triggers.

## Experience and business-rule lens

Ask:

- What is the end-to-end journey before, during, and after the feature?
- What are the entry points, roles, permissions, and data visibility rules?
- Which states, transitions, exceptions, and approvals exist?
- What do empty, loading, error, partial-success, and no-permission states look like?
- What business rules are non-negotiable, and which are configurable?
- What would make the flow confusing or unsafe?
- Does the feature need the domain references in `admin-product-design`?

Output:

- journey and state gaps;
- unresolved business rules;
- interaction risks;
- acceptance criteria candidates.

## Measurement lens

Ask:

- What business or user outcome proves this worked?
- What is the primary metric, leading indicator, and guardrail?
- What is the baseline, target, timeframe, and data source?
- What events or data must be instrumented?
- What would count as failure even if the feature ships?
- When and by whom will the result be reviewed?

Output:

- metric tree;
- instrumentation requirements;
- measurement risks;
- post-launch review plan.

## Stakeholder and handoff lens

Ask:

- Who decides, who reviews, and who must be informed?
- What are the unresolved disagreements?
- Is the PRD consistent with the brief, strategy, rules, and metrics?
- Can engineering and testing start without asking basic product questions?
- Are assumptions, risks, and open questions visible with owners?
- Is the handoff small enough to read and complete enough to execute?

Output:

- decision log;
- review findings;
- handoff gaps;
- next action and owner.

## Self-review rule

When acting alone:

1. Review as Problem lens.
2. Review as User and value lens.
3. Review as Scope and priority lens.
4. Review as Experience and business-rule lens.
5. Review as Measurement lens.
6. Review as Stakeholder and handoff lens.

For each lens, write at least one of:

- a blocking finding;
- a non-blocking risk;
- `no findings` with the evidence checked.

A single review cannot silently stand in for all six lenses.