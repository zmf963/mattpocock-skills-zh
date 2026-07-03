Quickstart:

```bash
npx skills add mattpocock/skills --skill=codebase-design
```

```bash
npx skills update codebase-design
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)

## 作用

`codebase-design` 为你提供一套共享、精确的词汇，用于设计**深层模块**——大量行为隐藏在小型接口之后，放置在清晰的接缝处，通过该接口可进行测试。

它是一种**语言，而非步骤**。它不会重构你的代码或给你一个重构计划——它固定了词汇（module、interface、depth、seam、adapter、leverage、locality），使每次设计对话和每个涉及设计的技能都以相同的方式表达。一致的用语是核心目的；"component"、"service"、"API"和"boundary"被刻意禁用，因为它们模糊了真正重要的区别。

## 何时使用

输入 `/codebase-design`，或者当任务适当时代理会自动调用它。

当你正在设计或改进模块的接口、寻找加深机会、决定接缝应该放在哪里、或使代码更易于测试和 AI 导航时使用。其他技能在需要深层模块词汇时会引入它。如果你想精炼项目的*领域*术语而非模块设计，请使用 [domain-modeling](https://aihero.dev/skills-domain-modeling)；要对现有代码库进行完整的架构评估，请使用 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。

## 深层，而非浅层

当大量行为位于小型接口之后时，模块就是**深层**的；当接口几乎与实现一样复杂时，模块就是**浅层**的。深度以**杠杆率**来衡量——调用者（或测试）每学习一个单位的接口能执行多少操作。关键在于，深度是*接口*的属性，而非实现：一个深层模块内部可以由小型、可替换的部件组成，但这些部件从不暴露给调用者。

两个检查方法完成了大部分工作。**删除测试**：想象删除该模块——如果复杂度消失了，说明它只是个传声筒；如果复杂度重新出现在 N 个调用者中，说明它物有所值。还有**一个适配器意味着假设的接缝；两个适配器意味着真正的接缝**——直到有东西真正跨接缝变化时，才去切开一个接缝。

## 接口就是测试面

调用者和测试跨越同一个接缝，所以一个放置得当的接口为测试提供了持久的目标，而底层的代码可以自由变动。这就是为什么词汇坚持使用**seam**（Feathers 的术语——一个可以在不编辑原处的情况下改变行为的地方）而不是已经被过度使用的"boundary"，以及为什么这里的"interface"意指*调用者需要知道的全部事实*：签名当然包括，但也包括不变量、顺序、错误模式和性能——而不仅仅是类型层面的表面。

## 特意独立出来

`codebase-design` 是深层模块词汇的**单一可信来源**，它作为独立的模型自动调用技能被拆分出来，以便任何其他技能都能引用它。其他技能指向它而不是重复表述这些词汇：[tdd](https://aihero.dev/skills-tdd) 借用它在编写测试之前放置接缝，[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在重构现有代码时依赖它，[to-prd](https://aihero.dev/skills-to-prd) 在编写规格之前用它来描绘接缝和加深机会。

保持其独立的意义在于，你也可以单独调用它——作为思考模块设计的**参考**——而无需触发其他任何技能所规定的更大流程。把词汇固定下来，固定在一个地方，每次设计对话都会继承它们。

## 所处位置

`codebase-design` 是一个**随时可调用的独立技能**——是工程技能之下的共享词汇层。它最近的邻居是 [domain-modeling](https://aihero.dev/skills-domain-modeling)，后者是问题领域而非模块结构的平行词汇技能。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
