# Arc Ext Skill 升级方案

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

# P0
cp $BASE/c4-architecture/agents/c4-context.md $REFS/
cp $BASE/c4-architecture/agents/c4-container.md $REFS/
cp $BASE/backend-development/agents/backend-architect.md $REFS/
cp $BASE/database-design/agents/database-architect.md $REFS/
cp $PLUGINS/agent-team-agile-workflow/agents/bmad-architect.md $REFS/

# P1
cp $BASE/c4-architecture/agents/c4-component.md $REFS/
cp $BASE/agents-development-architecture/agents/frontend-developer.md $REFS/
cp $BASE/database-design/agents/sql-pro.md $REFS/
cp $BASE/backend-development/agents/graphql-architect.md $REFS/
cp $BASE/backend-development/agents/event-sourcing-architect.md $REFS/

# P2
cp $BASE/c4-architecture/agents/c4-code.md $REFS/
cp $BASE/agents-design-experience/agents/ui-ux-designer.md $REFS/
cp $BASE/agents-design-experience/agents/accessibility-specialist.md $REFS/
cp $BASE/superpowers/skills/writing-plans/SKILL.md $REFS/writing-plans.md
```

### Step 3: 重新添加 TL;DR

```bash
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
