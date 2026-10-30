# Test-Driven Development (`test-driven-development`)

> 使用 RED-GREEN-REFACTOR 循环实现功能或修复缺陷：先写失败测试，再写最小实现，最后重构。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 实现阶段的质量内建 |
| 主要使用者 | 开发 |
| 输出 | 测试和通过测试的实现代码 |

## 1. 能力

先写测试并确认失败；确认失败原因正确；写最小实现让测试通过；重构保持测试通过；用测试描述行为和边界。

## 2. 定位

**它负责：**

- 先写测试并确认失败
- 确认失败原因正确
- 写最小实现让测试通过
- 重构保持测试通过
- 用测试描述行为和边界。

**它不负责：**

- 替代测试策略、测试计划或探索性测试
- 替代验收测试和产品验收
- 先写实现再补测试
- 无法验证行为时用测试假象掩盖问题

## 3. 适用场景

- 实现新功能或修复 bug
- 需要可重复的行级质量反馈
- 需要防止回归
- 希望用测试驱动接口和行为设计

## 4. 示例

**用户输入：**

```text
实现批量提醒的发送结果统计。先写失败测试覆盖全部成功、部分成功和全部失败三种结果，再实现最小逻辑。
```

**Skill 的执行方式：**

1. 写一个最小失败测试
2. 运行并确认因预期原因失败
3. 写最小实现
4. 运行并确认通过
5. 重构
6. 补充边界和异常测试

**产出：**

新增或修改的测试、最小实现、重构后的代码和测试运行结果。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 需求、验收标准、现有测试框架和代码库约定 |
| 输出 | 测试和通过测试的实现代码 |
| 主要产物 | 测试代码和实现代码 |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/test-driven-development/SKILL.md) | RED-GREEN-REFACTOR、铁律、好测试标准、常见借口和验证清单 |
| [`writing-good-tests.md`](../../skills/engineering/test-driven-development/writing-good-tests.md) | 如何写能表达行为、边界和回归价值的好测试 |

## 7. 关联 Skill

[`systematic-debugging`](systematic-debugging.md)、[`verification-before-completion`](verification-before-completion.md)、[`writing-plans`](writing-plans.md)
