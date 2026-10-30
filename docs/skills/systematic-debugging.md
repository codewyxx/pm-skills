# Systematic Debugging (`systematic-debugging`)

> 在提出修复前，通过复现、证据收集、假设验证和根因追踪系统性排查 bug、测试失败和异常行为。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 缺陷诊断 |
| 主要使用者 | 开发、测试、技术负责人 |
| 输出 | 根因说明、最小修复和验证证据 |

## 1. 能力

稳定复现问题；收集日志和证据；形成可证伪假设；用最小实验验证；追踪根因；设计防御性修复；添加回归验证。

## 2. 定位

**它负责：**

- 稳定复现问题
- 收集日志和证据
- 形成可证伪假设
- 用最小实验验证
- 追踪根因
- 设计防御性修复
- 添加回归验证。

**它不负责：**

- 功能需求定义和方案设计
- 没有证据时猜测修复
- 替代 TDD 或代码审查
- 把所有异常都归因于环境问题

## 3. 适用场景

- 出现 bug、测试失败或非预期行为
- 修复后问题反复出现
- 需要定位测试污染、时序问题或深层根因
- 需要判断问题来自代码、数据、环境还是外部依赖

## 4. 示例

**用户输入：**

```text
批量提醒在测试环境偶发重复发送。请先复现并定位根因，不要直接加去重补丁。
```

**Skill 的执行方式：**

1. 确认复现条件和影响范围
2. 收集日志、请求和状态证据
3. 列出候选根因并逐一验证
4. 用最小实验证伪假设
5. 找到根因后设计修复
6. 增加回归测试并验证

**产出：**

复现步骤、证据、根因、修复方案、回归测试和验证结果。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 错误现象、复现条件、日志、代码、测试和环境信息 |
| 输出 | 根因说明、最小修复和验证证据 |
| 主要产物 | 缺陷诊断报告和修复验证 |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/systematic-debugging/SKILL.md) | 复现、证据、假设、根因追踪、修复和验证流程 |
| [`condition-based-waiting.md`](../../skills/engineering/systematic-debugging/condition-based-waiting.md) | 用条件等待替代固定 sleep 的调试原则 |
| [`condition-based-waiting-example.ts`](../../skills/engineering/systematic-debugging/condition-based-waiting-example.ts) | 条件等待的实际示例 |
| [`defense-in-depth.md`](../../skills/engineering/systematic-debugging/defense-in-depth.md) | 多层防御和验证的设计方法 |
| [`root-cause-tracing.md`](../../skills/engineering/systematic-debugging/root-cause-tracing.md) | 从症状向上游追踪根因的方法 |
| [`find-polluter.sh`](../../skills/engineering/systematic-debugging/find-polluter.sh) | 定位测试污染源的辅助脚本 |
| [`test-academic.md`](../../skills/engineering/systematic-debugging/test-academic.md) | 技能行为评估场景：学术式压力测试 |
| [`test-pressure-1.md`](../../skills/engineering/systematic-debugging/test-pressure-1.md) | 技能行为评估场景：压力测试 1 |
| [`test-pressure-2.md`](../../skills/engineering/systematic-debugging/test-pressure-2.md) | 技能行为评估场景：压力测试 2 |
| [`test-pressure-3.md`](../../skills/engineering/systematic-debugging/test-pressure-3.md) | 技能行为评估场景：压力测试 3 |
| [`CREATION-LOG.md`](../../skills/engineering/systematic-debugging/CREATION-LOG.md) | 技能创建背景、设计取舍和演进记录 |

## 7. 关联 Skill

[`test-driven-development`](test-driven-development.md)、[`verification-before-completion`](verification-before-completion.md)、[`requesting-code-review`](requesting-code-review.md)
