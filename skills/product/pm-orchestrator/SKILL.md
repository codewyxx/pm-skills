---
name: pm-orchestrator
description: 'Use when a non-PM needs to perform product-manager work: turn an ambiguous request into a product brief, product strategy, product experience definition, PRD, success measurement, and review. Routes product work by size, enforces PM quality gates, and produces a clean handoff to engineering and testing without managing their execution.'
license: MIT
---

# PM Orchestrator

这是产品经理工作的总入口。它负责让非产品经理也能完成从需求判断到 PRD 交接的产品工作，不负责技术方案、测试执行或上线管理。

## Use this skill when

- 收到一个业务诉求、功能想法、内部工具请求，但还不确定是否值得做、做成什么样。
- 需求方不是产品经理，需要一条可执行的产品工作路径。
- 需要判断应该只写产品简报，还是需要完整的产品策略、体验定义和 PRD。
- 产品方案需要评审，但不能确定 PRD 是否足够清楚、可测试、可交接。
- 需求范围发生变化，需要重新判断产品工作量和产物。

## Do not use when

- 已有批准的产品方案和 PRD，只需要执行。
- 线上故障正在发生，优先处理事件和缺陷。
- 这是纯技术重构，且没有用户可见目标或业务规则变化；可只写轻量产品说明。
- 需要技术架构、测试设计或发布计划；这些属于下游专业工作，不在本 Skill 的职责范围。

## PM workflow

### 1. Intake

记录：

- 原始请求和提出人；
- 业务背景和触发事件；
- 目标用户或业务角色；
- 期望时间和关键约束；
- 已有材料、数据和证据。

读取现有文档和上下文，不要重复询问已经能回答的问题。

### 2. Classify product work

判断产品工作规模：

- `S`：小改动或局部优化；
- `M`：新功能或跨角色流程；
- `L`：新产品、新业务模式或多个团队参与的产品计划。

评估维度：

- 用户和业务影响范围；
- 是否改变核心流程、权限、商业规则或数据口径；
- 不确定性和决策数量；
- 是否需要产品策略、路线图或跨团队对齐；
- 失败或做错的业务代价。

读取 `references/pm-routing.md`。

### 3. Create the PM route

使用 `assets/pm-route.md` 生成路线图，必须包含：

- 工作规模和理由；
- 需要的产品产物；
- 每个产物使用的 Skill；
- 当前阶段和门禁状态；
- 已知假设、风险和待决策项；
- 下一步动作。

### 4. Run PM lenses

至少从以下六个视角检查当前工作：

- Problem lens
- User and value lens
- Scope and priority lens
- Experience and business-rule lens
- Measurement lens
- Stakeholder and handoff lens

读取 `references/pm-lenses.md`。单人工作时也要显式切换视角，并为每个视角输出发现、风险或 `no findings`。

### 5. Produce the right artifacts

按路线图调用对应 Skill：

| Product stage | Default skill | Output |
|---|---|---|
| Brief | `product-brief` | Problem, user, value, MVP, metrics, risks, go/no-go |
| Strategy | `product-strategy` (planned) | Product choices, alternatives, priority, roadmap |
| Experience | `product-experience` (planned) | User journey, information architecture, states, business rules |
| PRD | `prd` | Requirements, stories, acceptance criteria, edge cases |
| Admin business rules | `admin-product-design` | Lists, forms, permissions, states, batch ops, exports, notifications |
| Measurement | `metrics-experiment` (planned) | Metric tree, instrumentation, experiment, post-launch review |
| Review | `product-review` (planned) | PM quality gate and handoff review |

**MUST NOT:** silently skip a required product artifact because a future Skill is unavailable. Mark it `blocked` or create a fallback artifact using `references/artifact-contract.md`.

### 6. Check the PM gates

Read `references/pm-routing.md`. Each gate must be one of:

- `not-started`
- `in-progress`
- `blocked`
- `approved`
- `not-applicable`

A gate cannot be `approved` because of schedule pressure. It must be based on artifact content and PM lens review.

### 7. Handoff

The output of this Skill ends at a product handoff package:

- approved brief or PRD path;
- target users and outcomes;
- scope, non-goals, and priorities;
- end-to-end flows and edge cases;
- business rules and permissions;
- acceptance criteria;
- success metrics and instrumentation;
- assumptions, risks, and open questions;
- source documents and IDs.

The handoff must be sufficient for engineering and testing to work independently. It must not prescribe their internal technical design, test strategy, or release execution.

## Artifact chain

```text
00-route.md
01-brief.md
02-strategy.md        # when required
03-experience.md      # when UX or business flow changes
04-prd.md
05-metrics.md         # when outcome measurement matters
06-review.md
```

For small changes, collapse the chain into a Lean Brief and a short PRD. Do not create ceremony without product risk.

## PM guardrails

- **Problem before solution:** 没有清晰问题、用户和价值时，不进入 PRD。
- **No feature list as strategy:** 功能列表不是产品策略，必须说明取舍、优先级和为什么。
- **No invented facts:** 市场、用户、政策、阈值和数据一律区分事实与假设。
- **No silent assumptions:** 未确认信息标记 `TBD` 或 `Assumption`，并写清责任人。
- **Testable requirements:** 每条需求必须能被验收，不能只写提升体验、优化流程。
- **One source of truth:** 产品产物统一放入 `docs/product/<feature-slug>/`。
- **Handoff, not command:** 向下游交付清楚的产品定义，不替研发和测试做内部计划。
- **No gate skipping:** 时间压力不能成为跳过产品判断的理由。

## Output contract

```text
Feature: ...
Product work size: S | M | L
Current stage: intake | brief | strategy | experience | prd | measurement | review | handoff
Gate status: not-started | in-progress | blocked | approved | not-applicable
Artifacts:
  - path: ...
    skill: ...
    status: ...
PM lens findings:
  - Problem: ...
  - User and value: ...
  - Scope and priority: ...
  - Experience and business rules: ...
  - Measurement: ...
  - Stakeholder and handoff: ...
Next skill: ...
Open decisions: ...
Owner: ...
```

## Start here

For any new `M` or `L` request, start with `product-brief`. For a small `S` change, use the Lean Brief path and a short PRD. If the problem or opportunity is still unclear, stop at the brief and do not force a solution.