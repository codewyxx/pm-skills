# 01 — List, Search, Sort, Filter, and Pagination

## Load when

Use for any table, list, card feed, search area, filter panel, or drill-down destination in an admin product.

## Sorting

| Situation | Rule |
|---|---|
| Default sort | **DEFAULT:** `created_at DESC` (newest first). Use a more meaningful business time field when the object has one; state the substitute in `差异点`. |
| Multi-field sort | **MUST:** list the field priority, e.g. status priority first, then creation time descending. |
| Pinned/recommended rows | **MUST:** place before normal sorted rows and make the intervention visibly identifiable. |
| Sortable header | **MUST:** cycle ascending → descending → unsorted. Only one column may sort at a time. |
| Non-sortable columns | **MUST:** identify them in the PRD; the list retains its default order. |
| Null values | **MUST:** place at the end and exclude from ascending/descending comparison. |

Sorting interaction:

- Changing filters preserves the user's current sort; if no manual sort exists, preserve the default.
- A manual sort persists across pagination.
- Leaving the page and returning restores the default sort.

## Pagination

| Situation | Rule |
|---|---|
| Page size | **DEFAULT:** 20 rows. Card/content lists: 10. Optional 10/50 is **PENDING** and must not be presented as final. |
| When to paginate | **MUST:** paginate when result count exceeds page size; hide the pager when there is only one page. |
| Pager contents | **MUST:** total count, page number, previous, next, and jump-to-page input. |
| Selection across pages | **MUST:** preserve selected rows across pages and show the total selected count. |
| Scroll loading | **DEFAULT:** use a conventional pager; do not use infinite scroll. A PRD exception must state the reason. |
| Empty results | **MUST:** show the empty state from `03-feedback-states.md`; do not render a pager. |
| Card list layout | **MUST:** desktop image-left/text-right, fixed thumbnail size; mobile image-top/text-bottom; use a conventional pager. |

## Search

| Rule | Requirement |
|---|---|
| Admin matching | **DEFAULT:** fuzzy matching for name, phone, and similar text. Do not expose an exact/fuzzy mode switch unless explicitly required. |
| Search fields | **MUST:** enumerate every searched field and the minimum input length in the PRD. Fields outside that set must not match. |
| Exact lookup | **MUST:** use a separate exact-search entry when full-value lookup is required (for example, a full 11-digit phone number). Never mix exact and fuzzy behavior in one control. |
| No result | **MUST:** show "未找到符合条件的数据" plus reset/change-query guidance; keep the filter bar visible. |

## Filters and drill-down

- **MUST:** time ranges are closed intervals from `00:00:00` on the start date through `23:59:59` on the end date.
- **MUST:** one-sided ranges are allowed; combine different filters with `AND`; null records do not match the range.
- **DEFAULT:** filter defaults are empty/all; reset clears every filter and restores the default list.
- **MUST:** enum options match the values displayed in the list, and the PRD lists the complete enum.
- **DEFAULT:** filter order follows list-column order unless a strong business reason exists.
- **MUST:** include the filtered field in the list or detail view (for example, show phone when filtering by phone).
- **MUST:** drill-down destinations carry every source filter needed to reproduce the number and display the inherited values in filter controls.
- **MUST:** define the inherited field semantics, including real-time changes and empty-value display.
- **MUST:** URL parameters are initial state only; the user may change other filters after arrival.
- **MUST NOT:** implement drill-down through hidden hard-coded logic. Add a real filter if needed.
- **MUST:** the frontend owns drill-down parameter passing; do not require backend logic changes merely to forward filters.

## Required PRD output

- List columns in display order, including sortable and non-sortable columns.
- Default sort, alternate business-time field, multi-field priority, and tie-breaker.
- Search fields, minimum length, fuzzy/exact behavior, and no-result handling.
- Filter definitions, enum values, defaults, time semantics, and filter-to-column mapping.
- Page size, pagination behavior, cross-page selection, and empty state.
- Drill-down parameter mapping and inherited field semantics.
- Every deviation under `差异点`.

## Validation checklist

- [ ] Sort behavior is explicit for default, manual, filtered, paginated, and re-entry states.
- [ ] Null placement and multi-field ordering are defined.
- [ ] Search fields and exact-query boundary are unambiguous.
- [ ] Every filter has a default, operator, and empty-result state.
- [ ] Drill-down reproduces the source count and displays inherited filters.
- [ ] `PENDING` page-size alternatives are not stated as final.