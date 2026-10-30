# Subagent-Driven Development (`subagent-driven-development`)

> 把独立任务交给实现子代理，并由独立审查子代理逐任务复核，适合需要隔离上下文和多次质量检查的计划执行。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 实施执行与独立复核 |
| 主要使用者 | 开发、技术负责人 |
| 输出 | 实现结果、逐任务审查记录和最终分支复核 |

## 1. 能力

准备任务上下文；按依赖分批派发实现者；处理实现报告；派发任务审查者；执行修复循环；在最后进行整分支复核；保留无法验证事项和恢复状态。

## 2. 定位

**它负责：**

- 准备任务上下文
- 按依赖分批派发实现者
- 处理实现报告
- 派发任务审查者
- 执行修复循环
- 在最后进行整分支复核
- 保留无法验证事项和恢复状态。

**它不负责：**

- 任务很小或高度耦合，拆子代理会增加成本
- 没有子代理能力的环境
- 没有可执行计划时直接派发
- 用子代理替代产品判断和需求定义

## 3. 适用场景

- 计划包含多个相对独立的任务
- 希望每个任务由新上下文实现、由新审查者复核
- 长任务需要可恢复、可分批执行
- 需要整分支级别最终审查

## 4. 示例

**用户输入：**

```text
按已批准计划执行，每个任务派一个新实现者，再由独立审查者检查。发现需要修复时继续同一个任务，全部完成后做整分支复核。
```

**Skill 的执行方式：**

1. 做 preflight，确认计划和依赖
2. 为任务生成 task brief
3. 派发 implementer
4. 接收报告并判断完成情况
5. 派发 task reviewer
6. 执行 fix loop
7. 完成所有任务后进行 final review

**产出：**

代码变更、任务包、审查报告、修复记录和 final review 结论。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 批准的实施计划、代码库、测试命令、子代理能力和任务风险信息 |
| 输出 | 实现结果、逐任务审查记录和最终分支复核 |
| 主要产物 | 代码变更、task brief、review package、final review |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/subagent-driven-development/SKILL.md) | 子代理执行流程、模型选择、任务循环、审查和最终复核 |
| [`implementer-prompt.md`](../../skills/engineering/subagent-driven-development/implementer-prompt.md) | 派发给实现子代理的任务提示词 |
| [`task-reviewer-prompt.md`](../../skills/engineering/subagent-driven-development/task-reviewer-prompt.md) | 派发给任务审查者的提示词 |
| [`re-review-prompt.md`](../../skills/engineering/subagent-driven-development/re-review-prompt.md) | 修复后再次审查的提示词 |
| [`references/batching.md`](../../skills/engineering/subagent-driven-development/references/batching.md) | 如何把独立任务分批派发 |
| [`references/cannot-verify.md`](../../skills/engineering/subagent-driven-development/references/cannot-verify.md) | 无法验证某项声明时的处理方式 |
| [`references/final-review.md`](../../skills/engineering/subagent-driven-development/references/final-review.md) | 整分支最终审查流程 |
| [`references/fix-loop.md`](../../skills/engineering/subagent-driven-development/references/fix-loop.md) | 审查发现问题后的修复循环 |
| [`references/handling-reports.md`](../../skills/engineering/subagent-driven-development/references/handling-reports.md) | 处理实现者报告和异常状态 |
| [`references/preflight.md`](../../skills/engineering/subagent-driven-development/references/preflight.md) | 派发前的环境和计划检查 |
| [`references/resuming.md`](../../skills/engineering/subagent-driven-development/references/resuming.md) | 中断后恢复任务执行 |
| [`scripts/review-package`](../../skills/engineering/subagent-driven-development/scripts/review-package) | 打包审查所需上下文 |
| [`scripts/sdd-workspace`](../../skills/engineering/subagent-driven-development/scripts/sdd-workspace) | 准备子代理开发工作区 |
| [`scripts/task-brief`](../../skills/engineering/subagent-driven-development/scripts/task-brief) | 生成单个任务的执行简报 |

## 7. 关联 Skill

[`writing-plans`](writing-plans.md)、[`requesting-code-review`](requesting-code-review.md)、[`finishing-a-development-branch`](finishing-a-development-branch.md)
