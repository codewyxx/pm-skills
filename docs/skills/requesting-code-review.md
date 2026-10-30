# Requesting Code Review (`requesting-code-review`)

> 在任务完成、功能实现或准备合并前，准备结构化代码审查请求，让审查者重点关注需求一致性、回归风险和验证证据。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 代码审查 |
| 主要使用者 | 开发、技术负责人 |
| 输出 | 代码审查请求和审查发现 |

## 1. 能力

判断何时需要审查；整理变更范围、需求、测试和风险；提供 reviewer 提示词；明确要求发现问题而不是泛泛确认；跟踪审查结论。

## 2. 定位

**它负责：**

- 判断何时需要审查
- 整理变更范围、需求、测试和风险
- 提供 reviewer 提示词
- 明确要求发现问题而不是泛泛确认
- 跟踪审查结论。

**它不负责：**

- 替代自动化测试
- 在代码尚未实现时执行
- 替代产品验收
- 把代码审查当作合并前的形式步骤

## 3. 适用场景

- 完成一个任务或主要功能，需要独立审查
- 准备合并前需要检查回归风险
- 需要让审查者理解需求背景和验证方式
- 需要系统化收集审查发现

## 4. 示例

**用户输入：**

```text
功能已完成，测试通过。请基于这次变更、对应 PRD、测试证据和风险点发起代码审查，重点寻找真实缺陷和回归。
```

**Skill 的执行方式：**

1. 确认变更范围和需求对应关系
2. 准备测试证据和已知风险
3. 生成结构化审查请求
4. 使用 code-reviewer.md 作为审查提示
5. 收集发现并区分阻塞与非阻塞
6. 进入修复或合并流程

**产出：**

变更摘要、需求映射、验证证据、审查提示和按严重程度整理的问题列表。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 代码 diff、需求、设计、测试结果、已知风险和审查范围 |
| 输出 | 代码审查请求和审查发现 |
| 主要产物 | 代码审查记录 |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/requesting-code-review/SKILL.md) | 何时审查、如何组织审查请求、示例和常见借口 |
| [`code-reviewer.md`](../../skills/engineering/requesting-code-review/code-reviewer.md) | 给代码审查者的结构化提示词和检查视角 |

## 7. 关联 Skill

[`verification-before-completion`](verification-before-completion.md)、[`finishing-a-development-branch`](finishing-a-development-branch.md)、[`subagent-driven-development`](subagent-driven-development.md)
