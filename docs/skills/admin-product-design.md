# Admin Product Design (`admin-product-design`)

> 面向 B 端、运营后台和内部工具的 Agent 规则包，把列表、表单、权限、状态、批量操作、导出、通知、菜单和排序等业务规则转成可执行的设计约束。

| 维度 | 说明 |
|---|---|
| 分类 | 产品设计规范 |
| 阶段 | 后台产品体验与业务规则设计 |
| 主要使用者 | 非产品经理、产品负责人、后台产品设计者 |
| 输出 | 后台业务规则、交互约束和验收标准 |

## 1. 能力

按任务加载相关 reference；为后台需求提供默认规则、边界条件、异常状态和验收标准；帮助非产品经理避免遗漏权限、状态、批量结果、导出和通知等后台常见问题。

## 2. 定位

**它负责：**

- 按任务加载相关 reference
- 为后台需求提供默认规则、边界条件、异常状态和验收标准
- 帮助非产品经理避免遗漏权限、状态、批量结果、导出和通知等后台常见问题。

**它不负责：**

- C 端营销页或纯视觉设计
- 技术架构、接口和数据库设计
- 替代 PRD 的完整需求文档
- 在没有业务上下文时自动发明公司规则

## 3. 适用场景

- 设计后台列表、搜索、筛选和分页
- 设计表单、权限矩阵或状态流转
- 设计批量导入、结果页和数据导出
- 设计后台菜单分类和权限资源码

## 4. 示例

**用户输入：**

```text
设计一个运营后台订单列表，需要按状态筛选、批量处理、导出、控制查看和导出权限，并给出异常和空状态。
```

**Skill 的执行方式：**

1. 读取 index 和 manifest，选择列表、权限、批量、导出、反馈相关 reference
2. 把默认规则映射到当前业务对象
3. 标出差异点和待确认阈值
4. 输出后台交互规则和验收标准
5. 交给 prd 或产品评审

**产出：**

通常作为 `03-experience.md` 或 `04-prd.md` 的一部分，包含列表、权限、状态、批量、导出、通知和异常规则。

## 5. 输入与输出

| 项目 | 说明 |
|---|---|
| 输入 | 后台业务场景、用户角色、业务规则、现有后台模式和阈值 |
| 输出 | 后台业务规则、交互约束和验收标准 |
| 主要产物 | `docs/product/<feature-slug>/03-experience.md` 或 `04-prd.md` |

## 6. 文件结构

所有 Skill 都以 `SKILL.md` 为运行时入口；`assets/` 放模板，`references/` 放按需加载的参考文档，`scripts/` 放可执行辅助脚本。

| 文件 | 目的 |
|---|---|
| [`SKILL.md`](../../skills/product/admin-product-design/SKILL.md) | 触发条件、加载策略、全局护栏和 PRD 输出要求 |
| [`references/index.md`](../../skills/product/admin-product-design/references/index.md) | 按任务路由 reference，说明常见组合和 PRD 必须输出 |
| [`references/manifest.yaml`](../../skills/product/admin-product-design/references/manifest.yaml) | 机器可读的触发词、reference 文件和关联关系 |
| [`references/01-list-query.md`](../../skills/product/admin-product-design/references/01-list-query.md) | 列表排序、分页、搜索、筛选和下钻 |
| [`references/02-forms-validation.md`](../../skills/product/admin-product-design/references/02-forms-validation.md) | 表单必填、校验时机、错误文案、提交和草稿 |
| [`references/03-feedback-states.md`](../../skills/product/admin-product-design/references/03-feedback-states.md) | 空状态、加载、错误、成功反馈和确认框 |
| [`references/04-status-actions-batch.md`](../../skills/product/admin-product-design/references/04-status-actions-batch.md) | 状态机、操作按钮、批量操作、导入和结果页 |
| [`references/05-permissions.md`](../../skills/product/admin-product-design/references/05-permissions.md) | 权限点拆分、角色矩阵、默认策略和数据范围 |
| [`references/06-display-and-media.md`](../../skills/product/admin-product-design/references/06-display-and-media.md) | 日期、数字、金额、单位、图片、视频和上传 |
| [`references/07-notifications.md`](../../skills/product/admin-product-design/references/07-notifications.md) | 通知分级、渠道、触发要素、文案和频控 |
| [`references/08-export.md`](../../skills/product/admin-product-design/references/08-export.md) | 导出范围、文件字段、权限、审计和异步任务 |
| [`references/09-admin-menu.md`](../../skills/product/admin-product-design/references/09-admin-menu.md) | 后台菜单分类、命名、资源码和新增菜单流程 |
| [`references/10-weighted-sorting.md`](../../skills/product/admin-product-design/references/10-weighted-sorting.md) | 多因子权重、计分方式、配置界面和边界 |

## 7. 关联 Skill

[`prd`](prd.md)、[`pm-orchestrator`](pm-orchestrator.md)、[`frontend-design`](frontend-design.md)
