# 05 — Permission Points, Roles, and Data Scope

## Load when

Use for role-based access control, admin menus, action visibility, data scope, approval segregation, or sensitive-field access.

## Permission granularity

- **MUST:** split permission points by `模块 + 对象 + 动作`, e.g. `客户管理-客户-导出`.
- **MUST:** support the standard action set: 查看、新增、编辑、删除、导出、审批. Define non-standard actions (关闭、作废) separately.
- **MUST:** keep view permission separate from operation permissions. Seeing a page does not imply permission to act.
- **MUST:** make sensitive operations independent permission points: delete, export, plaintext viewing, refund/adjustment, and similar high-risk actions.
- **MUST:** never fold fund, accounting, refund, or adjustment actions into a generic "edit" permission.
- **MUST:** multi-level approval permissions state each level's role and threshold.

## Naming

- **MUST:** name permissions `模块名-对象名-动作`, e.g. `订单管理-订单-导出`.
- **MUST:** names must be understandable in the permission configuration UI; do not expose only English codes.
- **MUST:** reuse a permission point when the same object is managed by multiple modules; document the reuse relationship.

## Default policy

| Rule | Requirement |
|---|---|
| New role | **MUST:** deny by default; grant permissions explicitly. |
| Missing view permission | **MUST:** hide the menu and entry. |
| Missing action permission | **MUST:** hide the button; do not show it disabled. |
| Direct URL access | **MUST:** show the no-permission empty state. |
| Data scope | **MUST:** define scope separately from functional permission. |
| Tenant isolation | **DEFAULT:** tenant data is isolated. Cross-tenant access requires explicit authorization and audit. |
| Data-scope levels | **MUST:** choose from all data / department data / own data, or document another approved scope. |
| Permission change | **MUST:** state whether changes take effect immediately or at next login. |
| Approval separation | **MUST:** initial and final approval levels use different roles or people unless an explicit exception is approved. |

## Permission matrix

The PRD **MUST** provide a matrix when a feature has roles or data scopes:

| Permission point | Role A | Role B | Role C | Data scope / condition |
|---|---|---|---|---|
| `模块-对象-查看` | ✓ | ✓ | — | own / department / all |
| `模块-对象-编辑` | ✓ | — | — | own |
| `模块-对象-导出` | — | ✓ | — | masked fields only |

Rules:

- Rows are permission points; columns are roles.
- Cells state allow/deny plus any scope or condition.
- Use either a hierarchy tree or a matrix; use the matrix when there are more than three roles.
- Include approval level and threshold when multi-level review exists.

## Required PRD output

- Permission points and their granularity.
- Role × permission matrix with data scope.
- Visibility behavior for menus, buttons, direct URLs, and APIs.
- Sensitive-field and export restrictions.
- Approval separation and threshold rules.
- Permission-change timing and audit behavior.
- Deviations under `差异点`.

## Validation checklist

- [ ] Sensitive operations are independent permission points.
- [ ] View and action permissions are decoupled.
- [ ] Every role has an explicit allow/deny cell and data scope.
- [ ] Unauthorized menu, button, URL, and API behavior is defined.
- [ ] Approval segregation and thresholds are testable.
- [ ] Permission-change timing is explicit.