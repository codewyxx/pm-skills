---
name: admin-product-design
description: 'Use when specifying or building B-end, admin, operations, or back-office interfaces. Provides agent-ready rules for lists, search, pagination, forms, validation, permissions, status flows, batch operations, exports, notifications, menus, data display, uploads, and weighted sorting.'
license: MIT
---

# Admin Product Design

Use this skill as a runtime rule pack for internal admin/back-office products. It turns team-oriented product standards into selective, agent-readable references.

## Load policy

1. Read `references/index.md` before using any rule.
2. Load only the reference files whose triggers match the current task. Do not load all references by default.
3. Apply this precedence order:
   - explicit user or business requirement;
   - PRD-specific constraints and platform limits;
   - this reference set;
   - generic UI heuristics.
4. A reference rule marked **MUST** means: comply, or record the deviation under `差异点` with a reason.
5. **PENDING** values are draft or unconfirmed. Do not present them as final facts. Use the documented default, mark it `TBD` when material, and ask for confirmation only when the choice changes behavior or cost.
6. In generated PRDs, state the concrete behavior. Do not merely write "遵循规范" unless the reader has access to the same reference.

## Default workflow

1. Classify the feature: list, form, workflow, permission model, export, notification, menu, media, or weighted ranking.
2. Load the corresponding reference files from `references/index.md`.
3. Extract the applicable defaults and generate explicit requirements or acceptance criteria.
4. Add an `Admin UX rules applied` section and a `差异点` section to the PRD.
5. Before delivery, run the checklist in the loaded reference files.

## Global guardrails

- Hide unauthorized actions; do not show disabled buttons for missing permissions.
- Destructive or irreversible operations require confirmation and a consequence statement.
- Explicitly define empty, loading, error, and no-permission states.
- Use Beijing time, `YYYY-MM-DD`, and `-` for empty values unless a documented exception applies.
- For bulk or asynchronous work, define range, permissions, progress, result, failure reasons, and audit trail.
- Never invent organization-specific values, thresholds, enum values, or approval chains. Leave them as `TBD` and ask.