# Analytics Tracking (`analytics`)

> 规划、配置、审计和改进分析埋点，覆盖事件设计、命名、UTM、GA4、GTM、数据质量和测量口径。

| 维度 | 说明 |
|---|---|
| 分类 | 营销与分析 |
| 阶段 | 指标埋点与测量 |
| 主要使用者 | 营销、产品、数据、开发 |
| 输出 | Tracking Plan、事件规范和实现验证建议 |

## 1. 能力

从决策问题反推需要的事件；设计事件命名和属性；区分事件类型；维护数据质量；检查实现和验证埋点；给出 GA4/GTM 落地建议。

## 2. 定位

**它负责：**

- 从决策问题反推需要的事件
- 设计事件命名和属性
- 区分事件类型
- 维护数据质量
- 检查实现和验证埋点
- 给出 GA4/GTM 落地建议。

**它不负责：**

- 替代产品策略或业务指标决策
- 替代数据仓库建模和 BI 平台建设
- 只做广告平台转化追踪；这类需求应进一步使用 conversion-tracking 相关能力
- 没有业务问题时堆砌事件数量

## 3. 适用场景

- 新功能需要定义埋点和成功指标
- GA4、GTM 或事件实现需要审计
- 营销活动需要 UTM 和转化测量
- 现有事件命名混乱、数据口径不一致或埋点不触发

## 4. 示例

**用户输入：**

```text
为批量提醒功能设计埋点，目标是判断提醒是否减少了超时工单，并防止重复发送和误提醒。
```

**Skill 的执行方式：**

1. 明确决策问题和成功指标
2. 设计事件、属性和命名
3. 定义触发时机、去重和窗口
4. 映射到 GA4/GTM 实现
5. 制定验证和审计步骤
6. 输出 tracking plan

**产出：**

事件表、命名规范、属性、触发条件、指标口径、GA4/GTM 实现说明和验证清单。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 业务目标、用户流程、现有事件、分析工具、数据口径和实现环境 |
| 输出 | Tracking Plan、事件规范和实现验证建议 |
| 主要产物 | `05-metrics.md` 和 Tracking Plan |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/marketing/analytics/SKILL.md) | 分析原则、Tracking Plan 框架、事件命名、核心事件和实施流程 |
| [`references/event-library.md`](../../skills/marketing/analytics/references/event-library.md) | 常用事件库和事件设计参考 |
| [`references/ga4-implementation.md`](../../skills/marketing/analytics/references/ga4-implementation.md) | GA4 事件、参数和实现注意事项 |
| [`references/gtm-implementation.md`](../../skills/marketing/analytics/references/gtm-implementation.md) | GTM 标签、触发器和变量实现参考 |
| [`evals/evals.json`](../../skills/marketing/analytics/evals/evals.json) | Analytics Skill 的评估场景和预期行为 |

## 7. 关联 Skill

[`prd`](prd.md)、`metrics-experiment`（planned）、[`pm-orchestrator`](pm-orchestrator.md)
