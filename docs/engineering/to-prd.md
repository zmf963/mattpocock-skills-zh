快速开始：

```bash
npx skills add mattpocock/skills --skill=to-prd
```

```bash
npx skills update to-prd
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-prd)

## 它做什么

`to-prd` 将当前对话和你的代码库理解转化为产品需求文档，然后发布到你的问题跟踪器。

它**不**再次面试你。当你使用它时，对齐工作已经完成——`to-prd` 综合已知的内容，而不是询问新一轮问题。

## 何时使用它

你通过输入 `/to-prd` 来调用它——agent 不会自行调用它。

一旦一个变更已经被讨论过，领域语言已经确定，并且你想在写任何代码之前将该共享理解写为 spec 时使用它。如果你*尚未*对齐，先进行追问——为此，使用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。要将完成的 PRD 分解为工单，使用 [to-issues](https://aihero.dev/skills-to-issues)。

## 前置条件

`to-prd` 发布到你的问题跟踪器，因此 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必须首先为此仓库配置了跟踪器和分类标签。它自行应用 `ready-for-agent` 标签——不需要单独的分类环节。

## PRD 包含什么

- **问题陈述** — 什么坏了或缺失了，以及为什么值得解决，使用项目自己的词汇。
- **解决方案** — 修复的高层形态，在任何实现细节之前。
- **用户故事** — 变更必须支持的具体行为的详尽编号列表，每个都可独立检查。
- **实现决策** — 对话期间已经确定的选择，这样它们不会在以后被重新争论。
- **测试决策** — 功能将被测试的接缝，以及"完成"是什么样子。
- **范围外项目** — 此变更刻意*不*涵盖的内容，以保持工单有边界。
- **进一步说明** — 任何其他值得携带但不适合上述部分的内容。

## 深层模块

在编写 PRD 之前，`to-prd` 勾勒功能将被测试的**接缝**，并寻找**深层模块**机会——大量功能隐藏在小型、稳定的接口后面。它优先使用现有接缝而非新接缝，并使用尽可能最高的接缝，理想情况下整个变更只有一个。

这对 agentic 开发很重要：一个好的接口给测试一些持久的东西来瞄准，因此下面的代码可以在测试不动的情况下变化。

## 它在正常工作的标志

- 它开始写 PRD，而不是问你新一轮问题。
- 它在写之前与你检查接缝，并提议尽可能少的接缝。
- PRD 以你项目的领域词汇返回，而非通用模板。

## 它在哪里

`to-prd` 是主构建链中的一个步骤：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

在计划和领域语言已解决之后、你将工作分解为实现工单之前使用它。它的关键邻居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)，它锐化上下文使 PRD 精确，以及 [to-issues](https://aihero.dev/skills-to-issues)，它将 PRD 转化为 [implement](https://aihero.dev/skills-implement) 要构建的独立可领取的 issues。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
