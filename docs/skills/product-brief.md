# Product Brief (`product-brief`)

> 把一句模糊需求转成一页可评审的产品简报，明确问题、用户、价值、MVP、指标、备选方案、风险和 go/no-go 结论。

| 维度 | 说明 |
|---|---|
| 分类 | 产品经理工作流 |
| 阶段 | 问题定义与产品价值判断 |
| 主要使用者 | 非产品经理、业务负责人、产品负责人 |
| 输出 | 一页产品简报、建议结论和进入 PRD 的交接信息 |

## 1. 能力

先建立问题链，而不是先列功能；区分事实、假设、决策和未决问题；提出 2-3 个真实选项，包括不开发、人工流程或采购；给出推荐结论和进入 PRD 的条件。

## 2. 定位

**它负责：**

- 先建立问题链，而不是先列功能
- 区分事实、假设、决策和未决问题
- 提出 2-3 个真实选项，包括不开发、人工流程或采购
- 给出推荐结论和进入 PRD 的条件。

**它不负责：**

- 完整 PRD、详细用户故事或字段级规则
- 技术方案、接口设计或测试设计
- 线上缺陷排查
- 在没有任何问题定义时直接证明某个功能应该做

## 3. 适用场景

- 业务方只有一个功能想法，需要判断值不值得做
- 准备写 PRD，但用户、痛点和成功标准还不清楚
- 需要决定 MVP、先做什么和不做什么
- 需要向业务方或领导提交一页决策材料

## 4. 示例

**用户输入：**

```text
运营每天要手工复制超时工单到群里提醒，想做一个批量提醒按钮。请判断这个需求是否值得做，并给出 MVP 和成功指标。
```

**Skill 的执行方式：**

1. 读取已有流程和运营反馈
2. 还原问题链和当前人工成本
3. 比较不开发、人工流程、采购、开发等选项
4. 生成完整草案并标注假设
5. 最多提出 3 个会改变范围或价值的问题
6. 运行质量门禁并给出 go/pilot/defer/reject 结论

**产出：**

`01-brief.md`，包含问题、用户、当前代价、期望结果、指标、范围、备选方案、风险、假设和推荐结论。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 原始请求、业务背景、用户反馈、当前流程、已有数据或文档 |
| 输出 | 一页产品简报、建议结论和进入 PRD 的交接信息 |
| 主要产物 | `docs/product/<feature-slug>/01-brief.md` |

## 6. 文件结构

所有 Skill 都以 `SKILL.md` 为运行时入口；`assets/` 放模板，`references/` 放按需加载的参考文档，`scripts/` 放可执行辅助脚本。

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/product/product-brief/SKILL.md) | 问题链、Proposal-first 工作流、最多三个问题、质量规则和输出契约 |
| [`assets/product-brief.md`](../../skills/product/product-brief/assets/product-brief.md) | 标准产品简报模板 |
| [`references/quality-gate.md`](../../skills/product/product-brief/references/quality-gate.md) | 进入 PRD 前的必备检查、状态定义和非 PM 安全规则 |
| [`references/example.md`](../../skills/product/product-brief/references/example.md) | 从功能请求还原问题、MVP、指标和推荐结论的完整示例 |

## 7. 关联 Skill

[`pm-orchestrator`](pm-orchestrator.md)、[`prd`](prd.md)、[`admin-product-design`](admin-product-design.md)
