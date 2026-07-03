---
name: to-prd
description: 将当前对话转化为 PRD 并发布到项目 issue 追踪器 —— 不进行访谈，只是综合你已经讨论过的内容。
disable-model-invocation: true
---

此技能获取当前对话上下文和代码库理解，并产生一个 PRD。**不要**访谈用户 —— 只需综合你已经知道的内容。

issue 追踪器和 triage 标签词汇应该已经提供给你了 —— 如果没有，运行 `/setup-matt-pocock-skills`。

## 流程

1. 如果你还没有，探索仓库以理解代码库的当前状态。在整个 PRD 中使用项目的领域词汇表词汇，并尊重你正在接触的区域的任何 ADR。

2. 勾勒出你将用来测试功能的 seam。应优先使用现有 seam 而不是新的。使用尽可能最高的 seam。如果需要新的 seam，在你能达到的最高点提议它们。代码库中 seam 越少越好 —— 理想数量是一个。

与用户确认这些 seam 是否符合他们的期望。

3. 使用下面的模板编写 PRD，然后将其发布到项目 issue 追踪器。应用 `ready-for-agent` triage 标签 —— 不需要额外的 triage。

<prd-template>

## Problem Statement

用户面临的问题，从用户的角度。

## Solution

问题的解决方案，从用户的角度。

## User Stories

一个长长的、编号的用户故事列表。每个用户故事应采用以下格式：

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

这个用户故事列表应该非常全面，覆盖功能的所有方面。

## Implementation Decisions

已做出的实现决策列表。这可以包括：

- 将要构建/修改的模块
- 这些模块将要修改的接口
- 来自开发者的技术澄清
- 架构决策
- Schema 变更
- API 契约
- 具体交互

**不要**包含具体的文件路径或代码片段。它们可能很快就会过时。

例外：如果原型产生了一个比散文更精确地编码决策的片段（状态机、reducer、schema、类型形状），在相关决策中内联它并简要注明它来自原型。修剪到决策丰富的部分 —— 不是工作演示，只是重要的部分。

## Testing Decisions

已做出的测试决策列表。包括：

- 什么构成好的测试的描述（仅测试外部行为，不测试实现细节）
- 哪些模块将被测试
- 测试的先例（即代码库中类似类型的测试）

## Out of Scope

对此 PRD 来说超出范围的事情的描述。

## Further Notes

关于此功能的任何进一步注释。

</prd-template>
