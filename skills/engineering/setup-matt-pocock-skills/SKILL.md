---
name: setup-matt-pocock-skills
description: 为此仓库配置工程技能 —— 设置其 issue 追踪器、triage 标签词汇和领域文档布局。在其他工程技能首次使用前运行一次。
disable-model-invocation: true
---

# Setup Matt Pocock's Skills

搭建工程技能所假设的每个仓库的配置：

- **Issue 追踪器** — issue 在哪里（默认 GitHub；本地 markdown 也是开箱即用支持的）
- **Triage 标签** — 用于五个规范 triage 角色的字符串
- **领域文档** — `CONTEXT.md` 和 ADR 在哪里，以及阅读它们的消费者规则

这是一个提示驱动的技能，不是确定性脚本。探索，呈现你发现的，与用户确认，然后写入。

## 流程

### 1. 探索

查看当前仓库以理解其起始状态。阅读任何存在的东西；不要假设：

- `git remote -v` 和 `.git/config` — 这是 GitHub 仓库吗？哪一个？
- 仓库根目录的 `AGENTS.md` 和 `CLAUDE.md` — 任一存在吗？任一中是否已有 `## Agent skills` 部分？
- 仓库根目录的 `CONTEXT.md` 和 `CONTEXT-MAP.md`
- `docs/adr/` 和任何 `src/*/docs/adr/` 目录
- `docs/agents/` — 此技能的先前输出是否已存在？
- `.scratch/` — 表明本地 markdown issue 追踪器约定已在使用的迹象

### 2. 呈现发现并询问

总结存在什么和缺少什么。然后**一次一个**地带用户完成三个决策 —— 呈现一个部分，获取用户的答案，然后移到下一个。不要一次全部倾倒。

假设用户不知道这些术语意味着什么。每个部分以简短解释开始（它是什么，为什么这些技能需要它，如果他们选择不同会改变什么）。然后显示选择和默认值。

**部分 A — Issue 追踪器。**

> 解释："Issue 追踪器"是此仓库的 issue 所在的地方。像 `to-issues`、`triage`、`to-prd` 和 `qa` 这样的技能从中读取和写入 —— 它们需要知道是调用 `gh issue create`，在 `.scratch/` 下写入 markdown 文件，还是遵循你描述的其他工作流。选择你实际为此仓库跟踪工作的地方。

默认姿态：这些技能是为 GitHub 设计的。如果 `git remote` 指向 GitHub，建议使用它。如果 `git remote` 指向 GitLab（`gitlab.com` 或自托管主机），建议使用 GitLab。否则（或如果用户偏好），提供：

- **GitHub** — issue 存在于仓库的 GitHub Issues 中（使用 `gh` CLI）
- **GitLab** — issue 存在于仓库的 GitLab Issues 中（使用 [`glab`](https://gitlab.com/gitlab-org/cli) CLI）
- **本地 markdown** — issue 作为文件存在于此仓库的 `.scratch/<feature>/` 下（适合个人项目或没有远程的仓库）
- **其他**（Jira、Linear 等）—— 要求用户用一段话描述工作流；技能将其记录为自由文本

如果 —— 且仅当 —— 用户选择了 **GitHub** 或 **GitLab**，问一个后续问题：

> 解释：开源仓库通常以 pull request 而不是 issue 的形式接收功能请求 —— PR 是附带代码的 issue。如果你打开此选项，`/triage` 将*外部* PR 拉入同一队列，并通过与 issue 相同的标签和状态运行它们（协作者的进行中 PR 不受影响）。如果 PR 对你来说不是请求表面，就保持关闭。

- **PR 作为请求表面** — 是 / 否（默认：否）。在 `docs/agents/issue-tracker.md` 中记录答案。对于本地 markdown 和其他追踪器，跳过此问题 —— 没有 PR。

**部分 B — Triage 标签词汇。**

> 解释：当 `triage` 技能处理传入的 issue 时，它将其通过一个状态机移动 —— 需要评估、等待报告者、准备好供 AFK agent 领取、准备好供人类处理、或不会修复。要做到这一点，它需要应用匹配*你实际配置的*字符串的标签（或你 issue 追踪器中的等效物）。如果你的仓库已经使用不同的标签名称（例如 `bug:triage` 而不是 `needs-triage`），在这里映射它们，这样技能应用正确的标签而不是创建重复。

五个规范角色：

- `needs-triage` — 维护者需要评估
- `needs-info` — 等待报告者
- `ready-for-agent` — 完全指定，AFK 就绪（agent 可以在没有人类上下文的情况下领取）
- `ready-for-human` — 需要人类实现
- `wontfix` — 不会被处理

默认：每个角色的字符串等于其名称。询问用户是否要覆盖任何。如果他们的 issue 追踪器没有现有标签，默认值就可以。

**部分 C — 领域文档。**

> 解释：一些技能（`improve-codebase-architecture`、`diagnosing-bugs`、`tdd`）读取 `CONTEXT.md` 文件来学习项目的领域语言，以及 `docs/adr/` 获取过去的架构决策。它们需要知道仓库是有一个全局上下文还是多个（例如一个带有单独前端/后端上下文的 monorepo），这样它们能在正确的地方查找。

确认布局：

- **单一上下文** — 仓库根目录一个 `CONTEXT.md` + `docs/adr/`。大多数仓库是这样的。
- **多上下文** — 根目录的 `CONTEXT-MAP.md` 指向每个上下文的 `CONTEXT.md` 文件（通常是 monorepo）。

### 3. 确认并编辑

向用户展示草稿：

- 要添加到正在编辑的 `CLAUDE.md` / `AGENTS.md` 中的 `## Agent skills` 块（参见第 4 步的选择规则）
- `docs/agents/issue-tracker.md`、`docs/agents/triage-labels.md`、`docs/agents/domain.md` 的内容

让他们在写入前编辑。

### 4. 写入

**选择要编辑的文件：**

- 如果 `CLAUDE.md` 存在，编辑它。
- 否则如果 `AGENTS.md` 存在，编辑它。
- 如果都不存在，询问用户要创建哪一个 —— 不要替他们选择。

当 `CLAUDE.md` 已存在时，永远不要创建 `AGENTS.md`（反之亦然）—— 始终编辑已有的那个。

如果所选文件中已存在 `## Agent skills` 块，原地更新其内容而不是追加重复。不要覆盖用户对周围部分的编辑。

该块：

```markdown
## Agent skills

### Issue tracker

[issue 在哪里跟踪的一行摘要，加上外部 PR 是否是 triage 表面]。参见 `docs/agents/issue-tracker.md`。

### Triage labels

[标签词汇的一行摘要]。参见 `docs/agents/triage-labels.md`。

### Domain docs

[布局的一行摘要 —— "single-context" 或 "multi-context"]。参见 `docs/agents/domain.md`。
```

然后使用此技能文件夹中的种子模板作为起点，写入三个文档文件：

- [issue-tracker-github.md](./issue-tracker-github.md) — GitHub issue 追踪器
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md) — GitLab issue 追踪器
- [issue-tracker-local.md](./issue-tracker-local.md) — 本地 markdown issue 追踪器
- [triage-labels.md](./triage-labels.md) — 标签映射
- [domain.md](./domain.md) — 领域文档消费者规则 + 布局

对于"其他" issue 追踪器，使用用户的描述从零开始编写 `docs/agents/issue-tracker.md`。

### 5. 完成

告诉用户设置完成，以及哪些工程技能现在将从这些文件中读取。提到他们以后可以直接编辑 `docs/agents/*.md` —— 重新运行此技能仅在想要切换 issue 追踪器或从零开始时才需要。
