---
name: product-brief
description: 'Use at the start of a feature, change request, or internal tool request when a non-PM needs to turn an ambiguous ask into a concise, testable product brief. Covers problem, users, outcome, MVP scope, alternatives, success metrics, assumptions, risks, and a go/no-go recommendation before PRD or product planning.'
license: MIT
---

# Product Brief

把一个模糊需求变成一页可评审、可追踪的产品简报。它是 `PRD` 的前置产物，不是完整 PRD，也不是技术方案。

## Use this skill when

- 收到的是一句需求、一个功能想法、一个业务抱怨或一个内部工具请求。
- 需求方不是产品经理，无法直接写清用户、问题、价值和范围。
- 团队准备进入 PRD、技术方案、测试方案或排期，但目标、边界和成功标准还不稳定。
- 需要判断是否值得做，以及当前应做到什么程度。

## Do not use when

- 已有明确、评审通过的 PRD，只需拆实施计划。
- 这是线上缺陷排查，优先使用 `systematic-debugging`。
- 这是纯技术重构且没有用户可见目标；仍需写轻量 brief，但重点改为技术目标、风险和兼容性。

## Operating principles

1. **Problem before solution.** 先定义用户、场景和痛点，再讨论功能。
2. **Proposal first, not interrogation.** 能查到的先查；能合理推断的先写成假设；不要用长问卷阻塞需求方。
3. **One page.** 只保留会影响范围、价值、风险或验收的信息；细节留给 PRD 和设计文档。
4. **Facts, assumptions, decisions, open questions are separate.** 不得把推测写成事实。
5. **MVP is the smallest outcome, not the smallest feature list.** 说明不做什么，比堆功能更重要。
6. **Right-size the artifact.** 小改动用 Lean Brief；中大型功能用 Full Brief。
7. **No invented thresholds or business facts.** 未知值写 `TBD`，并说明由谁确认。

## Workflow

### 1. Read before asking

读取用户提供的需求、现有 PRD、截图、数据、代码或业务背景。先回答项目里已经能回答的问题，不得重复询问。

### 2. Build the problem chain

按顺序补齐：

```text
原始请求 → 谁在什么场景遇到什么问题 → 现在怎么处理 → 代价是什么
→ 期望结果 → 如何判断成功 → 为什么现在做
```

如果无法形成问题链，不要直接生成 PRD；先输出缺失信息和最多 3 个高价值问题。

### 3. Choose brief depth

| 类型 | 判断 | 输出 |
|---|---|---|
| Lean Brief | 单团队、低风险、可逆、无数据/权限/资金影响 | 半页到一页，保留问题、用户、结果、范围、验收和回滚 |
| Full Brief | 跨角色、跨系统、涉及数据/权限/资金/迁移/合规 | 完整模板，增加方案选项、指标、依赖、风险、假设和评审建议 |

### 4. Draft first

默认先给出一份**完整草案**，而不是逐条提问。草案必须：

- 明确标注 `Fact`、`Assumption`、`Decision`、`Open question`；
- 对未知业务值使用 `TBD`；
- 给出推荐方案和不做/延期的理由；
- 提供 2–3 个真实选项，包含不开发、人工流程或采购等非功能选项；
- 用业务语言描述结果，不提前锁定技术实现。

### 5. Ask at most three questions

只有在答案会改变**价值、范围、风险、验收或上线时机**时才提问。每个问题给出推荐默认值和可选答案。其余问题写入 `Open questions`，不要阻塞草案。

### 6. Run the quality gate

读取 `references/quality-gate.md`。不通过时：

- 标记 `Status: needs-clarification`；
- 列出阻塞项、责任人和下一步；
- 不要宣称已经可以进入 PRD。

### 7. Handoff

通过后：

- 生成 `REQ-*` 需求追踪编号；
- 交给 `prd` 展开用户故事、验收标准和完整需求；
- 如涉及后台业务规则，同时加载 `admin-product-design`；
- 如涉及界面，交给 UX flow 或 `frontend-design`；
- 如处于完整产品工作流中，由 `pm-orchestrator` 管理后续策略、体验、PRD、指标与评审；如已有明确产品方向，则直接交给 `prd`。

## Required brief schema

使用 `assets/product-brief.md`。必须包含：

1. Request and context
2. Problem statement
3. Target users and scenarios
4. Current state, evidence, and cost of inaction
5. Desired outcome
6. Success metrics and guardrails
7. Scope: in / out / non-goals / MVP
8. Options considered and recommendation
9. Constraints, dependencies, and risks
10. Assumptions and open questions
11. Go / no-go / pilot / defer recommendation
12. Handoff and traceability IDs

## Quality rules

- 问题陈述中不得直接写做一个 XX 功能作为问题。
- 目标用户必须具体到角色或场景，不能只写用户。
- 成功指标至少包含一个结果指标；无法量化时写 `TBD` 并给出建议指标。
- 范围必须同时有 `In scope` 和 `Out of scope`。
- 每个假设必须有验证方式或责任人。
- 每个风险必须有影响、概率或应对动作。
- 结论必须明确：`go`、`pilot`、`defer`、`reject` 或 `needs-discovery`。
- 一页 brief 不应复制 PRD 的完整字段清单。

## Output contract

```text
Status: draft | needs-clarification | ready-for-prd | rejected | deferred
Recommendation: go | pilot | defer | reject | needs-discovery
Change size: S | M | L
Primary metric: ...
MVP: ...
Next skill: prd | admin-product-design | pm-orchestrator | none
Open blockers: ...
```
