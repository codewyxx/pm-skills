# Admin Product Design Reference Index

## How to use

- Load only files matching the task. Each file is self-contained.
- If multiple rows match, load the primary file first, then supporting files.
- Use `manifest.yaml` for machine-readable routing.
- Rules use three markers: **MUST** (baseline requirement), **DEFAULT** (apply unless overridden), **PENDING** (draft value requiring confirmation when material).
- Explicit user/business requirements override this set, but the PRD must record the deviation under `差异点`.

## Routing table

| Task contains | Primary reference | Load next when needed |
|---|---|---|
| 列表、表格、排序、分页、搜索、筛选、下钻 | `01-list-query.md` | `03-feedback-states.md`, `05-permissions.md`, `08-export.md` |
| 表单、字段、校验、提交、草稿 | `02-forms-validation.md` | `03-feedback-states.md`, `05-permissions.md` |
| 空状态、加载、错误、成功反馈、确认框 | `03-feedback-states.md` | `01-list-query.md`, `04-status-actions-batch.md` |
| 状态机、状态流转、操作按钮、批量操作、导入结果页 | `04-status-actions-batch.md` | `03-feedback-states.md`, `05-permissions.md`, `07-notifications.md`, `08-export.md` |
| 权限、角色、权限矩阵、数据范围、越权 | `05-permissions.md` | `04-status-actions-batch.md`, `08-export.md` |
| 日期、金额、数字、单位、图片、视频、上传 | `06-display-and-media.md` | `03-feedback-states.md` |
| 站内信、短信、邮件、推送、通知频控 | `07-notifications.md` | `04-status-actions-batch.md` |
| 导出、下载、异步任务、敏感字段 | `08-export.md` | `05-permissions.md`, `07-notifications.md` |
| 后台菜单、导航、分类、资源码 | `09-admin-menu.md` | `05-permissions.md` |
| 多因子排序、权重、评分、运营排序 | `10-weighted-sorting.md` | `01-list-query.md` |

## Common combinations

### New admin list page

Load: `01-list-query.md` + `03-feedback-states.md`.
Add `05-permissions.md` when row actions, data scope, or sensitive fields exist. Add `08-export.md` when export exists.

### New create/edit form

Load: `02-forms-validation.md` + `03-feedback-states.md`.
Add `05-permissions.md` for role-gated fields or actions. Add `06-display-and-media.md` for formats or uploads.

### Approval or batch workflow

Load: `04-status-actions-batch.md` + `05-permissions.md` + `07-notifications.md`.
Add `08-export.md` for result downloads and `03-feedback-states.md` for exception UX.

### Operations ranking configuration

Load: `10-weighted-sorting.md` + `01-list-query.md` + `05-permissions.md`.

## Required PRD output

The generated PRD must include:

1. **Feature classification** — list, form, workflow, permission model, export, notification, menu, media, or ranking.
2. **Concrete behavior** — defaults, triggers, states, permissions, validation, failure handling, and edge cases.
3. **Acceptance criteria** — observable outcomes, not slogans.
4. **Admin UX rules applied** — short list of the reference IDs used.
5. **差异点** — each override with the reason and owner or `TBD`.
6. **Open questions** — unresolved `PENDING` or organization-specific values.

## Coverage map

| Reference | Source topics covered |
|---|---|
| `01-list-query.md` | List sorting, pagination, search, filtering, drilldown |
| `02-forms-validation.md` | Form validation and submission |
| `03-feedback-states.md` | Empty, loading, error, success, confirmation |
| `04-status-actions-batch.md` | State machines, action buttons, bulk operations, result pages |
| `05-permissions.md` | Permission granularity, naming, matrix, data scope |
| `06-display-and-media.md` | Date/number/money formatting, image/video upload and display |
| `07-notifications.md` | Notification levels, channels, copy, frequency control |
| `08-export.md` | Export scope, file format, permissions, audit |
| `09-admin-menu.md` | Admin menu taxonomy, naming, resource mapping |
| `10-weighted-sorting.md` | Multi-factor weighted ranking and configuration |