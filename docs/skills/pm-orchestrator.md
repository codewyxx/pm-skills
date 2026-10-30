# PM Orchestrator (`pm-orchestrator`)

> 面向非产品经理的 PM 工作总入口，负责判断产品工作规模、选择产品产物、执行六类 PM 视角检查，并控制 G0-G6 产品门禁。

| 维度 | 说明 |
|---|---|
| 分类 | 产品经理工作流 |
| 阶段 | 从需求判断到产品交接的编排 |
| 主要使用者 | 非产品经理、产品负责人、业务负责人 |
| 输出 | PM route、产物清单、门禁状态、下一 Skill 和产品交接包 |

## 1. 能力

把模糊需求路由到正确的产品工作路径；决定只需要 Lean Brief，还是需要策略、体验、PRD、指标和评审；检查每个阶段是否有可评审的产物；把产品定义整理成研发和测试可以独立执行的交接包。

## 2. 定位

**它负责：**

- 把模糊需求路由到正确的产品工作路径
- 决定只需要 Lean Brief，还是需要策略、体验、PRD、指标和评审
- 检查每个阶段是否有可评审的产物
- 把产品定义整理成研发和测试可以独立执行的交接包。

**它不负责：**

- 技术架构、API、数据模型和工程方案
- 测试用例设计、测试执行和发布管理
- 替代 PRD 的详细需求内容
- 用时间压力跳过产品判断

## 3. 适用场景

- 收到一句话业务需求，不知道是否需要写 PRD
- 已有 brief 或 PRD，需要判断能否交接
- 需求范围变化，需要重新评估产品工作量和门禁
- 非 PM 需要按产品经理的方式完成从问题到需求的闭环

## 4. 示例

**用户输入：**

```text
运营团队希望下周上线批量提醒功能，现在只有一句话需求。请判断产品工作量，安排需要写的产品文档，并在完成后检查是否可以交给研发和测试。
```

**Skill 的执行方式：**

1. 读取现有业务背景和材料
2. 判断为 S/M/L 产品工作规模
3. 生成 PM route 和 artifact plan
4. 调用 product-brief，必要时继续 strategy、experience、PRD、metrics、review
5. 运行六类 PM 视角检查
6. 输出 gate 状态、未决问题和交接包

**产出：**

一份 `00-route.md`，加上已经完成的产品产物路径、门禁状态、风险、未决问题和下一步动作。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 原始请求、业务背景、已有文档、用户反馈、业务规则和约束 |
| 输出 | PM route、产物清单、门禁状态、下一 Skill 和产品交接包 |
| 主要产物 | `docs/product/<feature-slug>/00-route.md` |

## 6. 文件结构

所有 Skill 都以 `SKILL.md` 为运行时入口；`assets/` 放模板，`references/` 放按需加载的参考文档，`scripts/` 放可执行辅助脚本。

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/product/pm-orchestrator/SKILL.md) | 触发条件、PM 工作流、产品阶段、六类视角和整体护栏 |
| [`assets/pm-route.md`](../../skills/product/pm-orchestrator/assets/pm-route.md) | PM route 模板，记录规模、产物、门禁、视角发现和下一动作 |
| [`references/pm-routing.md`](../../skills/product/pm-orchestrator/references/pm-routing.md) | S/M/L 判定、产物矩阵、G0-G6 门禁、Lean PM 路径和重新路由条件 |
| [`references/pm-lenses.md`](../../skills/product/pm-orchestrator/references/pm-lenses.md) | Problem、User/Value、Scope/Priority、Experience/Rules、Measurement、Stakeholder/Handoff 六类检查清单 |
| [`references/artifact-contract.md`](../../skills/product/pm-orchestrator/references/artifact-contract.md) | 产品产物目录、元数据、编号、追踪矩阵和交接包标准 |

## 7. 关联 Skill

[`product-brief`](product-brief.md)、[`prd`](prd.md)、[`admin-product-design`](admin-product-design.md)
