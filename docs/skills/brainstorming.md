# Brainstorming (`brainstorming`)

> 通过对话和可视化辅助，在需求不清或多方案取舍时帮助用户想清楚要做什么、为什么做，以及应该采用哪种方向。

| 维度 | 说明 |
|---|---|
| 分类 | 产品经理工作流 |
| 阶段 | 发现与方案探索 |
| 主要使用者 | 非产品经理、产品负责人、设计和研发 |
| 输出 | 澄清后的目标、约束、方案取舍和设计文档 |

## 1. 能力

先读已有上下文再提问；一次只推进一个关键问题；帮助用户描述目标、约束和取舍；对比多个方案；在进入实现前形成对设计和范围的共识。

## 2. 定位

**它负责：**

- 先读已有上下文再提问
- 一次只推进一个关键问题
- 帮助用户描述目标、约束和取舍
- 对比多个方案
- 在进入实现前形成对设计和范围的共识。

**它不负责：**

- 已有清晰需求时替代 PRD
- 直接做技术方案或代码实现
- 需要快速判断业务价值时的唯一工具
- 用开放式讨论拖延明确的小改动

## 3. 适用场景

- 想法很模糊，需要探索用户真正想要什么
- 存在多个产品方向，需要比较取舍
- 跨角色对目标或方案理解不一致
- 需要在写设计文档前进行结构化讨论

## 4. 示例

**用户输入：**

```text
我们想重做审批体验，但现在只有一个模糊方向，不确定应该优化表单、通知还是审批路径。先不要写代码，帮我梳理真正的问题和可选方案。
```

**Skill 的执行方式：**

1. 读取现有流程和用户反馈
2. 先复述已知信息
3. 一次提出一个高价值问题
4. 阶段性复述理解并邀请纠正
5. 比较多个方向及其代价
6. 形成设计文档或交由 product-brief 继续

**产出：**

讨论结论、方案比较，以及需要时生成的 `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 原始想法、已有上下文、用户反馈、约束和可选方案 |
| 输出 | 澄清后的目标、约束、方案取舍和设计文档 |
| 主要产物 | 视任务而定，通常是设计文档或产品 brief |

## 6. 文件结构

所有 Skill 都以 `SKILL.md` 为运行时入口；`assets/` 放模板，`references/` 放按需加载的参考文档，`scripts/` 放可执行辅助脚本。

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/product/brainstorming/SKILL.md) | 对话策略、提问方式、方案比较、设计文档和大小判断 |
| [`builder-check-prompt.md`](../../skills/product/brainstorming/builder-check-prompt.md) | 让独立 builder 检查设计文档是否足够可执行的提示词 |
| [`visual-companion.md`](../../skills/product/brainstorming/visual-companion.md) | 通过可视化和 mockup 辅助设计讨论的说明 |
| [`scripts/frame-template.html`](../../skills/product/brainstorming/scripts/frame-template.html) | 可视化伴侣的页面框架模板 |
| [`scripts/helper.js`](../../skills/product/brainstorming/scripts/helper.js) | 可视化伴侣的浏览器端辅助逻辑 |
| [`scripts/server.cjs`](../../skills/product/brainstorming/scripts/server.cjs) | 本地可视化伴侣服务 |
| [`scripts/start-server.sh`](../../skills/product/brainstorming/scripts/start-server.sh) | 启动可视化伴侣 |
| [`scripts/stop-server.sh`](../../skills/product/brainstorming/scripts/stop-server.sh) | 停止可视化伴侣 |

## 7. 关联 Skill

[`product-brief`](product-brief.md)、[`prd`](prd.md)、[`frontend-design`](frontend-design.md)
