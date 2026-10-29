# 04 — Status Flows, Action Buttons, Batch Operations, and Result Pages

## Load when

Use for objects with lifecycle states, approval flows, row actions, bulk operations, template imports, or asynchronous execution results.

## State naming and display

- **MUST:** use a consistent grammar: `待 + 动作`, `动作 + 中`, `已 + 动作` (for example 待提交、审核中、已通过、已关闭).
- **MUST:** use one state vocabulary per object across the product; check for synonyms before adding a state.
- **MUST:** keep color semantics fixed:
  - in progress: blue;
  - success: green;
  - warning / pending: orange;
  - failure / rejected: red;
  - terminated / closed: gray.
- **MUST:** use the same state color on every page.

## State machine

Every flow-bearing object **MUST** have a state machine with this minimum schema:

| Current state | Action | Actor / role | Preconditions | Next state | Reversible? | Side effects |
|---|---|---|---|---|---|---|

Additional rules:

- **MUST:** define the trigger, actor, condition, resulting state, and side effects for every transition.
- **MUST:** mark irreversible transitions (close, void, archive) explicitly.
- **MUST:** define immediate UI refresh and the maximum delay for other clients.
- **MUST:** define a `当前状态 × 可用操作` matrix; do not rely on prose such as "按状态展示按钮".
- **MUST:** for multi-level serial approval, define each level's role, threshold, and final outcome. Intermediate approval is advisory when the source rule says so; only the final level sets the terminal result.
- **MUST:** approval stages that must be performed by different people state the separation constraint in the permission matrix.
- **MUST:** log exemption/no-review actions such as publish, unpublish, or archive.

## Action button rules

| Rule | Requirement |
|---|---|
| Primary action | **MUST:** at most one primary button per page or modal. |
| Copy | **MUST:** use a verb or verb-object phrase; use one term for one action across the product. Do not mix 提交/保存/确认 for the same behavior. |
| Destructive actions | **MUST:** use warning styling and a consequence-specific confirmation dialog. |
| Disabled state | **MUST:** explain why the action is disabled and what unlocks it. |
| Selection gating | **MUST:** disable confirm/submit until required selections are complete and state the completion condition. |
| Permission | **MUST:** hide actions the user cannot perform; do not show a disabled button for missing permission. |
| Batch bar | **MUST:** show it only after selection; show selected count; preserve cross-page selection. |

## Batch operation baseline

- **MUST:** define selection scope, permissions, confirmation, execution mode, result handling, and audit.
- **MUST:** destructive bulk actions require a confirmation that states how many records are affected and what will happen.
- **MUST:** template-based operations place the entry in the list `PageHeader` next to export.
- **MUST:** bind and unbind are separate entries even when they share a template and preview flow; document only their validation differences.

## Template import

1. **Download template** — system-provided only; users cannot build their own file.
2. **Upload and validate** — format, required columns, row limit, and row-level validity.
3. **Preview** — total, executable, failed, and no-op counts; show reason distribution and any multi-step matching chain.
4. **Execute** — enabled only when at least one row is executable; rows not passing validation are skipped and explained.
5. **Result** — provide success/failure statistics, failure details, and file downloads.

Template rules:

- **MUST:** fixed first-row header, fixed column names and order; users may not add, remove, or rename columns.
- **MUST:** keep columns minimal: business key + target key only.
- **MUST:** provide a "查看模板示例" dialog with column names, example values, and formats.
- **MUST:** accept only the declared file types (CSV/XLSX when supported).
- **MUST:** all data columns use text format to prevent long numbers from becoming scientific notation.
- **MUST:** document exact value formats, case sensitivity, whitespace rules, and encoding (CSV: UTF-8 with BOM).
- **DEFAULT:** maximum 5,000 rows per import. This is **PENDING**; confirm for each business object.
- **MUST:** file name: `{业务对象}{操作}导入模板_v{版本号}.xlsx`; increment the version when the template structure changes.

## Preview and result page

- **MUST:** preview uses three stat categories: `校验通过（将执行）`, `校验失败（不参与执行）`, `无需处理（幂等）`.
- **MUST:** detail rows show row number, business keys, validation result, and reason.
- **MUST:** only `校验通过` rows execute; failed and no-op rows are skipped.
- **MUST:** result banner has exactly three states: all succeeded / partially succeeded / all failed.
- **MUST:** result page shows success and failure counts, an operation-log link, `下载失败明细（X 条）`, and `下载全量结果`.
- **MUST:** detail rows include row number, business fields, result, and complete failure reason.
- **MUST:** success detail rows do not have individual log links.
- **MUST:** failure reasons are MECE. Do not use "其他" as a catch-all.
- **MUST:** file names:
  - success/combined: `{操作}结果明细_{yyyyMMddHHmmss}.xlsx`
  - failures: `{操作}失败明细_{yyyyMMddHHmm}.xlsx`
- **MUST:** use server time for the file timestamp.

## Failure reason contract

Define a table with `error_code`, trigger condition, user-visible copy, and whether the row is failed or no-op. Generic pattern:

| Error code | Trigger | User-visible message |
|---|---|---|
| `NOT_FOUND` | Matching record does not exist | 未找到匹配记录，请检查输入 |
| `ALREADY_EXISTS` | Target is already bound/created | 该记录已存在，无需重复操作（幂等） |
| `INVALID_STATE` | Object is disabled or not eligible | 当前状态不允许执行该操作 |
| `DUPLICATE_ROW` | Template contains duplicate keys | 与第 N 行重复，已自动去重 |
| `NO_CHANGE` | Requested state already equals target state | 当前已是目标状态，已跳过 |
| `TEMPLATE_INVALID` | Missing/renamed column or unsupported file | 模板格式不正确，请使用系统提供的模板 |

## Required PRD output

- State machine table and operation matrix.
- Button behavior, copy, confirmation, permission, and disabled reasons.
- Batch selection/permission/confirmation/result and audit behavior.
- Template schema, validation messages, preview stats, and row-limit.
- Failure enum and file naming.
- Every deviation under `差异点`.

## Validation checklist

- [ ] Every state transition has actor, condition, target state, and side effects.
- [ ] The action matrix covers all states.
- [ ] Batch scope and cross-page selection are explicit.
- [ ] Preview, execution, and result counts reconcile.
- [ ] Failure reasons are complete and non-overlapping.
- [ ] Audit and download behavior are specified.