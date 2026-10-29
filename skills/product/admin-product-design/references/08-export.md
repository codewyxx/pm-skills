# 08 — Admin Data Export and Download

## Load when

Use for list export, filtered export, asynchronous export jobs, result downloads, or sensitive-field downloads.

## Export trigger and scope

| Item | Rule |
|---|---|
| Export scope | **DEFAULT:** export all records matching the current filters, not only the current page; do not depend on row selection. |
| Reset filters | Export uses the filters present at export time; after reset, use the reset state. |
| No filters | Export all records the user is authorized to access. |
| Volume cap | **DEFAULT/PENDING:** 100,000 rows per export; a module may declare a smaller cap. |
| Async threshold | **DEFAULT/PENDING:** >5,000 rows becomes an async task with in-app notification and a download link. |
| Large detail format | **DEFAULT/PENDING:** >50,000 detail rows switches to CSV; state the switch rule in the PRD. |
| Link lifetime | **DEFAULT/PENDING:** 24 hours. |
| Empty result | **MUST:** disable export and show "当前筛选条件下无数据"; do not create an empty file. |

## File and field contract

- **MUST:** use XLSX by default.
- **MUST:** file name is `模块名_筛选条件摘要_YYYYMMDDHHmm.xlsx`.
- **MUST:** exported columns match list columns and order exactly.
- **MUST:** ambiguous headers include a comment or note explaining the field semantics.
- **MUST:** export enum display labels, not internal codes.
- **MUST:** amounts export as numeric values with an explicit unit; dates follow `06-display-and-media.md`.
- **MUST:** when a list column is added, the export adds it in the same position with the same header.
- **MUST:** time columns export as text in `YYYY-MM-DD HH:mm:ss`; empty values export as `-`.
- **MUST:** failure-detail exports enumerate all failure reasons; no "其他" catch-all.

## Permissions and audit

- **MUST:** the export entry is visible only to roles with export permission.
- **MUST:** sensitive fields (phone, ID number, bank card) are masked by default.
- **MUST:** plaintext export requires a separate permission and an approval record.
- **MUST:** every export records actor, time, filter conditions, row count, and file identity; the audit record is queryable.
- **MUST:** async export completion notifies the requester through `07-notifications.md`.

## Batch result downloads

For import, bind, unbind, or other batch operations:

- **MUST:** provide `下载失败明细（X 条）` and `下载全量结果`.
- **MUST:** failure details include the complete failure reason per row.
- **MUST:** file naming, format, and lifetime follow this reference.
- **MUST:** provide a `查看操作日志` entry from the result page.

## Required PRD output

- Export scope and filter behavior.
- Row limits, sync/async threshold, file-format switch, and link lifetime.
- File name, column order, enum handling, date/time and empty-value format.
- Masking, plaintext permission, approval, and audit fields.
- Async notification and failure handling.
- Deviations under `差异点`.

## Validation checklist

- [ ] Export is based on filters, not current page or selection.
- [ ] Row cap and async threshold are explicit.
- [ ] File columns match list columns in name and order.
- [ ] Sensitive fields are masked by default and audited.
- [ ] Empty result does not produce a file.
- [ ] All `PENDING` limits are marked.