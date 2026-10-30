# PM Skills 文档

> 每个 Skill 的能力、定位、适用场景、示例、输入输出和文件结构说明。

## 导航

- [全部 Skill](#全部-skill)
- [按问题选择 Skill](#按问题选择-skill)
- [Skill 包结构](#skill-包结构)
- [产品产物结构](artifacts.md)
- [返回仓库首页](../README.md)

## 先理解三类文档

| 文档类型 | 位置 | 作用 |
|---|---|---|
| Skill 运行入口 | `skills/<category>/<skill>/SKILL.md` | Agent 实际加载的触发条件、工作流、规则和输出契约 |
| Skill 参考文档 | `skills/<category>/<skill>/references/` | 按需加载的细则、检查表、领域规则和示例 |
| 业务产物文档 | `docs/product/<feature-slug>/` | 产品经理工作中产生的 brief、strategy、experience、PRD、metrics 和 review |

本目录的 `docs/skills/*.md` 是面向人的说明文档，不参与 Agent 运行；运行时以各 Skill 的 `SKILL.md` 和 `references/` 为准。

## 全部 Skill

### 产品经理工作流

| Skill | 定位 | 典型场景 |
|---|---|---|
| [`pm-orchestrator`](skills/pm-orchestrator.md) | PM 工作总入口，按规模路由产品工作和门禁 | 收到模糊需求，需要安排产品文档和交接 |
| [`product-brief`](skills/product-brief.md) | 一页产品简报，判断问题、价值、MVP 和 go/no-go | 只有一个功能想法，需要判断值不值得做 |
| [`prd`](skills/prd.md) | 把已确认的方向展开为结构化 PRD | brief 已批准，需要写需求和验收标准 |
| [`brainstorming`](skills/brainstorming.md) | 通过对话探索问题、约束和方案取舍 | 想法模糊，或存在多个产品方向 |
| [`admin-product-design`](skills/admin-product-design.md) | B 端后台产品规则包 | 列表、表单、权限、状态、批量、导出、通知、菜单 |

### 计划与工程执行

| Skill | 定位 | 典型场景 |
|---|---|---|
| [`writing-plans`](skills/writing-plans.md) | 把批准的设计拆成文件级实施计划 | 需求和技术方案已明确，准备开发 |
| [`executing-plans`](skills/executing-plans.md) | 在当前会话逐任务执行实施计划 | 需要按计划顺序实现并验证 |
| [`subagent-driven-development`](skills/subagent-driven-development.md) | 用实现子代理和独立审查子代理执行计划 | 多个独立任务，需要隔离上下文和任务级复核 |
| [`using-git-worktrees`](skills/using-git-worktrees.md) | 创建隔离开发工作区 | 功能开发需要独立 worktree 和干净基线 |
| [`finishing-a-development-branch`](skills/finishing-a-development-branch.md) | 验证并选择合并、PR、保留或丢弃分支 | 实现完成，准备集成 |
| [`requesting-code-review`](skills/requesting-code-review.md) | 发起结构化代码审查 | 准备合并前需要独立检查回归风险 |
| [`systematic-debugging`](skills/systematic-debugging.md) | 先定位根因再修复 | 出现 bug、测试失败或异常行为 |
| [`test-driven-development`](skills/test-driven-development.md) | 用 RED-GREEN-REFACTOR 实现代码 | 实现功能或修 bug，需要测试先行 |
| [`verification-before-completion`](skills/verification-before-completion.md) | 用验证证据代替完成断言 | 准备提交、发 PR 或宣布完成 |

### 界面与测量

| Skill | 定位 | 典型场景 |
|---|---|---|
| [`frontend-design`](skills/frontend-design.md) | 有意图的视觉方向和前端实现 | 新页面需要辨识度，避免模板化设计 |
| [`analytics`](skills/analytics.md) | 指标、事件、GA4/GTM 和 Tracking Plan | 新功能需要埋点、审计或测量方案 |

## 按问题选择 Skill

| 你遇到的问题 | 先使用 | 然后使用 |
|---|---|---|
| 只有一个模糊想法 | `product-brief` | `prd`、`admin-product-design` |
| 不知道应该写哪些产品文档 | `pm-orchestrator` | 按 route 调用 `product-brief` 等 |
| 需求和用户价值还不清楚 | `brainstorming` 或 `product-brief` | `prd` |
| 需要写后台列表、表单、权限或导出 | `admin-product-design` | `prd` |
| 已有 brief，需要完整需求 | `prd` | `writing-plans` |
| 已有设计和需求，准备开发 | `writing-plans` | `executing-plans` 或 `subagent-driven-development` |
| 需要独立代码审查 | `requesting-code-review` | `finishing-a-development-branch` |
| 出现 bug 或测试失败 | `systematic-debugging` | `test-driven-development` |
| 准备宣布完成 | `verification-before-completion` | `finishing-a-development-branch` |
| 需要埋点或指标方案 | `analytics` | `prd`、`05-metrics.md` |

## Skill 包结构

```text
skills/<category>/<skill>/
├── SKILL.md             # Agent 运行时入口
├── references/          # 按需加载的规则、清单、示例
├── assets/              # 可直接复用的模板
├── scripts/             # 可执行辅助脚本
├── *.prompt.md          # 子代理或审查提示词
└── manifest.yaml        # 机器可读路由配置（如适用）
```

| 文件类型 | 目的 | 何时加载 |
|---|---|---|
| `SKILL.md` | 定义触发条件、工作流、护栏和输出契约 | 命中 Skill 时 |
| `references/*.md` | 提供领域细则、检查表、决策规则和示例 | 按任务相关性选择性加载 |
| `assets/*.md` | 提供标准输出模板 | 生成产物时 |
| `scripts/*` | 执行辅助动作，如任务状态、审查打包、启动可视化服务 | 执行对应动作时 |
| `*.prompt.md` | 给子代理、审查者或实现者的角色提示词 | 派发子代理时 |
| `manifest.yaml` | 机器可读的触发词、reference 路由和关联关系 | 需要自动路由时 |

## 每个 Skill 页面包含什么

每个 `docs/skills/<name>.md` 统一包含：

1. 能力
2. 定位与不负责的范围
3. 适用场景
4. 输入示例和执行方式
5. 输入与输出
6. 文件结构及每个文件的目的
7. 关联 Skill

## 运行机制

Agent 不需要一次加载整个仓库。典型流程是：

```text
用户请求
  → 匹配 SKILL.md
  → 读取必要的 references
  → 使用 assets 生成产物
  → 写入 docs/product 或项目约定路径
  → 通过输出契约和门禁检查
```
