# Matt Pocock Skills

一组由 Claude Code 加载的 agent skills（斜杠命令与行为）。Skills 按 bucket（桶）组织，并由 `/setup-matt-pocock-skills` 产出的按仓库配置所消费。

## 语言（词汇表）

**Issue tracker（issue 跟踪器）**：
托管仓库 issue 的工具——GitHub Issues、Linear、本地 `.scratch/` markdown 约定，或类似工具。`to-tickets`、`to-spec`、`triage`、`qa` 等 skills 会从中读取并写入。
_避免_：backlog manager、backlog backend、issue host

**Issue**：
**Issue tracker** 内部一个被跟踪的工作单元——由 `to-tickets` 产出的 bug、任务、spec 或切片。
_避免_：ticket（仅在引用把它们称为 ticket 的外部系统时使用，或用于**决策票据**——见下）

**Decision ticket（决策票据）**：
一个 `wayfinder` 单元——一张 `wayfinder:map` 的子 **Issue**，持有一个*问题*，其结论是一个决策，而非待执行的构建切片。**决策**这个限定词使其区别于实施票据；`wayfinder` 引入这个术语，然后简称为"票据"。

**Triage role（分诊角色）**：
在 triage 期间施加于一个 **Issue** 的正典状态机标签（例如 `needs-triage`、`ready-for-afk`）。每个角色都通过 `docs/agents/triage-labels.md` 映射到 **Issue tracker** 中的一个真实标签字符串。

## 关系

- 一个 **Issue tracker** 包含许多 **Issue**
- 一个 **Issue** 同一时刻只携带一个 **Triage role**
- 一个 **Decision ticket** 是一个 **Issue**（`wayfinder:map` 的子 issue）

## 已标记的歧义

- "backlog" 之前既用来表示托管 issue 的*工具*，也表示其中的*工作体*——已解决：该工具即 **Issue tracker**；"backlog" 不再作为领域术语使用。
- "backlog backend" / "backlog manager"——已解决：合并进 **Issue tracker**。
