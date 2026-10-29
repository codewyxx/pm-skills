# PM Skills

> 一组按工作流分组的 Agent Skills，面向产品管理、工程设计、界面设计与营销分析。

本仓库整理了 **14 个**可直接被支持 Agent Skills 的工具读取的技能。每个 Skill 都是一个包含 `SKILL.md` 的独立目录，相关脚本、模板和参考文档均随 Skill 保留。

## 目录结构

```text
pm-skills/
└── skills/
    ├── product/
    │   ├── prd/
    │   ├── brainstorming/
    │   ├── writing-plans/
    │   └── admin-product-design/
    ├── engineering/
    │   ├── executing-plans/
    │   ├── subagent-driven-development/
    │   ├── using-git-worktrees/
    │   ├── finishing-a-development-branch/
    │   ├── requesting-code-review/
    │   ├── systematic-debugging/
    │   ├── test-driven-development/
    │   └── verification-before-completion/
    ├── design/
    │   └── frontend-design/
    └── marketing/
        └── analytics/
```

## Skill 清单

### 产品与规划

| Skill | 用途 |
|---|---|
| [`prd`](skills/product/prd/SKILL.md) | 生成结构化、可评审的产品需求文档（PRD） |
| [`brainstorming`](skills/product/brainstorming/SKILL.md) | 在开始创作或实现前，澄清目标、约束和可行方案 |
| [`writing-plans`](skills/product/writing-plans/SKILL.md) | 将已确认的需求和设计拆成可执行、可验证的实施计划 |
| [`admin-product-design`](skills/product/admin-product-design/SKILL.md) | B 端与运营后台的产品设计规则包：列表、表单、权限、状态流转、批量操作、导出、通知、菜单与排序 |

### 工程流程

| Skill | 用途 |
|---|---|
| [`executing-plans`](skills/engineering/executing-plans/SKILL.md) | 按任务逐项执行实施计划并维护进度 |
| [`subagent-driven-development`](skills/engineering/subagent-driven-development/SKILL.md) | 用独立子代理实现任务，并逐任务进行检查和复核 |
| [`using-git-worktrees`](skills/engineering/using-git-worktrees/SKILL.md) | 使用 Git worktree 隔离功能开发，保持主工作区干净 |
| [`finishing-a-development-branch`](skills/engineering/finishing-a-development-branch/SKILL.md) | 完成开发分支的验证、清理和合并准备 |
| [`requesting-code-review`](skills/engineering/requesting-code-review/SKILL.md) | 发起结构化代码审查，聚焦真实风险和回归 |
| [`systematic-debugging`](skills/engineering/systematic-debugging/SKILL.md) | 通过根因分析、假设验证和最小复现系统性排查缺陷 |
| [`test-driven-development`](skills/engineering/test-driven-development/SKILL.md) | 使用测试先行（TDD）工作流实现功能和修复缺陷 |
| [`verification-before-completion`](skills/engineering/verification-before-completion/SKILL.md) | 在宣称工作完成前运行验证并检查证据 |

### 设计

| Skill | 用途 |
|---|---|
| [`frontend-design`](skills/design/frontend-design/SKILL.md) | 创建有辨识度、视觉统一且符合使用场景的前端界面 |

### 营销与分析

| Skill | 用途 |
|---|---|
| [`analytics`](skills/marketing/analytics/SKILL.md) | 规划、配置、审计和改进分析埋点，覆盖 GA4、GTM、事件设计等场景 |

### Agent 运行时参考

`admin-product-design` 采用渐进式披露：

- `SKILL.md` 只负责触发条件、加载策略和全局约束；
- `references/index.md` 按任务路由到具体规范；
- `references/manifest.yaml` 提供机器可读的触发词和引用关系；
- 具体规范按列表、表单、反馈、状态与批量操作、权限、展示与媒体、通知、导出、后台菜单、加权排序拆分。

每条规则使用 `MUST`、`DEFAULT`、`PENDING` 标记。Agent 只加载当前任务匹配的 reference，避免把全部规范一次性注入上下文。原始业务文档不包含在本仓库中。

## 安装

### 1. 克隆仓库

```bash
git clone https://github.com/codewyxx/pm-skills.git
```

### 2. 安装到 Agent 的 Skill 目录

目录中的 `product`、`engineering` 等分组仅用于本仓库归类。安装时需要将各分组下的 Skill 目录平铺到 Agent 的 skill 根目录。

**Windows PowerShell**

```powershell
$src = ".\pm-skills\skills"
$dst = "$HOME\.agents\skills"
New-Item -ItemType Directory -Force -Path $dst | Out-Null

Get-ChildItem $src -Directory | ForEach-Object {
    Get-ChildItem $_.FullName -Directory | ForEach-Object {
        Copy-Item $_.FullName -Destination $dst -Recurse -Force
    }
}
```

**macOS / Linux**

```bash
mkdir -p ~/.agents/skills
cp -R pm-skills/skills/*/* ~/.agents/skills/
```

如果使用 Claude Code，可以将目标目录换成 `~/.claude/skills`；如果使用其他 Agent，请替换为该 Agent 对应的 skills 目录。

## 使用

支持用户显式调用 Skill 的 Agent 可以直接使用：

```text
/brainstorming
/prd
/writing-plans
/admin-product-design
/frontend-design
/analytics
```

支持 `skill` 工具的 Agent 也可以通过精确的 Skill 名称加载，例如：

```text
brainstorming
prd
writing-plans
admin-product-design
```

## 上游来源

本仓库汇集多个来源。除 `admin-product-design` 外，Skill 内容基本保留上游原文；为说明联动，`prd` 和 `frontend-design` 增加了指向 `admin-product-design` 的说明段。主要来源如下：

| 上游仓库 | 本仓库中的 Skill |
|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | `brainstorming`、`writing-plans`、`executing-plans`、`subagent-driven-development`、`using-git-worktrees`、`finishing-a-development-branch`、`requesting-code-review`、`systematic-debugging`、`test-driven-development`、`verification-before-completion` |
| [github/awesome-copilot](https://github.com/github/awesome-copilot) | `prd` |
| [anthropics/skills](https://github.com/anthropics/skills) | `frontend-design` |
| [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | `analytics` |
| 本仓库整理（基于团队产品设计规范脱敏改写） | `admin-product-design` |

### 关于 `analytics`

skills.sh 上的原始页面 slug 为 `analytics-tracking`。上游仓库在 v2.0 中已将该 Skill 正式改名为 `analytics`，本仓库使用当前名称和当前内容。

## 许可与归属

各 Skill 的版权和许可归其上游作者所有。使用、修改或再分发前，请查看对应上游仓库的许可证。

`frontend-design` 的 `LICENSE.txt` 已随 Skill 一并保留在：

```text
skills/design/frontend-design/LICENSE.txt
```

## 维护

新增 Skill 时，建议：

1. 按用途放入 `skills/<category>/<skill-name>/`；
2. 确保目录中包含有效的 `SKILL.md`，且 frontmatter 至少包含 `name` 和 `description`；
3. 保留该 Skill 需要的脚本、模板和参考资料；
4. 在 README 的 Skill 清单和上游来源中补充说明。
