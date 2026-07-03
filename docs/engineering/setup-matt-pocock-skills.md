快速开始：

```bash
npx skills add mattpocock/skills --skill=setup-matt-pocock-skills
```

```bash
npx skills update setup-matt-pocock-skills
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills)

## 它做什么

`setup-matt-pocock-skills` 教一个仓库工程 skills 应如何在其中行为——issues 在哪里、分类标签叫什么、领域文档在哪里——并将这些答案记录为其他 skills 读取的**配置**。

它写入配置，不硬编码行为。工程链假设 `docs/agents/` 下存在三个文件；此 skill 是产生它们的一次性引导，从你的实际仓库中发现（`git remote`、现有标签、现有 `CONTEXT.md`）并与你确认而非猜测。它是 prompt 驱动的——探索、呈现发现的内容、确认、然后写入——而非确定性脚手架。

## 何时使用它

你通过输入 `/setup-matt-pocock-skills` 来调用它——agent 不会自行调用它。

**每个仓库一次，在首次使用任何其他工程 skill 之前**使用它。如果 [triage](https://aihero.dev/skills-triage)、[to-prd](https://aihero.dev/skills-to-prd) 或 [to-issues](https://aihero.dev/skills-to-issues) 开始猜测你的 issues 在哪里或应用不存在的标签，说明它们尚未在此处设置。仅在切换问题跟踪器或重新开始时重新运行它——日常调整只需编辑 `docs/agents/*.md`。

## 三个决策

它带你走过三个选择，一次一个，每个都附有简单语言的解释（它假设你还不了解这些术语）：

- **问题跟踪器** — 工作在哪里被跟踪，这样 `triage`/`to-prd`/`to-issues` 知道是调用 `gh`、`glab`、在 `.scratch/` 下写 markdown，还是遵循你描述的工作流。GitHub、GitLab、本地 markdown 或其他。
- **分类标签** — 五个规范角色背后的字符串（`needs-triage`、`needs-info`、`ready-for-agent`、`ready-for-human`、`wontfix`），映射到你实际配置的标签，这样 `triage` 应用真实的标签而不是创建重复。
- **领域文档** — 仓库有一个 `CONTEXT.md` 还是多上下文映射，这样读取领域语言的 skills 知道在哪里找。

输出是三个文件——`docs/agents/issue-tracker.md`、`docs/agents/triage-labels.md`、`docs/agents/domain.md`——加上一个 `## Agent skills` 块，指向仓库已在使用的 `CLAUDE.md` / `AGENTS.md` 中的它们。这些文件是工具包其余部分所依赖的共享基础。

## 它在正常工作的标志

- 三个文件落入 `docs/agents/`，且 `## Agent skills` 部分出现在你的 `CLAUDE.md` 或 `AGENTS.md` 中。
- 它提议的跟踪器匹配你真实的 `git remote`，标签匹配你仓库中已存在的字符串。
- 之后，`triage` 和 `to-issues` 在正确的位置用正确的标签操作，而不是询问或猜测。

## 它在哪里

`setup-matt-pocock-skills` 是**运行一次**的设置——整个工程集合站立的基础，不是你重复的步骤。它的邻居是读取它写入内容的 skills：[triage](https://aihero.dev/skills-triage)，因为它应用此处配置的标签词汇，以及 [to-prd](https://aihero.dev/skills-to-prd) / [to-issues](https://aihero.dev/skills-to-issues)，因为它们发布到此处配置的问题跟踪器。先运行它；下游的一切都假设已经运行过。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
