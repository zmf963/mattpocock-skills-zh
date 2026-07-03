Quickstart:

```bash
npx skills add mattpocock/skills --skill=improve-codebase-architecture
```

```bash
npx skills update improve-codebase-architecture
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture)

## 作用

`improve-codebase-architecture` 扫描代码库寻找**加深机会**——即浅层模块（接口几乎和它所隐藏的东西一样复杂）可以变成深层模块的地方——以独立的可视化 HTML 报告形式呈现，然后在你选择其中一个时进行盘问。

它**不会**给你一张扁平的重构清单。每个候选者必须通过**删除测试**——移除这个模块是会将复杂度*集中*到更小的接口后面，还是仅仅将其搬来搬去？只有"集中复杂度"的情况才能获得一张卡片。这个筛选器正是防止报告变成泛泛的清理建议的关键。

## 何时使用

你需要通过输入 `/improve-codebase-architecture` 来调用它——代理不会自行触发。

将其作为定期健康检查使用：每隔几天，或者每当代码库开始让人觉得为了理解一个概念需要在太多小模块之间跳转时使用。它读取现有的架构并提出在哪些地方加深它。如果你已经知道要重新设计的模块，只需要思考所需的词汇，请使用 [codebase-design](https://aihero.dev/skills-codebase-design)——这个技能是发现候选者的调查工具，而那个是设计工作台。

## 加深机会

整个技能围绕一个想法展开：**深度**。深层模块将大量功能隐藏在小型、稳定的接口后面；浅层模块通过几乎和底层代码一样宽的接口泄露其实现。报告会寻找浅层性——仅为可测试性而提取的纯函数，而真正的 bug 隐藏在它们被调用的方式中（没有**局部性**）、泄露到其**接缝**之外的模块、以及不打开五个文件就无法理解的概念——并提出可以修复问题的加深方案。

它使用共享的设计词汇（**module**、**interface**、**depth**、**seam**、**adapter**、**leverage**、**locality**）和来自 `CONTEXT.md` 的项目自身领域语言，因此候选者读起来像是"加深 Order 接收模块"，而不是"重构 FooBarHandler"。

## 报告，然后盘问

输出是一个浏览器可读的 HTML 文件，写入你的 OS 临时目录——不会进入仓库。每个候选者是一张卡片，包含涉及的文件、摩擦点、用通俗语言描述的解决方案、在局部性和杠杆率方面的收益、改造前/后图示，以及 `Strong` / `Worth exploring` / `Speculative` 徽章。报告最后会给出它会优先处理哪一个。

然后它停下来，询问你想探索哪一个。选择一个后，它会在该设计上运行 [grilling](https://aihero.dev/skills-grilling) 循环——约束条件、接缝后面是什么、哪些测试能够存活——在决策明确时实时更新领域模型。

## 所处位置

`improve-codebase-architecture` 是**定期维护**——每隔几天运行一次，而不是作为链条中的某个步骤。它的邻居是 [codebase-design](https://aihero.dev/skills-codebase-design)（拥有每个候选者所依据的深度和接缝词汇）、[grilling](https://aihero.dev/skills-grilling)（在你选定候选者后遍历设计树）、以及 [domain-modeling](https://aihero.dev/skills-domain-modeling)（在重新设计方案确定时保持 `CONTEXT.md` 和 ADR 的最新状态）。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
