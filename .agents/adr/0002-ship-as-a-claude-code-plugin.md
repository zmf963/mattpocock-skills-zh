# 将 skill 集作为原生 Claude Code 插件发布；推迟原生 Codex 插件

这些 skills 一直可以通过 [skills.sh](https://skills.sh/mattpocock/skills)（`npx skills add mattpocock/skills`）安装，该方法将可编辑的 skill 文件复制到用户项目中，覆盖 Claude Code、Codex 和其他 Agent-Skills 标准的 harness。一个反复出现的需求是一种**即插即用**的分发方式：将整个 skill 集作为只读、始终最新的捆绑包来订阅，而非你拥有的一个分支。这正是原生插件系统提供的。

我们发布原生 **Claude Code 插件**，目前**推迟**原生 **Codex 插件**。这种分裂是由每个生态系统的插件清单选择 skills 的方式与本仓库的分桶（bucketed）布局之间的冲突所导致的。

## 约束：分桶 skills vs. 单路径选择

Skills 存在于 `skills/` 下的 bucket 文件夹中——`engineering/` 和 `productivity/` 是**推广的**（发布）；`misc/`、`personal/`、`in-progress/`和 `deprecated/` **不是**。一个插件必须只暴露推广的技能集，而它跨越了其中两个 bucket 文件夹。

- **Claude Code**——`.claude-plugin/plugin.json` 接受 `skills` 作为**显式 skill 目录路径数组**。我们逐一列出推广的 skills，零歧义排除其他所有，并添加 `.claude-plugin/marketplace.json` 使仓库本身成为一个单插件市场。端到端验证通过：`claude plugin validate . --strict` 通过，且 `marketplace add` → `install` 能解析所有推广的 skills。

- **Codex**——`.codex-plugin/plugin.json` 只接受 `skills` 作为**单个路径字符串**（数组会被拒绝，提示 `missing or invalid plugin.json`），且 Codex 在它下面递归发现 `SKILL.md` 文件。没有办法从一个路径命名两个 bucket 文件夹，或筛选子集。尝试并拒绝了两种绕行方案：
  - 指向 `./skills/` 也会发布 `deprecated/`、`in-progress/`、`personal/` 和 `misc/`——我们刻意不推广的已退役、草稿和个人 skills。
  - 指向 bucket 的**符号链接**组成的扁平目录在安装后不存活：Codex 将插件树复制到其缓存中并**丢弃符号链接**，所以 skills 到达时为空。

唯一稳健的给 Codex 提供单一推广路径的方式是（a）**重构**使 `skills/` 只包含推广的 skills（将非推广 buckets 移出——影响范围很大，波及 `CLAUDE.md`、`scripts/link-skills.sh`、各 bucket 的 README 以及依赖 `in-progress/` 和 `personal/` 的本地开发工作流），或（b）**提交推广 skills 的复制副本**到扁平目录中（同步负担和第二个真实来源）。两者都是结构性决策，不是打包进 Claude 插件发布中的事。这极可能就是原初那个半记得的原因——为什么更早没有发布插件：清单格式无法干净地表达分桶仓库的筛选子集。

## 决策

- 现在发布 **Claude Code 插件**（`.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json`），筛选为推广集，作为 v1.2 的头号交付物。
- 保持 **skills.sh** 作为通用安装器——它今天已经服务 Codex 和其他 harness，所以没有 Codex 用户会缺少安装路径。
- **推迟**原生 Codex 插件，直到我们决定是重构 `skills/` 为只推广还是提交生成的扁平副本。在 Codex 支持 `skills` 数组/包含列表或在安装时保留符号链接时重新审视。

## 这产生的约束

- 每个推广的 skill 在 `.claude-plugin/plugin.json` 的 `skills` 数组中都有一个条目（这已经是 `CLAUDE.md` 中的一条规则；它现在也把关插件的内容）。
- `.claude-plugin/plugin.json` 的 `version` 与 `package.json` 的 `version` 保持同步——发布时一起 bump。Claude 使用插件 `version` 来决定已安装用户何时看到更新。
