# Matt Pocock Skills

一组由 Claude Code 加载的 agent skills（斜杠命令和行为）。Skills 按桶组织，由 `/setup-matt-pocock-skills` 发出的每个仓库配置来消费。

## 语言

**问题跟踪器**：
托管仓库 issues 的工具——GitHub Issues、Linear、本地 `.scratch/` markdown 约定或类似工具。像 `to-issues`、`to-prd`、`triage` 和 `qa` 这样的 skills 从中读取和写入。
_避免_：backlog 管理器、backlog 后端、issue 托管

**Issue**：
**问题跟踪器**中的单个跟踪工作单元——一个 bug、任务、PRD 或由 `to-issues` 产生的切片。
_避免_：ticket（仅在引用将其称为 ticket 的外部系统时使用）

**分类角色**：
在分类过程中应用于 **Issue** 的规范状态机标签（例如 `needs-triage`、`ready-for-afk`）。每个角色通过 `docs/agents/triage-labels.md` 映射到**问题跟踪器**中的真实标签字符串。

## 关系

- 一个**问题跟踪器**包含多个 **Issues**
- 一个 **Issue** 一次带有一个**分类角色**

## 已标记的歧义

- "backlog" 曾用于表示*托管 issues 的工具*和*其中的工作体*两者——已解决：工具是**问题跟踪器**；"backlog" 不再作为领域术语使用。
- "backlog backend" / "backlog manager"——已解决：合并为**问题跟踪器**。
