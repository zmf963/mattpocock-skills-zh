---
name: improve-codebase-architecture
description: 扫描代码库寻找深化机会，以可视化 HTML 报告呈现它们，然后对你选择的任何一个进行 grill。
disable-model-invocation: true
---

# Improve Codebase Architecture

揭示架构摩擦并提出**深化机会**（deepening opportunities）—— 将浅层模块转化为深度模块的重构。目标是可测试性和 AI 可导航性。

此命令*由*项目的领域模型提供信息，并建立在共享的设计词汇之上：

- 运行 `/codebase-design` 技能获取架构词汇（**module**、**interface**、**depth**、**seam**、**adapter**、**leverage**、**locality**）及其原则（删除测试、"接口就是测试表面"、"一个适配器 = 假设的 seam，两个 = 真实的"）。在每个建议中精确使用这些术语 —— 不要滑向 "component"、"service"、"API" 或 "boundary"。
- `CONTEXT.md` 中的领域语言为好的 seam 命名；`docs/adr/` 中的 ADR 记录了此命令不应重新争论的决策。

## 流程

### 1. 探索

首先阅读项目的领域词汇表（`CONTEXT.md`）和你正在接触的区域的任何 ADR。

然后使用 Agent 工具，以 `subagent_type=Explore` 来遍历代码库。不要遵循僵化的启发式 —— 有机地探索并注意你在哪里经历摩擦：

- 在哪里理解一个概念需要在许多小模块之间跳转？
- 哪些模块是**浅的**（shallow）—— 接口几乎和实现一样复杂？
- 哪些地方纯粹为了可测试性而提取了纯函数，但真正的 bug 隐藏它们如何被调用中（没有**局部性** locality）？
- 哪些地方紧密耦合的模块在其 seam 处泄漏？
- 代码库的哪些部分未经测试，或难以通过其当前接口测试？

对你怀疑是浅层的任何东西应用**删除测试**：删除它会集中复杂性，还是只是移动它？"是的，集中"是你想要的信号。

### 2. 以 HTML 报告呈现候选方案

将自包含的 HTML 文件写入操作系统临时目录，这样不会有东西落在仓库中。从 `$TMPDIR` 解析临时目录，回退到 `/tmp`（Windows 上为 `%TEMP%`），并写入 `<tmpdir>/architecture-review-<timestamp>.html`，这样每次运行都得到一个新文件。为用户打开它 —— Linux 上 `xdg-open <path>`，macOS 上 `open <path>`，Windows 上 `start <path>` —— 并告诉他们绝对路径。

报告使用**通过 CDN 的 Tailwind** 进行布局和样式，以及**通过 CDN 的 Mermaid** 用于图表，当图形/流程/序列能可靠地传达结构时。混合 Mermaid 与手工制作的 CSS/SVG 视觉效果 —— 当关系是图形状的（调用图、依赖关系、序列）时使用 Mermaid，当你想做一些更具编辑性的东西（质量图、横截面、折叠动画）时使用手工构建的 div/SVG。每个候选方案获得一个**前后对比可视化**。要视觉化。

对于每个候选方案，渲染一张卡片，包含：

- **文件** — 涉及哪些文件/模块
- **问题** — 为什么当前架构正在造成摩擦
- **解决方案** — 用通俗英语描述什么会改变
- **收益** — 用 locality 和 leverage 的术语解释，以及测试将如何改善
- **前后对比图** — 并排，自定义绘制，说明浅层性和深化
- **推荐强度** — 以下之一：`Strong`、`Worth exploring`、`Speculative`，渲染为徽章

以**最佳推荐**部分结束报告：你会首先处理哪个候选方案以及为什么。

**对领域使用 CONTEXT.md 的词汇，对架构使用 `/codebase-design` 的词汇。** 如果 `CONTEXT.md` 定义了 "Order"，谈论 "Order intake module" —— 而不是 "FooBarHandler"，也不是 "Order service"。

**ADR 冲突**：如果一个候选方案与现有 ADR 矛盾，只有当摩擦真实到足以值得重新审视 ADR 时才提出来。在卡片中清晰标记（例如，警告提示：*"与 ADR-0007 矛盾 —— 但值得重新打开因为……"*）。不要列出 ADR 禁止的每个理论重构。

参见 [HTML-REPORT.md](HTML-REPORT.md) 获取完整的 HTML 脚手架、图表模式和样式指南。

**不要**在此阶段提出接口。文件写入后，问用户："你想探索其中哪一个？"

### 3. Grilling 循环

一旦用户选择了一个候选方案，运行 `/grilling` 技能与他们一起遍历设计树 —— 约束、依赖关系、深化模块的形状、seam 后面是什么、哪些测试存活。

在决策结晶时，副作用内联发生 —— 运行 `/domain-modeling` 技能以在进行中保持领域模型最新：

- **以不在 `CONTEXT.md` 中的概念命名深化模块？** 将该术语添加到 `CONTEXT.md`。如果文件不存在则惰性创建。
- **在对话中打磨一个模糊术语？** 立即更新 `CONTEXT.md`。
- **用户以负载支撑的理由拒绝候选方案？** 提供一个 ADR，框架为：*"想让我将此记录为 ADR 以便未来的架构审查不会重新建议它吗？"* 仅当理由确实会被未来探索者需要以避免重新建议相同东西时才提供 —— 跳过短暂的理由（"现在不值得"）和不言自明的理由。
- **想要为深化模块探索替代接口？** 运行 `/codebase-design` 技能并使用其 design-it-twice 并行子 agent 模式。
