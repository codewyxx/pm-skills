# Executing Plans (`executing-plans`)

> 在当前会话中按已批准的实施计划逐任务执行，并在每个任务完成后留下可检查的完成证据。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 实施执行 |
| 主要使用者 | 开发、技术负责人 |
| 输出 | 完成的代码、任务状态和验证证据 |

## 1. 能力

读取计划并确认上下文；一次只处理一个任务；按步骤写测试和实现；运行验证；记录完成状态；最后完成全量检查并进入分支收尾。

## 2. 定位

**它负责：**

- 读取计划并确认上下文
- 一次只处理一个任务
- 按步骤写测试和实现
- 运行验证
- 记录完成状态
- 最后完成全量检查并进入分支收尾。

**它不负责：**

- 没有批准计划时直接开始写代码
- 产品发现、产品策略或 PRD 编写
- 多子代理并行执行；这种情况使用 subagent-driven-development
- 替代代码审查和测试设计

## 3. 适用场景

- 已有详细实施计划，需要当前会话直接实现
- 没有子代理工具，或用户明确选择本会话内执行
- 任务之间有顺序依赖，需要逐个完成
- 需要保留每一步验证证据

## 4. 示例

**用户输入：**

```text
按照 docs/superpowers/plans/2026-10-30-batch-reminder.md 逐任务执行。每完成一个任务，运行指定测试并报告结果。
```

**Skill 的执行方式：**

1. 读取完整计划和项目上下文
2. 确认工作区和前置条件
3. 领取第一个任务
4. 按步骤执行并验证
5. 满足完成契约后标记任务
6. 重复直到全部任务完成
7. 执行最终检查和收尾

**产出：**

代码变更、计划中已完成的任务、测试和验证输出，以及交给分支收尾步骤的完成报告。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 已批准的实施计划、代码库、测试命令和项目约定 |
| 输出 | 完成的代码、任务状态和验证证据 |
| 主要产物 | 代码变更和计划执行状态 |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/executing-plans/SKILL.md) | 执行流程、任务循环、完成契约、最终检查和常见借口防范 |
| [`scripts/task-start`](../../skills/engineering/executing-plans/scripts/task-start) | 记录开始某个计划任务的状态辅助脚本 |
| [`scripts/task-done`](../../skills/engineering/executing-plans/scripts/task-done) | 记录任务完成状态和验证结果的辅助脚本 |

## 7. 关联 Skill

[`writing-plans`](writing-plans.md)、[`finishing-a-development-branch`](finishing-a-development-branch.md)、[`verification-before-completion`](verification-before-completion.md)
