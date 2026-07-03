---
name: to-issues
description: 使用示踪子弹垂直切片，将计划、规格或 PRD 分解为项目 issue 追踪器上可独立领取的 issue。
disable-model-invocation: true
---

# To Issues

使用垂直切片（示踪子弹）将计划分解为可独立领取的 issue。

issue 追踪器和 triage 标签词汇应该已经提供给你了 —— 如果没有，运行 `/setup-matt-pocock-skills`。

## 流程

### 1. 收集上下文

从对话上下文中已有的内容开始工作。如果用户将 issue 引用（issue 编号、URL 或路径）作为参数传入，从 issue 追踪器获取它并阅读其完整正文和评论。

### 2. 探索代码库（可选）

如果你尚未探索代码库，请这样做以理解代码的当前状态。Issue 标题和描述应使用项目的领域词汇表词汇，并尊重你正在接触的区域的 ADR。

寻找预重构代码以使实现更容易的机会。"让变更容易，然后做容易的变更。"

### 3. 起草垂直切片

将计划分解为**示踪子弹**（tracer bullet）issue。每个 issue 是一个薄的垂直切片，端到端地切穿所有集成层，而不是一个层的水平切片。

<vertical-slice-rules>

- 每个切片交付一条窄但完整的路径，穿过每一层（schema、API、UI、tests）
- 一个完成的切片是可独立演示或可验证的
- 任何预重构应该先做

</vertical-slice-rules>

### 4. 向用户提问

将提议的分解作为编号列表呈现。对于每个切片，显示：

- **标题**：简短的描述性名称
- **被阻塞于**：哪些其他切片（如果有）必须先完成
- **覆盖的用户故事**：这处理哪些用户故事（如果源材料有的话）

询问用户：

- 粒度感觉对吗？（太粗 / 太细）
- 依赖关系正确吗？
- 是否应该合并或进一步拆分任何切片？

迭代直到用户批准分解。

### 5. 将 issue 发布到 issue 追踪器

对于每个批准的切片，向 issue 追踪器发布一个新 issue。使用下面的 issue 正文模板。这些 issue 被视为 AFK agent 就绪，因此使用正确的 triage 标签发布它们，除非另有指示。

按依赖顺序发布 issue（阻塞者先发布），这样你可以在"Blocked by"字段中引用真实的 issue 标识符。

<issue-template>
## Parent

对 issue 追踪器上父 issue 的引用（如果来源是现有 issue，否则省略此部分）。

## What to build

对此垂直切片的简洁描述。描述端到端行为，而不是逐层实现。

避免具体的文件路径或代码片段 —— 它们很快就会过时。例外：如果原型产生了一个比散文更精确地编码决策的片段（状态机、reducer、schema、类型形状），在这里内联它并简要注明它来自原型。修剪到决策丰富的部分 —— 不是工作演示，只是重要的部分。

## Acceptance criteria

- [ ] 标准 1
- [ ] 标准 2
- [ ] 标准 3

## Blocked by

- 对阻塞 ticket 的引用（如果有）

或 "None - can start immediately" 如果没有阻塞者。

</issue-template>

**不要**关闭或修改任何父 issue。
