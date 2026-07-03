快速开始：

```bash
npx skills add mattpocock/skills --skill=research
```

```bash
npx skills update research
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/research)

## 它做什么

`research` 通过阅读拥有答案的来源来回答问题，并留下一个带引用的 Markdown 文件。它仅从**主要来源**工作——官方文档、源代码、spec、第一方 API——从不是它们的二次转述，因此它保存的东西可追溯到权威的来源，而不是摘要的摘要。

## 何时使用它

输入 `/research`，或者 agent 在任务变成阅读跑腿工作时自动调用它。

当下一步是*找出某些信息*——API 如何行为、spec 实际说了什么、一个说法是否成立——并且你宁愿不停止自己的线程去做阅读时使用它。对于通过面试而非阅读来锐化计划，使用 [grilling](https://aihero.dev/skills-grilling)；对于用一次性代码探索要构建什么，使用 [prototype](https://aihero.dev/skills-prototype)。

## 委托的跑腿工作

定义性的动作是阅读作为**后台 agent** 运行。你继续工作；它离开，将每个说法追溯到其主要来源，并将一个带引用的 Markdown 文件放入仓库保存此类笔记的地方。研究是你委托的跑腿工作，而不是你外包的思考——你拿回的是一份可以回应的文档，附有其来源。

## 它在哪里

一个随时可用的独立 skill，为思考类 skills 提供输入：它产生的文件是可以追问、计划或设计的基础，因此它位于像 [grilling](https://aihero.dev/skills-grilling) 和 [to-prd](https://aihero.dev/skills-to-prd) 这样的工作的上游，而不是在构建链中。要查看完整地图，参见 [ask-matt](https://aihero.dev/skills-ask-matt)。
