快速开始：

```bash
npx skills add mattpocock/skills --skill=to-spec
```

```bash
npx skills update to-spec
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec)

## 它做什么

`to-spec` 将当前对话和对代码库的理解转化为一份 spec（你可能称这份文档为 PRD），然后将其发布到你的 issue 跟踪器。

它**不会**再次访谈你。当你使用它时，对齐工作已经完成——`to-spec` 综合已经知道的内容，而不是再问一轮新问题。

## 何时使用

你通过输入 `/to-spec` 来调用它——agent 不会自己触发它。

当一个变更已经被讨论透彻、领域语言已确定，且你希望在写任何代码之前将那份共识写下来时使用。如果你*还没有*对齐，先做 grilling——用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。要将完成的 spec 拆分为票据，使用 [to-tickets](https://aihero.dev/skills-to-tickets)。

## 前置条件

`to-spec` 发布到你的 issue 跟踪器，所以 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必须预先为这个仓库配置好跟踪器和 triage 标签。它自己会应用 `ready-for-agent` 标签——不需要单独的 triage 流程。

## spec 包含什么

- **问题陈述**——什么坏了或缺失了，以及为什么值得解决，使用项目自身的词汇。
- **解决方案**——修复在高层次上的形状，在任何实现细节之前。
- **用户故事**——一份详尽、编号的列表，描述变更必须支持的具体行为，每一条都可独立检查。
- **实施决策**——在对话中已经确定的选择，以免日后反复争论。
- **测试决策**——该功能将在哪些接缝处被测试，"完成"是什么样子。
- **范围外项目**——这次变更刻意*不*涵盖什么，以保持票据边界清晰。
- **补充说明**——值得传递的其他任何内容，不适合以上各节的。

## 深模块

在写 spec 之前，`to-spec` 草拟该功能将在哪些**接缝**处被测试，并寻找**深模块**机会——大量功能隐藏在一个小巧、稳定的接口后面。它优先使用已有接缝而非新建，尽可能使用最高层的接缝，理想情况下整个变更只有一个接缝。

这对 agentic 开发很关键：一个好的接口让测试有一个持久的目标，这样接口下面的代码可以变化而测试不需要变动。

## 它有效的标志

- 它开始写 spec，而不是问你新一轮问题。
- 它在写之前与你确认接缝，并提议尽可能少的接缝。
- spec 使用你项目自身的领域词汇，而不是通用模板。

## 它在哪里嵌入

`to-spec` 是主构建链中的一步：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

在计划和领域语言确定之后、将工作拆分为实施票据之前使用它。它的关键邻居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)，它磨利上下文使 spec 精确，以及 [to-tickets](https://aihero.dev/skills-to-tickets)，它将 spec 转化为一组票据供 [implement](https://aihero.dev/skills-implement) 构建。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你导航。
