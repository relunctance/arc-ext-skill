# Arc Ext Skill

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platforms](https://img.shields.io/badge/platforms-hermes-blue.svg)](#)
[![Version](https://img.shields.io/badge/Version-2.0.0-green.svg)](SKILL.md)
[![Arc Skills](https://img.shields.io/badge/Arc_Skills-14-orange.svg)](#)
[![Auto Route](https://img.shields.io/badge/Auto_Route-Enabled-blue.svg)](#)

架构师技能索引路由器 - 接收任何架构任务，智能推荐最合适的 skill 并执行。

## 一句话路由规则

```
收到架构任务
    │
    ├─ "架构"/"系统" → c4-context
    ├─ "后端"/"api" → backend-architect
    ├─ "数据库" → database-architect
    ├─ "评审" → bmad-architect
    └─ 无匹配 → bmad-architect
```

## 目录

- [快速开始](#快速开始)
- [技能地图](#技能地图)
- [工作流](#工作流)
- [升级](#升级)
- [AGENTS.md](AGENTS.md) - AI Agent 使用指南
- [INSTALL.md](INSTALL.md) - 安装部署说明

## 快速开始

```bash
# 安装
git clone https://gitee.com/ztanfo_admin/arc-ext-skill.git ~/.hermes/profiles/arc/skills/arc-ext-skill

# 使用
hermes -p arc -s arc-ext-skill
```

## 技能地图

| Skill | 说明 | 级别 |
|-------|------|------|
| c4-context | C4上下文建模 | P0 |
| c4-container | C4容器设计 | P0 |
| backend-architect | 后端架构 | P0 |
| database-architect | 数据库架构 | P0 |
| bmad-architect | 架构评审 | P0 |
| c4-component | C4组件设计 | P1 |
| frontend-developer | 前端架构 | P1 |
| sql-pro | SQL优化 | P1 |
| graphql-architect | GraphQL方案 | P1 |
| event-sourcing-architect | 事件驱动 | P1 |
| c4-code | 代码架构 | P2 |
| ui-ux-designer | UI/UX设计 | P2 |
| accessibility-specialist | 无障碍设计 | P2 |
| writing-plans | 规划文档 | P2 |

## 同步到 Hermes

### 安装 Skill 文件到 Hermes Profile

```bash
# 进入仓库目录
cd /home/gql/repos/arc-ext-skill

# 执行同步脚本
python sync_to_hermes.py arc
```

同步后目录结构：
```
~/.hermes/profiles/arc/skills/
├── arc-ext-skill/                      # 路由器
│   ├── SKILL.md
│   └── references/
├── bmad-architect/                    # 独立 skill（软链接）
│   └── SKILL.md → arc-ext-skill/references/bmad-architect.md
├── backend-architect/                # 独立 skill（软链接）
│   └── SKILL.md → arc-ext-skill/references/backend-architect.md
└── ...                               # 其他 skills
```

### 验证安装

```bash
# 查看已安装的 skills
ls -la ~/.hermes/profiles/arc/skills/

# 验证软链接
readlink -f ~/.hermes/profiles/arc/skills/bmad-architect/SKILL.md
```

---

## 工作流

详见 [SKILL.md](SKILL.md)

## 升级

详见 [update_readme.md](update_readme.md)
