# 03 — Empty, Loading, Error, Success, and Confirmation Feedback

## Load when

Use whenever the PRD defines a page, table, card, modal, async action, network dependency, or operation result.

## Empty states

| Pattern | Trigger | Required presentation |
|---|---|---|
| Initial empty | User has no data yet | Explanation + primary action, e.g. "暂无订单，去发布需求". |
| Filtered empty | Search/filter has no match | "未找到符合条件的数据" + reset filters; keep filter bar styling identical to the populated state. |
| Removed content | Link points to archived/offline content | "该内容已下线" + return/list action; return HTTP 410 when SEO-relevant. |
| No permission | User lacks access | Explain the missing permission + request-access path or contact. |
| Load failure | Service/network failure | "加载失败" + retry; do not expose technical error codes to ordinary users. |

Additional rules:

- **MUST:** empty-state copy is declarative and action-oriented; do not use jokes, cute tone, or vague language.
- **MUST:** keep style and copy structure consistent across pages in the same module.
- **MUST:** modal query with no match shows a no-match message and change-query guidance, not an empty table.

## Loading states

- **MUST:** lists and detail pages use a skeleton or progress indicator.
- **DEFAULT:** after 10 seconds show "加载时间较长，请稍候或刷新重试". The threshold is **PENDING**; do not present it as final without confirmation.
- **MUST:** submit-button loading behavior follows `02-forms-validation.md`.

## Feedback hierarchy

| Level | Use | Presentation |
|---|---|---|
| Light feedback | Success or general information | Top toast, auto-dismiss after about 3 seconds. Duration is **PENDING**. |
| Confirmation | Destructive or irreversible action | Centered dialog, consequence statement, confirm as primary action. |
| Blocking error | System error prevents progress | Dialog with cause and recovery path, or a page-level error page. |

## Post-action behavior

- **MUST:** define refresh behavior after success.
- **DEFAULT:** list operations refresh current-page data; create operations open detail or return to the list and show a success message.
- **MUST:** user-facing network/service/timeout copy is "网络异常，请稍后重试"; technical details belong in logs only.
- **MUST:** when a result is only partially successful, do not use a generic success toast; use the result-page pattern in `04-status-actions-batch.md`.

## Required PRD output

- Every empty-state type that can occur and its copy/action.
- Loading indicators and long-wait behavior.
- Success, warning, blocking-error, and confirmation behavior.
- Refresh/navigation behavior after each action.
- Which technical details stay out of user-facing copy.

## Validation checklist

- [ ] Initial, filtered, removed, no-permission, and load-failure states are covered where applicable.
- [ ] Empty-state copy states what happened and what the user can do next.
- [ ] Destructive operations have consequence-specific confirmation.
- [ ] Network errors have a retry path.
- [ ] Success behavior defines refresh and navigation.
- [ ] `PENDING` time thresholds remain configurable and labeled.