Quickstart:

```bash
npx skills add mattpocock/skills --skill=ask-matt
```

```bash
npx skills update ask-matt
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt)

## 作用

`ask-matt` 是本仓库中所有技能的**路由器**。你描述当前所处的情况，它会告诉你哪个技能或流程合适，以及它们的执行顺序。

它**本身不做任何实际工作**。它不会盘问、写 PRD 或修复任何问题——它只负责指引方向。它存在的意义首先是面向**用户主动调用的**技能：这些技能不会自动触发，所以*你*必须记得它们的存在，而 `ask-matt` 就是你卸掉这份记忆负担的地方。它同时指向那些你会通过名称直接调用的**模型自动调用**技能——`/tdd`、`/diagnosing-bugs`、`/prototype`、`/code-review`，以及两个词汇参考工具 `/domain-modeling` 和 `/codebase-design`。它回答"用哪个，什么时候用"，然后把你交给真正干活的技能。

## 何时使用

你需要通过输入 `/ask-matt` 来调用它——代理不会自行触发。

当你拿不准当前情况该用哪个技能或流程时就用它：你有个想法但不知从何入手，一堆 bug 报告但不确定是否该用 `/triage`，或者两个技能看起来可以互换但你分不清它们的区别。如果你已经知道要用的技能，跳过路由器直接调用即可。

## 流程，不止是技能

`ask-matt` 让你用来思考的核心概念是**流程**——一条*贯穿*多个技能的路径，而非单个技能。大多数工作沿着一条**主线流程**（构思 → 发布：grill → PRD → issues → implement → review）进行，两条**入口匝道**汇入主线（一条用于处理外来的 bug 和需求；一条用于产生代码库健康改进想法），其余的都是可以独立调用的**独立技能**。提出问题后，你会被引导到正确的流程和正确的步骤上——而不仅仅是拿到一个工具。

## 所处位置

`ask-matt` 是**路由器**——一张独立的地图，覆盖整个技能集。所有其他文档页面都以 [ask-matt](https://aihero.dev/skills-ask-matt) 的形式链接回这个节点，所以它从不*处于*某个链条之中；它指向*进入*每个链条的入口。从这里出发，你最常到达的是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)（主流程的起点）或 [triage](https://aihero.dev/skills-triage)（处理非你创建的工作的入口匝道）。即使路由器自身的图示过时了，它的 [Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt) 也是最终的地图依据。
