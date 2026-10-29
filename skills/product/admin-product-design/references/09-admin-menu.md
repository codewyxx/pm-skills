# 09 — Admin Menu Taxonomy, Naming, and Resource Mapping

## Load when

Use for admin navigation design, adding or moving a menu item, defining menu hierarchy, naming menus, or registering permission resource codes.

## Core model

A menu leaf represents one managed entity. Every menu item **MUST** answer:

1. Which entity does it manage?
2. Which level should it sit at?
3. Does it belong in the primary navigation?

If the entity is unknown or unregistered, the menu item is not ready for review.

## Classification rules

| Rule | Test | Placement |
|---|---|---|
| R1 Entity uniqueness | Each leaf has one entity; one entity has one primary entry | Consolidate duplicate entries under one group. |
| R2 Follow the owner | One entity and only a subordinate view of its owner | Place under the owner's second level. |
| R3 Cross-cutting capability | Affects two or more entities and creates no business document | Place under platform capabilities, grouped with similar entities. |
| R4 Parameters are not primary nav | No business document; referenced by rules; changed once and applied globally | Place under business parameters, mirroring the main navigation's names and order. |
| R5 Depth limit | Two levels preferred; third level only when a second-level group would exceed about 7 items; never four levels | Use third-level grouping only where justified. |
| R6 Permission mapping | Every leaf maps to one permission resource code | Add missing menus or missing resource codes; never allow a menu without a resource. |

## Decision order

Apply in this order; stop at the first match:

1. **Parameter test** — no business document, referenced by rules, global effect → business parameters.
2. **Cross-cutting test** — affects two or more entities, no business document → platform capabilities.
3. **Subordinate test** — exactly one entity and not the entity's management page → second level under the owner.
4. **Independent test** — otherwise → first level.

### Exception: promote to first level

A multi-entity evolving system may become a first-level domain only when all three are true:

- at least 3 pages;
- no overlap with an existing domain;
- a written promotion rationale is included in review.

If any condition fails, keep it subordinate.

## Naming

| Level | Rule | Good example | Bad example |
|---|---|---|---|
| First level / domain | 2–4 character noun; no "管理" or "配置" | 客户、订单与履约 | 客户管理、业务规则配置 |
| Second level | ≤4 characters; remove redundant prefixes; pair list/review entries | 评级、资金账户、绑定关系 | 客户列表、账户管理页 |
| Third level | `对象 · 状态` | 合同 · 审核、合同 · 已签约 | 待审核合同管理 |
| Parameter page | Sub-domain + object + `规则` | 结算规则 · 保证金规则 | 客户费用配置（含审核） |
| Ambiguous terms | One global definition; never mix meanings | 响应保证金 ≠ 履约保证金 | Multiple meanings of 保证金 |

## Permission resource mapping

- **MUST:** resource code format is `object:action`, e.g. `resource_binding:view`.
- **MUST:** read-only pages grant `view` and, when supported, `export`.
- **MUST:** action pages split permissions by action.
- **MUST:** review pages grant `review` and `secondary_review`.
- **MUST:** allow a hidden resource without a menu only when it is registered; never allow a menu without a resource.

## New menu workflow

1. **Propose** — page name, backing entity, entity relationship (management page vs subordinate view), whether it creates a business document, target users, and permission resource code.
2. **Classify** — run the decision order and record the matched rule number.
3. **Name check** — apply naming rules and search the full tree for duplicate names or second entries to the same entity.
4. **Register permission** — create the resource code and attach it to the correct first-level domain.
5. **Review** — proposal must cite the rule number and include all required fields.

Responsibilities:

- Product owns completeness and rule citation.
- Engineering owns resource-code registration and route registration.
- Operations uses the final menu and does not add entries ad hoc.
- Unresolved cases go to the platform product group for a written decision and a future rule update.

## Required PRD output

- Entity and menu placement.
- Matched rule number and rationale.
- Menu hierarchy and names.
- Permission resource codes.
- Any promotion exception with its three checks.
- Deviation under `差异点`.

## Validation checklist

- [ ] Every leaf maps to exactly one entity.
- [ ] The decision order and matched rule are recorded.
- [ ] Names follow level-specific rules.
- [ ] No duplicate entry for the same entity.
- [ ] Every menu has a resource code; hidden resources are registered.
- [ ] No fourth-level menu exists.