---
name: feature-orchestrator
description: 'Use as the entry point for a feature, change request, or internal tool request when a non-PM must move from an ambiguous ask to a planned, reviewed, launch-ready delivery. Routes work by change size, enforces product, UX, engineering, QA, and operations lenses, selects artifacts, and checks stage gates before invoking product-brief, prd, design, test, or planning skills.'
license: MIT
---

# Feature Orchestrator

这是从需求到上线的总入口。它不负责一次生成所有文档，而是判断当前需求应该走哪条路径、需要哪些产物、下一阶段做什么、什么条件下才能通过门禁。

## Use this skill when

- 收到一个新的功能、改进、内部工具或业务诉求，但还不知道应该从哪开始。
- 需求方不是产品经理，需要一条有护栏的端到端路径。
- 开发、测试、运维需要明确各自在 PLAN 和 DESIGN 阶段要产出什么。
- 已有部分文档，但不确定是否足以进入开发。
- 需求范围发生变化，需要重新判断路径和工作量。

## Do not use when

- 线上故障正在发生，优先使用 `systematic-debugging` 和事件处理流程。
- 已有批准的设计与计划，只需要执行，直接使用 `executing-plans`。
- 只是单个文件的小修复，且不需要产品判断，可按 Small change 快速通道处理。

## Orchestration loop

### 1. Intake

记录原始请求、提出人、业务背景、期望时间、约束和已知证据。读取已有文档、代码和上下文，不要重复询问已经能回答的问题。

### 2. Classify change size

判断为 `S`、`M` 或 `L`。至少评估：

- 涉及的用户角色和团队数量；
- 是否改变数据模型、接口、权限、资金、安全或合规；
- 是否可逆，是否影响线上数据；
- 不确定性和依赖数量；
- 预计交付周期。

读取 `references/routing-and-gates.md` 的完整判定表。若信息不足，先按较高的风险等级处理，或标记 `needs-discovery`。

### 3. Create the route plan

使用 `assets/feature-route.md` 生成路线图。路线图必须包含：

- 变更大小和判断理由；
- 需要的产物清单；
- 每个产物使用的 Skill；
- 当前阶段和门禁状态；
- 已知风险、假设和待决策项；
- 下一步动作。

### 4. Run role lenses

至少从以下五个视角检查当前产物：

- Product lens
- UX lens
- Engineering lens
- QA lens
- Ops lens

单人开发也要显式切换视角。读取 `references/role-lenses.md`，为每个视角输出发现、风险或 `no findings`。

### 5. Execute the stage

按路线图调用对应 Skill：

| Stage | Default skill | Fallback when skill is unavailable |
|---|---|---|
| Brief | `product-brief` | Use the brief template embedded in `product-brief` or mark blocked |
| PRD | `prd` | Use the PRD schema in `prd`; do not skip requirements |
| Admin business rules | `admin-product-design` | Load the relevant reference pack manually |
| UX flow | to be added | Create a flow/state document and mark gate blocked |
| Technical design | `solution-design` (planned) | Use `references/artifact-contract.md`; mark technical gate blocked |
| Test design | `test-design` (planned) | Use `references/artifact-contract.md`; mark test gate blocked |
| Delivery plan | `delivery-plan` (planned) | Use `writing-plans` for task-level planning and add environment/test/release sections |
| Launch readiness | to be added | Require monitoring, rollback, ownership, and support checks before release |

**MUST NOT:** silently skip a required artifact because a Skill is unavailable. Mark it `blocked` or produce a fallback artifact, then keep the gate open.

### 6. Gate and handoff

每一个阶段都必须有明确状态：

- `not-started`
- `in-progress`
- `blocked`
- `approved`
- `not-applicable`

门禁未通过时，不得把下一阶段标记为可执行。Handoff 必须包含上游产物路径、未决问题、负责人和下一步 Skill。

### 7. Re-route on change

出现以下情况时重新评估变更大小和路线：

- 新增角色、系统、数据迁移或权限模型；
- 发现安全、资金、合规或不可逆风险；
- 关键假设被推翻；
- 范围显著扩大；
- 外部依赖阻塞。

## Right-sized artifacts

| Size | Required minimum | Optional |
|---|---|---|
| S | Lean brief, acceptance criteria, test notes, release/rollback notes | PRD, separate technical design, test plan |
| M | Product brief, PRD, UX flow if UI, technical design, test design, delivery plan | ADR, launch readiness review |
| L | Full brief, PRD, UX flow, technical design, test design, delivery plan, launch readiness, migration/rollback plan | Discovery, architecture review, staged rollout plan |

详细判定见 `references/routing-and-gates.md`。

## Global guardrails

- **Problem before solution:** 没有清晰问题、用户和价值时，不进入技术设计。
- **No silent assumptions:** 未知业务规则、阈值、权限和指标必须标记 `TBD` 或 `Assumption`。
- **No code before design gate:** M/L 需求在技术设计、测试设计和交付计划通过前，不进入实现。
- **Traceability:** 使用 `FEAT-*`、`REQ-*`、`UX-*`、`DES-*`、`TEST-*`、`TASK-*`、`RISK-*` 编号。
- **One source of truth:** 所有产物统一放入 `docs/delivery/<feature-slug>/`。
- **Evidence over status:** `approved` 必须基于产物内容和角色检查，不得因为时间紧而跳过。

## Output contract

```text
Feature: ...
Size: S | M | L
Current stage: intake | brief | product-design | technical-design | test-design | delivery-plan | launch-ready
Gate status: not-started | in-progress | blocked | approved | not-applicable
Artifacts:
  - path: ...
    skill: ...
    status: ...
Role lens findings:
  - Product: ...
  - UX: ...
  - Engineering: ...
  - QA: ...
  - Ops: ...
Next skill: ...
Open decisions: ...
Owner: ...
```

## Start here

For a new `M` or `L` request, invoke `product-brief` first. For an `S` request, use the Lean Brief path in `product-brief` and keep the route plan lightweight.