快速开始：

```bash
npx skills add mattpocock/skills --skill=research
```

```bash
npx skills update research
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/research)

## 作用

`research` 通过阅读拥有答案的来源来回答问题，并在身后留下一份带引用的 Markdown 文件。它只从**一手来源**工作——官方文档、源代码、spec、第一方 API——从不从它们的二手转述，所以它保存的东西可以追溯到某种权威之物，而不是对摘要的摘要。

## 何时使用

输入 `/research`，或者当任务变成阅读跑腿时 agent 会自动调用它。

当下一步是*查明某事*——一个 API 如何表现、一份 spec 到底说什么、一个论断是否成立——而你不愿因为自己去做阅读而卡住自己的线程时使用。要用访谈而非阅读来打磨计划，使用 [grilling](https://aihero.dev/skills-grilling)；要用一次性代码探索该构建什么，使用 [prototype](https://aihero.dev/skills-prototype)。

## 委托的跑腿

定义性的动作是阅读作为**后台 agent** 运行。你继续工作；它走开，把每个论断一路追到它的一手来源，然后把一份带引用的 Markdown 文件放进仓库存放此类笔记的任何地方。研究是你委托的跑腿，不是你外包的思考——你拿回一份可以回应的文档，带着它的来源。

## 所处位置

一个随时可以调用的独立技能，为思考类 skills 提供素材：它产生的文件是可用来 grill、计划或设计的对象，所以它位于 [grilling](https://aihero.dev/skills-grilling) 和 [to-prd](https://aihero.dev/skills-to-prd) 之类工作的上游，而非构建链之中。要看完整地图，见 [ask-matt](https://aihero.dev/skills-ask-matt)。
