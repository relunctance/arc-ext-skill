---
name: arc-ext-skill
description: Arc 技能索引路由器 - 接收任何架构任务，智能推荐最合适的 skill 并执行
version: 2.0.0
hermes:
  auto_route: true
---

# Arc Ext Skill - 智能技能路由器

## ⚡ 快速路由（必读）

### 任务 → Skill 速查

| 你的任务（说人话） | → 推荐 Skill | 直接调用 |
|------------------|-------------|---------|
| "设计系统架构" | c4-context | `hermes -p arc -s c4-context` |
| "设计容器架构" | c4-container | `hermes -p arc -s c4-container` |
| "设计后端架构" | backend-architect | `hermes -p arc -s backend-architect` |
| "设计数据库" | database-architect | `hermes -p arc -s database-architect` |
| "架构评审" | bmad-architect | `hermes -p arc -s bmad-architect` |
| "设计组件" | c4-component | `hermes -p arc -s c4-component` |
| "前端架构" | frontend-developer | `hermes -p arc -s frontend-developer` |
| "SQL 性能" | sql-pro | `hermes -p arc -s sql-pro` |
| "GraphQL 方案" | graphql-architect | `hermes -p arc -s graphql-architect` |
| "事件驱动" | event-sourcing-architect | `hermes -p arc -s event-sourcing-architect` |
| "代码架构" | c4-code | `hermes -p arc -s c4-code` |
| "UI/UX" | ui-ux-designer | `hermes -p arc -s ui-ux-designer` |
| "无障碍" | accessibility-specialist | `hermes -p arc -s accessibility-specialist` |
| "写规划文档" | writing-plans | `hermes -p arc -s writing-plans` |

### 一句话触发规则

```
任务包含...         → 直接路由到...
------------------------------------------------------------
"架构"、"系统设计"、"上下文" → c4-context
"容器"、"docker"、"k8s" → c4-container
"后端"、"api"、"服务" → backend-architect
"数据库"、"db"、"存储" → database-architect
"评审"、"review"、"检查" → bmad-architect
"组件"、"module" → c4-component
"前端"、"react"、"vue" → frontend-developer
"sql"、"查询"、"索引" → sql-pro
"graphql" → graphql-architect
"事件"、"event"、"cqrs" → event-sourcing-architect
"代码级"、"实现" → c4-code
"ui"、"ux"、"界面" → ui-ux-designer
"无障碍"、"a11y"、"wcag" → accessibility-specialist
"规划"、"plan"、"文档" → writing-plans
```

## 🔀 智能路由决策树

```
收到架构任务
    │
    ├─ 包含 "架构" / "系统设计" / "上下文"
    │   └─→ c4-context（上下文建模）
    │       ├─ "容器" / "docker" / "k8s" → c4-container
    │       └─ "组件" / "module" → c4-component
    │
    ├─ 包含 "后端" / "api" / "服务"
    │   └─→ backend-architect
    │       ├─ "graphql" → graphql-architect
    │       └─ "事件" / "cqrs" → event-sourcing-architect
    │
    ├─ 包含 "数据库" / "db" / "存储"
    │   └─→ database-architect
    │       └─ "sql" / "索引" → sql-pro
    │
    ├─ 包含 "评审" / "review"
    │   └─→ bmad-architect
    │
    ├─ 包含 "前端" / "react" / "vue"
    │   └─→ frontend-developer
    │
    ├─ 包含 "ui" / "ux" / "界面"
    │   └─→ ui-ux-designer
    │
    ├─ 包含 "无障碍" / "a11y" / "wcag"
    │   └─→ accessibility-specialist
    │
    └─ 包含 "规划" / "plan" / "文档"
        └─→ writing-plans
```

## 📋 技能地图

| Skill | TL;DR | 级别 | 触发关键词 |
|-------|-------|------|-----------|
| c4-context | C4模型上下文建模：系统边界、依赖关系 | P0 | 架构、系统设计、上下文 |
| c4-container | C4模型容器设计：应用、进程、数据 | P0 | 容器、docker、k8s |
| backend-architect | 后端架构决策：API设计、数据处理 | P0 | 后端、api、服务 |
| database-architect | 数据库架构：schema、索引、主从 | P0 | 数据库、db、存储 |
| bmad-architect | 架构评审：方案评估、风险识别 | P0 | 评审、review |
| c4-component | C4模型组件设计：模块、类、接口 | P1 | 组件、module |
| frontend-developer | 前端架构：框架、状态管理、性能 | P1 | 前端、react、vue |
| sql-pro | SQL性能优化：索引、查询优化 | P1 | sql、查询、索引 |
| graphql-architect | GraphQL方案：schema、resolver | P1 | graphql |
| event-sourcing-architect | 事件驱动：CQRS、事件溯源 | P1 | 事件、event、cqrs |
| c4-code | 代码级架构：类图、时序、协作 | P2 | 代码、实现 |
| ui-ux-designer | UI/UX设计：原型、交互、体验 | P2 | ui、ux、界面 |
| accessibility-specialist | 无障碍设计：WCAG、ARIA、屏幕阅读器 | P2 | 无障碍、a11y、wcag |
| writing-plans | 规划文档：PRD、技术方案 | P2 | 规划、plan |

## 🎯 场景化深度参考

### 详细参考（引用）

**自然语言示例 + Fallback + 组合流** → 见 `references/quick-reference.md`

### 快速决策速查

```
系统架构设计     → c4-context → c4-container → c4-component
后端架构        → backend-architect
数据库设计      → database-architect
架构评审        → bmad-architect
前端架构        → frontend-developer
SQL 性能        → sql-pro
GraphQL        → graphql-architect
事件驱动        → event-sourcing-architect
UI/UX          → ui-ux-designer
无障碍          → accessibility-specialist
规划文档        → writing-plans
未知任务        → bmad-architect + 询问澄清
```

---

## ❓ Fallback 处理

当任务**无法匹配**以上任何规则时：

```
未知任务
    │
    ├─ 询问用户澄清：
    │   "这个任务是系统设计、数据库设计、还是其他架构相关？"
    │
    └─ 如果用户无法描述：
        └─→ bmad-architect（让架构评审帮你判断）
```

---

## 🔗 任务组合流

### 组合 1: 新系统设计

```
"设计新的电商系统"
    │
    └─ c4-context（上下文）
          └─ c4-container（容器）
                └─ c4-component（组件）
                      └─ c4-code（代码级）
```

### 组合 2: 后端架构

```
"设计后端服务"
    │
    └─ backend-architect
          ├─ graphql → graphql-architect
          └─ 事件 → event-sourcing-architect
```

### 组合 3: 数据库架构

```
"设计数据库"
    │
    └─ database-architect
          └─ sql性能 → sql-pro
```

---

## 🔗 与 gql-arc 主 skill 联动

**注意**：`arc-ext-skill` 不会覆盖 `gql-arc` 主 skill，它们协同工作。

```
┌─────────────────────────────────────────────────────────────┐
│  gql-arc 主 skill                                           │
│    │                                                        │
│    ├─ 通用架构任务 → arc-ext-skill（路由）                  │
│    │              └─→ 具体 skill 执行                         │
│    │                                                        │
│    └─ 特定技能任务 → 直接调用具体 skill                       │
└─────────────────────────────────────────────────────────────┘
```

**何时使用 arc-ext-skill**：
- 任务模糊，需要判断用哪个 skill
- 复杂任务需要多 skill 组合
- 不确定某个 skill 是否适用

**何时直接调用具体 skill**：
- 任务明确，比如"设计容器架构"
- 已确定需要哪个 skill
- 只需要单个 skill

---

## 📖 References 快速索引

详见 `references/quick-reference.md`（自然语言示例 + Fallback + 组合流）

每个 skill 文件都有 TL;DR 摘要：

| Skill | TL;DR | 说明 |
|-------|-------|------|
| c4-context.md | C4上下文建模 | 系统边界、依赖关系 |
| c4-container.md | C4容器设计 | 应用、进程、数据 |
| backend-architect.md | 后端架构 | API设计、数据处理 |
| database-architect.md | 数据库架构 | schema、索引、主从 |
| bmad-architect.md | 架构评审 | 方案评估、风险识别 |
| c4-component.md | C4组件设计 | 模块、类、接口 |
| frontend-developer.md | 前端架构 | 框架、状态管理 |
| sql-pro.md | SQL优化 | 索引、查询优化 |
| graphql-architect.md | GraphQL方案 | schema、resolver |
| event-sourcing-architect.md | 事件驱动 | CQRS、事件溯源 |
| c4-code.md | 代码架构 | 类图、时序、协作 |
| ui-ux-designer.md | UI/UX设计 | 原型、交互、体验 |
| accessibility-specialist.md | 无障碍设计 | WCAG、ARIA |
| writing-plans.md | 规划文档 | PRD、技术方案 |

---

## 🚨 常见错误

| 错误 | 正确做法 |
|------|---------|
| 直接说"设计架构" | 说明设计什么（系统？后端？数据库？） |
| 过度路由 | 直接路由到最可能的 skill |
| 忘记 Fallback | 无法匹配时 → bmad-architect |

---

## 🔗 相关角色联动

| 角色 | 协作场景 |
|------|---------|
| **coder** | 架构完成后：arc-ext-skill 评审架构 → coder-ext-skill 执行开发 |
| **review** | 架构方案：arc-ext-skill 设计 → review-ext-skill 评审架构 |
| **sm** | 项目规划：sm-ext-skill 规划 → arc-ext-skill 评审技术可行性 |
| **qa** | 测试策略：arc-ext-skill 设计架构 → qa-ext-skill 评审可测试性 |

---

## 🗣️ 示例对话

### 示例 1: 路由到 c4-context

```
用户：设计一个新的电商系统
AI：分析：包含"设计"、"电商系统"
     路由到 c4-context
     执行：C4上下文建模
```

### 示例 2: 路由到后端架构组合

```
用户：后端用 GraphQL 怎么设计
AI：分析：包含"后端"、"GraphQL"
     路由到 backend-architect
          → graphql-architect
     执行：GraphQL 架构方案
```

### 示例 3: Fallback 处理

```
用户：帮我看看这个架构合不合理
AI：分析：包含"架构"
     但无法确定具体类型
     Fallback → bmad-architect
     执行：架构评审核心判断任务类型
     反馈：这个任务是"系统架构评审"，建议用 bmad-architect
```

---

## 升级说明

查看 [update_readme.md](update_readme.md) 了解如何同步最新 skill。

当前版本：v2.0.0
