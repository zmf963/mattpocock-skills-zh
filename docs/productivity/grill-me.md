快速开始：

```bash
npx skills add mattpocock/skills --skill=grill-me
```

```bash
npx skills update grill-me
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)

## 它做什么

`grill-me` 就一个计划或设计进行无情的面试，遍历决策树的每个分支，直到你和 agent 达成**共享理解**。

它**一次问一个问题**并等待。它从不向你倾倒一批问题——那会让人困惑——在可以通过阅读代码库回答的问题上，它会去阅读而不是询问。每个问题都附带 agent 自己的推荐答案，所以你在回应一个提案，而不是盯着一个空白提示。

## 何时使用它

你通过输入 `/grill-me` 来调用它——agent 不会自行调用它。

在你构建之前使用它，当一个计划感觉大致正确但你能感觉到其中隐藏着未解决的决策时——你想要找到薄弱点并强迫它们暴露出来。如果你想要同样的审问同时也留下 ADR 和术语表的书面记录，改用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。

## 设计树

会话将计划作为决策树来遍历，逐一解决它们之间的依赖关系——在悬于其下的选择之前先解决父决策。重点不是快速达成一致；而是让每个隐含的选择变得明确，这样重要的东西不会被默认为假设。你从另一端出来时，计划的所有分支都已被访问。

`grill-me` 是**无状态的**：它不写任何东西，也不留下工作区。它可以在任何地方运行，唯一的产物是对话本身中被锐化的理解。这就是与 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 的刻意对比，后者将相同的面试捕获为持久的 ADR 和术语表。

## 它在哪里

`grill-me` 是一个随时可用的独立 skill——你每当需要让计划更坚固时运行的构建前压力测试。它是通往 [grilling](https://aihero.dev/skills-grilling) 原语的无状态、用户调用的前门；它最近的邻居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)，有状态的兄弟，运行相同的面试但额外将决策记录为 ADR 和术语表。如果结果是你想要写下来的 spec，交给 [to-prd](https://aihero.dev/skills-to-prd)，它将确定的理综合为 PRD 而无需重新面试你。当你不确定哪个流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
