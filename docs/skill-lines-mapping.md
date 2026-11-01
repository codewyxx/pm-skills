# 三条技能线 × Skill 映射

> AI 时代产品功能设计的能力地图：按「与 AI 的关系」把能力分为三条线，每条线对应一类 Skill 用法。
> 用途：团队培训、个人加点规划、Skill 选型速查。

## 一、框架

| 技能线 | 核心问题 | 包含能力 | 定位 |
|---|---|---|---|
| **L1 · 交给 AI 加速**（offload） | 什么事直接外包给 AI？ | 文档撰写、原型绘制、资料整理、数据汇总、会议纪要 | 不是不重要，而是**不再是护城河**，做快即可 |
| **L2 · 和 AI 一起变强**（co-train） | 什么能力越用 AI 越强？ | 提问和拆解、整理项目资料、审校和判断 | **用得越多，变得越快** |
| **L3 · 只能自己练**（amplify） | 什么能力 AI 无法替代？ | 用户洞察、取舍、影响力、为结果负责 | **真正的天赋点**，AI 只能放大 |

**加点建议**：把 L1 省下的时间投到 L3——每周少花半天写文档，多花半天见用户。

## 二、本仓库 Skill 映射

### L1 · 直接替代执行

| 能力 | Skill | 干什么用 |
|---|---|---|
| 文档撰写 | [`prd`](../skills/product/prd/SKILL.md) | 零散想法 → 结构完整、可评审的 PRD |

### L2 · 用 Skill 的过程就是陪练

| 能力 | Skill | 练的是什么 |
|---|---|---|
| 提问和拆解 | [`brainstorming`](../skills/product/brainstorming/SKILL.md) | 苏格拉底式追问，把模糊想法逼成清晰问题 |
| 提问和拆解 | [`product-brief`](../skills/product/product-brief/SKILL.md) | 一句话需求 →「问题-用户-结果-MVP」可测试简报 |
| 工作路由 | [`pm-orchestrator`](../skills/product/pm-orchestrator/SKILL.md) | 按需求规模路由流程，强制过质量门禁 |
| 拆解落地 | [`writing-plans`](../skills/product/writing-plans/SKILL.md) → [`executing-plans`](../skills/engineering/executing-plans/SKILL.md) | 需求 → 可执行的多步实施计划 |
| 审校和判断 | [`admin-product-design`](../skills/product/admin-product-design/SKILL.md) | B 端规格校验清单：AI 给 70 分，它告诉你差的 30 分在哪 |
| 审校和判断 | [`requesting-code-review`](../skills/engineering/requesting-code-review/SKILL.md) / [`verification-before-completion`](../skills/engineering/verification-before-completion/SKILL.md) | 交付前自查，证据先于断言 |
| 测试排障 | [`systematic-debugging`](../skills/engineering/systematic-debugging/SKILL.md) | 假设 → 验证 → 最小修复的排障闭环 |
| 开发规范 | [`test-driven-development`](../skills/engineering/test-driven-development/SKILL.md) / [`using-git-worktrees`](../skills/engineering/using-git-worktrees/SKILL.md) / [`finishing-a-development-branch`](../skills/engineering/finishing-a-development-branch/SKILL.md) / [`subagent-driven-development`](../skills/engineering/subagent-driven-development/SKILL.md) | 超级个体在开发、测试环节的规范护栏 |
| 界面表达 | [`frontend-design`](../skills/design/frontend-design/SKILL.md) | 有辨识度的界面，而非模板化默认 |
| 效果度量 | [`analytics`](../skills/marketing/analytics/SKILL.md) | 埋点与指标，为结果负责提供证据 |

### L3 · 没有 Skill 能替代，只能放大

| 能力 | 为什么没有 Skill | 可被什么辅助 |
|---|---|---|
| 用户洞察 | 替你去现场的 Skill 不存在 | 案头研究给背景、行为数据给线索——**原话只能自己听** |
| 取舍 | 拍板责任无法外包 | `product-brief` 的「备选方案与权衡」字段，逼你写清**不做什么、为什么** |
| 影响力 | 信任无法自动化 | 精良的文档与演示是放大器，不是替代品 |
| 为结果负责 | 结果只能人扛 | `analytics` 定指标、`verification-before-completion` 拿证据 |

## 三、落地工作流（产品功能设计层）

```
一句话需求 → brainstorming 发散 → product-brief 收敛 → prd 产出 → admin-product-design 校验 → 交付开发
   入口          L2 提问拆解        L2 收敛判断        L1 执行产出      L2 审校判断          人站两端做判断，AI 在中间做执行
```

## 四、配套资产

- [业务本体模板](ontology-template.md)：把团队先例抽象成可迁移的语义模型（实体/状态机/口径/权限/模式）
- [先例文档模板](precedent-template.md)：先例结构 + 语义卡片 + 脱敏示例——先例喂本体，本体反哺先例去重
