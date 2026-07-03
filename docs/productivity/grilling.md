快速开始：

```bash
npx skills add mattpocock/skills --skill=grilling
```

```bash
npx skills update grilling
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

## 它做什么

`grilling` 是在你构建之前对计划或设计进行压力测试的无情面试。它沿着设计树逐个分支走下去，逐一解决决策之间的依赖关系，直到你和 agent 共享相同的理解。

它**一次问一个问题**并在下一个问题之前等待你的答案——从不批量列表，那会让人困惑。每个问题都附带 agent 自己的推荐答案，代码库可以解决的任何问题它都会去探索而不是问你。

## 何时使用它

输入 `/grilling`，或者 agent 在任务匹配时自动调用它——这是底层原语，不是仅用户入口点。

当一个计划或设计仍有薄弱点，并且你想在代码编写之前让它们浮出水面时使用它。在实践中，你通常通过它的两个包装器之一而非按名称调用它：对于普通的追问会话使用 [grill-me](https://aihero.dev/skills-grill-me)；要让会话在进行中也写入 ADR 和术语表，使用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。

## 设计树

心智模型是**设计树**：每个计划分支为决策，而决策相互依赖。`grilling` 一次一个节点地下降那棵树，因此早期的答案可以重塑接下来出现哪些问题。这就是为什么问题逐个到达并按依赖顺序——并行的消防水管式问题会丢失让面试汇聚到共享理解的结构。

## 刻意拆分出来

`grilling` 是面试技术的**单一真相来源**，作为模型调用的**原语**拆分出来，这样每个需要面试的 skill 都可以访问它而不是重新发明一个。[grill-me](https://aihero.dev/skills-grill-me) 和 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 是它的两个用户调用的前门，但 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 和 [triage](https://aihero.dev/skills-triage) 也依赖它来压力测试自己的决策。

将技术保持在一个地方意味着你也可以直接使用它，当你只想要面试时——而不需要其包装器在顶部添加的 ADR 编写或工单塑形。

## 它在哪里

`grilling` 是主构建链下的面试**原语**：[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 在 [to-prd](https://aihero.dev/skills-to-prd) 写 spec 之前运行它以锐化上下文。当你不确定哪个入口点适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
