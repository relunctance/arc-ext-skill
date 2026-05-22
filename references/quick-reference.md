<!-- TL;DR: 自然语言示例 + Fallback + 组合流快速参考 -->

# Arc 技能路由快速参考

> 详细决策树见 SKILL.md 主文件

## 🗣️ 自然语言触发示例

| 用户实际说法 | → 路由到 | 说明 |
|-------------|---------|------|
| "设计系统架构" | c4-context | C4上下文 |
| "设计容器" | c4-container | C4容器 |
| "后端架构" | backend-architect | 后端设计 |
| "数据库设计" | database-architect | 数据库 |
| "评审架构" | bmad-architect | 评审 |
| "组件设计" | c4-component | C4组件 |
| "前端架构" | frontend-developer | 前端 |
| "SQL 优化" | sql-pro | SQL |
| "GraphQL" | graphql-architect | GraphQL |
| "事件驱动" | event-sourcing-architect | 事件 |
| "代码架构" | c4-code | 代码级 |
| "UI/UX" | ui-ux-designer | UI设计 |
| "无障碍" | accessibility-specialist | a11y |
| "写规划" | writing-plans | 文档 |

---

## 🔄 Fallback 处理

当任务**无法匹配**时：

```
无匹配 → bmad-architect（让架构评审帮你判断）
```

---

## 🔗 任务组合流

### 组合 1: 新系统设计

```
"设计电商系统"
    └─ c4-context → c4-container → c4-component → c4-code
```

### 组合 2: 后端架构

```
"后端服务设计"
    └─ backend-architect
          ├─ graphql → graphql-architect
          └─ 事件 → event-sourcing-architect
```

### 组合 3: 数据库架构

```
"数据库设计"
    └─ database-architect
          └─ sql → sql-pro
```

---

## ⚡ 快速决策速查卡

```
┌─────────────────────────────────────────────────────────────┐
│  任务类型          │  首选 Skill           │  组合        │
├─────────────────────────────────────────────────────────────┤
│  系统架构          │  c4-context          │  →container  │
│  容器              │  c4-container        │  →component   │
│  后端              │  backend-architect   │  graphql/ev  │
│  数据库            │  database-architect  │  →sql-pro    │
│  架构评审          │  bmad-architect     │              │
│  组件              │  c4-component       │              │
│  前端              │  frontend-developer │              │
│  SQL               │  sql-pro            │              │
│  GraphQL           │  graphql-architect │              │
│  事件驱动          │  event-sourcing..  │              │
│  代码              │  c4-code           │              │
│  UI/UX            │  ui-ux-designer     │              │
│  无障碍            │  accessibility..    │              │
│  规划              │  writing-plans      │              │
│  未知              │  bmad-architect     │  询问澄清    │
└─────────────────────────────────────────────────────────────┘
```
