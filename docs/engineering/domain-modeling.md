Quickstart:

```bash
npx skills add mattpocock/skills --skill=domain-modeling
```

```bash
npx skills update domain-modeling
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling)

## 作用

`domain-modeling` 在设计过程中构建和精炼项目的**通用语言**——挑战模糊的术语、用具体场景压力测试关系、并在术语和决策一旦明确时就立刻记录下来。

这是**主动**的实践，而非被动。仅仅阅读 `CONTEXT.md` 来借用其词汇是任何技能都能做的单行习惯；此技能适用于当你*正在改变*模型时——创造一个规范术语、发现代码与你刚才所说的内容之间的矛盾、记录一个难以撤销的决策。它保持词汇表整洁：`CONTEXT.md` 只是一个词汇表，别无其他——没有实现细节、没有规格、没有草稿。

## 何时使用

输入 `/domain-modeling`，或者当任务适当时代理会自动调用它——当你正在确定术语、解决一个多义词、或记录架构决策时。

当*词汇*本身是问题时使用它：两个人对"cancellation"有不同的理解、"account"承担了三种职责、或者设计对话反复卡在一个从未被精确定义的概念上。如果问题是模块的*形状*——接缝放在哪里、接口有多深——请使用 [codebase-design](https://aihero.dev/skills-codebase-design)。如果你想在构建之前对计划本身进行审查，请使用 [grilling](https://aihero.dev/skills-grilling)。

## 前置条件

该技能写入两个位置，两者都是惰性创建的——只在有内容需要记录时才创建。已解决的术语写入根目录下的 `CONTEXT.md`（或者，在由 `CONTEXT-MAP.md` 标记的多上下文仓库中，写入对应上下文的 `CONTEXT.md`）。决策写入 `docs/adr/`。不需要预先存在任何东西；第一个解决的术语创建词汇表，第一个真正的权衡创建 ADR。

## 词汇表 vs. ADR

两个产物，两种不同的标准：

- **词汇表**（`CONTEXT.md`）记录语言。每当一个模糊的术语变得规范时，它会被立即写入——而非批量处理——这样共享词汇表就能与对话保持同步。它严格避免包含实现细节。
- **ADR** 记录决策，且标准很高：仅在决策**难以撤销**、**在没有上下文的情况下令人惊讶**、且**是真正权衡的结果**时才会提供。缺少三者中的任何一个，就没有 ADR。这正是保持 `docs/adr/` 成为关键分岔点记录而非流水账的原因。

使其发挥作用的关键动作：当你陈述某物如何工作时，该技能会交叉引用代码并揭示矛盾——"你的代码取消了整个 Orders，但你刚才说部分取消是可能的——哪个是对的？"语言和代码被迫达成一致。

## 特意独立出来

`domain-modeling` 是构建项目通用语言的**单一可信来源**，作为独立的模型自动调用技能被拆分出来，以便任何其他技能都能引用它。[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 在盘问过程中依赖它来记录术语和决策，[triage](https://aihero.dev/skills-triage) 用它来保持工单使用项目自己的语言，[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在工作时也会调用它。

保持其独立意味着你也可以直接调用它——作为精炼模型的**参考**——而无需承诺使用任何这些技能所规定的步骤。语言存在于一个地方，所有需要它的东西都指向那里。

## 所处位置

`domain-modeling` 是一个**随时可调用的独立技能**，它既在固定步骤中被调用，也经常在其他技能*之下*运行。它最近的邻居是 [codebase-design](https://aihero.dev/skills-codebase-design)，因为共享语言正是让你能够精确命名深层模块及其接缝的前提；下游，一个确定下来的词汇表正是 [to-prd](https://aihero.dev/skills-to-prd) 综合成以项目自身语言编写的规格所需的内容。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
