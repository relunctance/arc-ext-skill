# INSTALL.md - Arc Ext Skill 安装部署

## 前置要求

- Hermes Agent 已安装
- 目标 profile 已存在（如 `arc`）

## 安装步骤

### 方式 1：使用同步脚本（推荐）

```bash
# 进入仓库目录
cd /home/gql/repos/arc-ext-skill

# 执行同步脚本
bash sync-to-hermes.sh arc
```

### 方式 2：手动安装

```bash
# 1. 克隆仓库
git clone https://github.com/relunctance/arc-ext-skill.git ~/.hermes/profiles/arc/skills/arc-ext-skill

# 2. 进入目录
cd ~/.hermes/profiles/arc/skills/arc-ext-skill

# 3. 执行同步
bash sync-to-hermes.sh arc
```

## 验证安装

```bash
# 查看已安装的 skills
ls -la ~/.hermes/profiles/arc/skills/

# 验证软链接
readlink -f ~/.hermes/profiles/arc/skills/arc-ext-skill/SKILL.md
```

## 目录结构

安装后 `~/.hermes/profiles/arc/skills/` 应包含：

```
arc/
├── arc-ext-skill/              # 主 skill
│   ├── SKILL.md
│   ├── AGENTS.md
│   ├── INSTALL.md
│   ├── references/
│   └── shared/
├── gql-arc/                    # 主角色 skill（来自 gql-bots）
│   └── SKILL.md
└── ...
```

## 配置文件

### vars.md 配置

`arc/vars.md` 应包含：

```yaml
# Arc 配置变量
DOCS_HOME: {{GQL_BOTS_HOME}}/docs

## 通知模式
notify_mode: team  # report | team
HERMES_PROFILE: arc
FEISHU_MAIN: oc_22e019265c6096916f5a78de44f3cdea

## 模式配置
MODE_CONFIG: full_auto  # full_auto | semi_auto
```

## 更新 skill

```bash
cd /home/gql/repos/arc-ext-skill
git pull
bash sync-to-hermes.sh arc
```

## 卸载

```bash
rm -rf ~/.hermes/profiles/arc/skills/arc-ext-skill
```
