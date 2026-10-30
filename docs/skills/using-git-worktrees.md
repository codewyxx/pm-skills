# Using Git Worktrees (`using-git-worktrees`)

> 在功能开发前创建隔离工作区，优先使用原生 worktree 工具，必要时回退到 git worktree，并验证干净基线。

| 维度 | 说明 |
|---|---|
| 分类 | 计划与工程执行 |
| 阶段 | 开发环境隔离 |
| 主要使用者 | 开发、技术负责人 |
| 输出 | 隔离工作区、基线验证结果和执行说明 |

## 1. 能力

检测当前是否已隔离；选择 worktree 位置；创建设置项目依赖；运行基线测试；报告工作区路径和状态。

## 2. 定位

**它负责：**

- 检测当前是否已隔离
- 选择 worktree 位置
- 创建设置项目依赖
- 运行基线测试
- 报告工作区路径和状态。

**它不负责：**

- 替代分支规划或代码审查
- 功能完成后决定合并或 PR；使用 finishing-a-development-branch
- 不适合所有小改动，简单任务可以直接在主工作区完成
- 自动清理用户未授权的工作区

## 3. 适用场景

- 需要在不污染主工作区的情况下开发功能
- 准备执行实施计划，需要独立分支环境
- 多个任务并行但需要隔离
- 需要在开始前确认基线测试状态

## 4. 示例

**用户输入：**

```text
开始批量提醒功能前，创建一个隔离 worktree，完成依赖安装，并确认基线测试通过。
```

**Skill 的执行方式：**

1. 检测是否已在隔离 worktree
2. 优先使用原生 worktree 工具
3. 否则创建 git worktree
4. 安装项目依赖并完成项目设置
5. 运行基线测试
6. 报告路径、命令和基线结果

**产出：**

worktree 路径、分支、依赖安装状态、基线测试结果和进入实施阶段的说明。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 仓库、分支策略、项目设置命令、测试命令和工作区位置偏好 |
| 输出 | 隔离工作区、基线验证结果和执行说明 |
| 主要产物 | 隔离 worktree 和基线报告 |

## 6. 文件结构

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/engineering/using-git-worktrees/SKILL.md) | 隔离检测、原生工具优先、git worktree 回退、项目设置和基线验证 |

## 7. 关联 Skill

[`executing-plans`](executing-plans.md)、[`subagent-driven-development`](subagent-driven-development.md)、[`finishing-a-development-branch`](finishing-a-development-branch.md)
