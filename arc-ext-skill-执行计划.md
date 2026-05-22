# Arc Ext Skill 创建执行计划

## 目标

基于 `profile_role_skill.md` 和 `skills-catalog.md`，创建智能技能路由器仓库 `arc-ext-skill`，包含：
- ✅ 智能索引推荐功能（决策树 + 触发关键词 + 快速参考表）
- ✅ 所有 Arc skill 的 references（含 TL;DR 摘要）
- ✅ 升级方案
- ✅ learns 踩坑记录

---

## Step 1: 下载 & 解压插件包

```bash
# 下载最新插件包
curl -L https://download.codebuddy.cn/plugin-marketplace/codebuddy-plugins-official.zip \
  -o /tmp/codebuddy-plugins-official.zip

# 解压到 /home/gql/tmp/codebuddy-skills（目录存在则跳过）
mkdir -p /home/gql/tmp/codebuddy-skills
unzip -o /tmp/codebuddy-plugins-official.zip -d /home/gql/tmp/codebuddy-skills
```

---

## Step 2: 确认 GitHub 仓库

仓库名：`arc-ext-skill`

```bash
gh repo view relunctance/arc-ext-skill 2>/dev/null && echo "EXISTS" || echo "NOT_EXISTS"
```

---

## Step 3: 复制 profile_role_skill.md

```bash
cp /home/gql/repos/gql-bots/shared/profile_role_skill.md /tmp/profile_role_skill.md
```

**Arc 角色 skill 列表（来源：`/home/gql/repos/gql-bots/shared/profile_role_skill.md`）**：

| Skill | 路径 | 级别 |
|-------|------|------|
| c4-context | `c4-architecture/agents/c4-context.md` | P0 |
| c4-container | `c4-architecture/agents/c4-container.md` | P0 |
| backend-architect | `backend-development/agents/backend-architect.md` | P0 |
| database-architect | `database-design/agents/database-architect.md` | P0 |
| bmad-architect | `agent-team-agile-workflow/agents/bmad-architect.md` | P0 |
| c4-component | `c4-architecture/agents/c4-component.md` | P1 |
| frontend-developer | `agents-development-architecture/agents/frontend-developer.md` | P1 |
| sql-pro | `database-design/agents/sql-pro.md` | P1 |
| graphql-architect | `backend-development/agents/graphql-architect.md` | P1 |
| event-sourcing-architect | `backend-development/agents/event-sourcing-architect.md` | P1 |
| c4-code | `c4-architecture/agents/c4-code.md` | P2 |
| ui-ux-designer | `agents-design-experience/agents/ui-ux-designer.md` | P2 |
| accessibility-specialist | `agents-design-experience/agents/accessibility-specialist.md` | P2 |
| writing-plans | `superpowers/skills/writing-plans/SKILL.md` | P2 |

---

## Step 4: 确认 skill 路径存在

```bash
BASE=/home/gql/tmp/codebuddy-skills/external_plugins
PLUGINS=/home/gql/tmp/codebuddy-skills/plugins

# 逐个验证
for skill in \
  "c4-architecture/agents/c4-context.md" \
  "c4-architecture/agents/c4-container.md" \
  "c4-architecture/agents/c4-component.md" \
  "c4-architecture/agents/c4-code.md" \
  "backend-development/agents/backend-architect.md" \
  "backend-development/agents/graphql-architect.md" \
  "backend-development/agents/event-sourcing-architect.md" \
  "database-design/agents/database-architect.md" \
  "database-design/agents/sql-pro.md" \
  "agents-development-architecture/agents/frontend-developer.md" \
  "agents-design-experience/agents/ui-ux-designer.md" \
  "agents-design-experience/agents/accessibility-specialist.md" \
  "agent-team-agile-workflow/agents/bmad-architect.md" \
  "superpowers/skills/writing-plans/SKILL.md"
do
  if [ -f "$BASE/$skill" ] || [ -f "$PLUGINS/$skill" ]; then
    echo "✅ $skill"
  else
    echo "❌ $skill NOT FOUND"
  fi
done
```

---

## Step 5: 阅读 arc_update.md 获取上下文

```bash
cat /home/gql/repos/gql-bots/docs/roles_skill/arc_update.md
```

---

## Step 6: 阅读 skills-catalog.md 理解技能地图

```bash
cat /home/gql/repos/gql-bots/shared/skills-catalog.md
```

**Arc 技能地图（来源：`/home/gql/repos/gql-bots/shared/skills-catalog.md`）**：

| 场景 | 推荐 Skill | 理由 |
|------|-----------|------|
| 系统上下文建模 | c4-context | 系统上下文建模 |
| 容器架构设计 | c4-container | 容器架构设计 |
| 后端架构决策 | backend-architect | 后端架构决策 |
| 数据库架构 | database-architect | 数据库架构 |
| 架构评审 | bmad-architect | 架构评审 |
| 组件级设计 | c4-component | 组件级设计 |
| 前端架构 | frontend-developer | 前端架构 |
| SQL 性能优化 | sql-pro | SQL 性能优化 |
| GraphQL 方案 | graphql-architect | GraphQL 方案 |
| 事件驱动模式 | event-sourcing-architect | 事件驱动模式 |
| 代码级架构 | c4-code | 代码级架构 |
| UI/UX 设计 | ui-ux-designer | UI/UX 设计 |
| 无障碍设计 | accessibility-specialist | 无障碍设计 |
| 规划文档 | writing-plans | 规划文档 |

---

## Step 7: 创建 arc-ext-skill 仓库

### 7.0 仓库初始化（重要！）

```bash
# 1. 创建 Gitee 仓库
curl -X POST "https://gitee.com/api/v5/user/repos" \
  -d "name=arc-ext-skill&description=Arc技能索引路由器&private=false&auto_init=false" \
  -H "Authorization: token 4995bfdbb1093963081f117438cc9b3a"

# 2. 创建本地仓库
mkdir -p /home/gql/repos/arc-ext-skill
cd /home/gql/repos/arc-ext-skill
git init
git remote add origin https://gitee.com/ztanfo_admin/arc-ext-skill.git
git remote add gitee https://ztanfo_admin:4995bfdbb1093963081f117438cc9b3a@gitee.com/ztanfo_admin/arc-ext-skill.git

# 3. 创建目录结构
mkdir -p /home/gql/repos/arc-ext-skill/learns
mkdir -p /home/gql/repos/arc-ext-skill/references
```

### 7.1 SKILL.md 设计要点（超级重要）

```markdown
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
────────────────────────────────────────────────────────────
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

## 🗣️ 自然语言触发示例（引用）

**详细示例** → 见 `references/quick-reference.md`

```
用户："设计一个新的电商系统"
路由：c4-context

用户："后端用 GraphQL 怎么设计"
路由：backend-architect → graphql-architect
```

---

## ❓ Fallback 处理

**当任务无法匹配任何规则时**：

```markdown
1. 询问用户澄清：
   "这个任务是系统设计、数据库设计、还是其他架构相关？"

2. 如果用户无法描述：
   → bmad-architect（让架构评审帮你判断）
```

---

## 🔗 任务组合流

**详细组合** → 见 `references/quick-reference.md`

```
组合 1: 新系统设计
  c4-context（上下文）
    └─ c4-container（容器）
        └─ c4-component（组件）
            └─ c4-code（代码级）

组合 2: 后端架构
  backend-architect
    ├─ graphql → graphql-architect
    └─ 事件 → event-sourcing-architect

组合 3: 数据库架构
  database-architect
    └─ sql性能 → sql-pro
```

---

## 🔗 与 gql-arc 主 skill 联动

当 Arc 角色加载 `arc-ext-skill` 时：

```markdown
1. 收到架构任务
2. 先加载 arc-ext-skill（路由器）
3. 根据任务路由到具体 skill
4. 执行完成后返回 bmad-architect 做评审
```

**注意**：`arc-ext-skill` 不会覆盖 `gql-arc` 主 skill，它们协同工作。

---

## 🚨 常见错误

### 错误 1: 过度路由

```
❌ "用户说设计架构，路由到 c4-context，
    然后又问用户要不要用 c4-container"
✓  直接路由到最可能的 skill，让用户决定是否深入
```

### 错误 2: 路由到不存在的 skill

```
❌ 根据关键词猜 skill 名称
✓  严格按照技能地图中的 skill 名称路由
```

### 错误 3: 忘记 Fallback

```
❌ 无法匹配时不知所措
✓  无法匹配时 → bmad-architect（让架构评审帮你判断）
```

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

查看 `update_readme.md` 了解如何同步最新 skill。

当前版本：v2.0.0

---

### 7.2 references 复制命令

```bash
BASE=/home/gql/tmp/codebuddy-skills/external_plugins
PLUGINS=/home/gql/tmp/codebuddy-skills/plugins
REFS=/home/gql/repos/arc-ext-skill/references

mkdir -p $REFS

# P0 Skills
cp $BASE/c4-architecture/agents/c4-context.md $REFS/c4-context.md
cp $BASE/c4-architecture/agents/c4-container.md $REFS/c4-container.md
cp $BASE/backend-development/agents/backend-architect.md $REFS/backend-architect.md
cp $BASE/database-design/agents/database-architect.md $REFS/database-architect.md
cp $PLUGINS/agent-team-agile-workflow/agents/bmad-architect.md $REFS/bmad-architect.md

# P1 Skills
cp $BASE/c4-architecture/agents/c4-component.md $REFS/c4-component.md
cp $BASE/agents-development-architecture/agents/frontend-developer.md $REFS/frontend-developer.md
cp $BASE/database-design/agents/sql-pro.md $REFS/sql-pro.md
cp $BASE/backend-development/agents/graphql-architect.md $REFS/graphql-architect.md
cp $BASE/backend-development/agents/event-sourcing-architect.md $REFS/event-sourcing-architect.md

# P2 Skills
cp $BASE/c4-architecture/agents/c4-code.md $REFS/c4-code.md
cp $BASE/agents-design-experience/agents/ui-ux-designer.md $REFS/ui-ux-designer.md
cp $BASE/agents-design-experience/agents/accessibility-specialist.md $REFS/accessibility-specialist.md
cp $BASE/superpowers/skills/writing-plans/SKILL.md $REFS/writing-plans.md
```

### 7.3 references 添加 TL;DR

```bash
for f in references/*.md; do
  if ! grep -q "^<!-- TL;DR" "$f"; then
    case "$f" in
      c4-context.md)
        echo "<!-- TL;DR: C4模型上下文建模：系统边界、依赖关系 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      c4-container.md)
        echo "<!-- TL;DR: C4模型容器设计：应用、进程、数据架构 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      backend-architect.md)
        echo "<!-- TL;DR: 后端架构决策：API设计、数据处理、服务建模 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      database-architect.md)
        echo "<!-- TL;DR: 数据库架构：schema设计、索引优化、主从复制 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      bmad-architect.md)
        echo "<!-- TL;DR: 架构评审：方案评估、风险识别、改进建议 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      c4-component.md)
        echo "<!-- TL;DR: C4模型组件设计：模块、类、接口关系 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      frontend-developer.md)
        echo "<!-- TL;DR: 前端架构：框架选择、状态管理、性能优化 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      sql-pro.md)
        echo "<!-- TL;DR: SQL性能优化：索引优化、查询优化、执行计划 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      graphql-architect.md)
        echo "<!-- TL;DR: GraphQL方案：schema设计、resolver实现 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      event-sourcing-architect.md)
        echo "<!-- TL;DR: 事件驱动架构：CQRS、事件溯源、消息队列 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      c4-code.md)
        echo "<!-- TL;DR: 代码级架构：类图、时序图、协作图 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      ui-ux-designer.md)
        echo "<!-- TL;DR: UI/UX设计：原型设计、交互设计、用户体验 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      accessibility-specialist.md)
        echo "<!-- TL;DR: 无障碍设计：WCAG 2.1、ARIA、屏幕阅读器适配 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
      writing-plans.md)
        echo "<!-- TL;DR: 规划文档：PRD模板、技术方案模板 -->" | cat - "$f" > temp && mv temp "$f"
        ;;
    esac
  fi
done
```

---

## Step 8: 创建 learns/ 踩坑记录

```bash
mkdir -p /home/gql/repos/arc-ext-skill/learns
```

**learns/README.md 模板**：

```markdown
# Arc Ext Skill 踩坑沉淀

## 🏷️ 按标签索引

## #路径确认

### c4-context / c4-container / c4-component / c4-code
- **位置**: `c4-architecture/agents/*.md`
- **注意**: 都在同一个目录

### backend-architect / graphql-architect / event-sourcing-architect
- **位置**: `backend-development/agents/*.md`
- **注意**: 和 c4 不在同一目录

### database-architect / sql-pro
- **位置**: `database-design/agents/*.md`
- **注意**: sql-pro 和 database-architect 在同一目录

### bmad-architect
- **位置**: `agent-team-agile-workflow/agents/bmad-architect.md`
- **注意**: 在 plugins 目录，不是 external_plugins

## #source-区分

| 目录 | Skills |
|------|--------|
| `external_plugins/c4-architecture/` | c4-context, c4-container, c4-component, c4-code |
| `external_plugins/backend-development/` | backend-architect, graphql-architect, event-sourcing-architect |
| `external_plugins/database-design/` | database-architect, sql-pro |
| `external_plugins/agents-development-architecture/` | frontend-developer |
| `external_plugins/agents-design-experience/` | ui-ux-designer, accessibility-specialist |
| `external_plugins/superpowers/` | writing-plans |
| `plugins/agent-team-agile-workflow/` | bmad-architect |

## #references-增强

### TL;DR 标记
- **目的**: 快速定位关键信息，AI 读取效率提升
- **格式**: `<!-- TL;DR: 一句话描述 -->`
- **位置**: 每个 reference 文件第一行
```

---

## Step 9: 创建 update_readme.md 升级方案

```markdown
# Arc Ext Skill 升级方案

## 执行计划

详见 `arc-ext-skill-执行计划.md`（详细步骤说明）

## 何时升级

1. `codebuddy-plugins-official.zip` 更新时
2. `gql-bots/shared/profile_role_skill.md` 变化时
3. `gql-bots/shared/skills-catalog.md` 更新时

## 升级步骤

### Step 1: 下载最新插件包

```bash
curl -L https://download.codebuddy.cn/plugin-marketplace/codebuddy-plugins-official.zip \
  -o /tmp/codebuddy-plugins-official.zip
unzip -o /tmp/codebuddy-plugins-official.zip -d /home/gql/tmp/codebuddy-skills
```

### Step 2: 同步 references

```bash
BASE=/home/gql/tmp/codebuddy-skills/external_plugins
PLUGINS=/home/gql/tmp/codebuddy-skills/plugins
REFS=/home/gql/repos/arc-ext-skill/references

# 复制所有 skill 文件
# [同 Step 7.2 的复制命令]
```

### Step 3: 重新添加 TL;DR（如有需要）

```bash
# 检查并添加 TL;DR
for f in references/*.md; do
  if ! grep -q "^<!-- TL;DR" "$f"; then
    # 添加 TL;DR
    ...
  fi
done
```

### Step 4: 提交

```bash
cd /home/gql/repos/arc-ext-skill
git add -A
git commit -m "chore: sync with latest codebuddy-plugins"
git push origin main
```

## 版本号规则

| 类型 | 规则 |
|------|------|
| 主版本 | skill 索引结构变化、决策树重构 |
| 次版本 | 新增/删除 skill、触发关键词更新 |
| 修订版 | 内容更新、TL;DR 更新 |

## 路径速查

| Skill | 源路径 |
|-------|--------|
| c4-context | `external_plugins/c4-architecture/agents/c4-context.md` |
| c4-container | `external_plugins/c4-architecture/agents/c4-container.md` |
| c4-component | `external_plugins/c4-architecture/agents/c4-component.md` |
| c4-code | `external_plugins/c4-architecture/agents/c4-code.md` |
| backend-architect | `external_plugins/backend-development/agents/backend-architect.md` |
| graphql-architect | `external_plugins/backend-development/agents/graphql-architect.md` |
| event-sourcing-architect | `external_plugins/backend-development/agents/event-sourcing-architect.md` |
| database-architect | `external_plugins/database-design/agents/database-architect.md` |
| sql-pro | `external_plugins/database-design/agents/sql-pro.md` |
| frontend-developer | `external_plugins/agents-development-architecture/agents/frontend-developer.md` |
| ui-ux-designer | `external_plugins/agents-design-experience/agents/ui-ux-designer.md` |
| accessibility-specialist | `external_plugins/agents-design-experience/agents/accessibility-specialist.md` |
| bmad-architect | `plugins/agent-team-agile-workflow/agents/bmad-architect.md` |
| writing-plans | `external_plugins/superpowers/skills/writing-plans/SKILL.md` |
```

---

## Step 10: 更新 README.md

使用 `readme-skill` 美化 README，包含：
- 5 个徽章（包括 auto_route）
- 目录结构
- 一句话路由规则
- 决策树
- TL;DR 索引表

---

## Step 11: Git 提交

```bash
cd /home/gql/repos/arc-ext-skill
git add -A
git commit -m "feat: v2.0 - intelligent skill router with auto_route"
git push origin main
```

---

## 验证清单

- [ ] 下载解压成功
- [ ] GitHub 仓库已创建/更新
- [ ] 所有 14 个 skill 路径验证通过
- [ ] references/ 包含所有 skill 文件（含 TL;DR）
- [ ] SKILL.md 包含智能索引：
  - [ ] 一句话触发规则
  - [ ] 决策树
  - [ ] 技能地图
  - [ ] 场景化深度参考
  - [ ] TL;DR 索引表
- [ ] learns/ 有踩坑记录
- [ ] update_readme.md 有升级方案
- [ ] README.md 已美化
- [ ] auto_route: true 启用
- [ ] git push 成功

---

## 其他角色创建注意事项

创建其他角色时，参考以下通用模板：

### 1. SKILL.md 必须包含

```markdown
## ⚡ 快速路由（必读）

### 任务 → Skill 速查

| 你的任务（说人话） | → 推荐 Skill | 直接调用 |
|------------------|-------------|---------|
| ... | ... | ... |

### 一句话触发规则

```
任务包含...         → 直接路由到...
```

## 🔀 智能路由决策树

```
收到任务
    │
    ├─ 包含 "X"
    │   └─→ skill-a + skill-b
    │
    ...
```

## 📋 技能地图

| Skill | TL;DR | 级别 | 触发关键词 |
|-------|-------|------|-----------|

## 🎯 场景化深度参考

### 场景 1: ...
```

### 2. references 添加 TL;DR

```bash
for f in references/*.md; do
  if ! grep -q "^<!-- TL;DR" "$f"; then
    echo "<!-- TL;DR: 一句话描述 -->" | cat - "$f" > temp && mv temp "$f"
  fi
done
```

### 3. 路径速查（更新 document 中的路径）

确保 `update_readme.md` 中的路径速查表是最新的。

### 4. 踩坑记录

记录：
- 路径确认问题
- source 区分（external_plugins vs plugins）
- TL;DR 相关问题
