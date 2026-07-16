快速开始：

```bash
npx skills add mattpocock/skills --skill=to-tickets
```

```bash
npx skills update to-tickets
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets)

## 它做什么

`to-tickets` 将计划、spec 或当前对话拆分为一组**票据**——每个都是曳光弹垂直切片——并发布到你配置的跟踪器，每张票据声明阻塞它的票据。

每张票据都是一枚**曳光弹**——一条薄薄的*垂直*切片，端到端贯穿所有集成层（schema、API、UI、tests），永远不是单层的水平切片。已完成的切片可以独立演示或验证，这正是让每张票据安全交给 agent 的原因。

## 何时使用

你通过输入 `/to-tickets` 来调用它——agent 不会自己触发它。

当你有一个已达成共识的计划或一份写好的 spec，且你想将其拆分为票据时使用。将它指向对话，或传入 spec 或 issue 引用，它会先获取正文和评论。如果变更还没有写成 spec，先产出一份——用 [to-spec](https://aihero.dev/skills-to-spec)。

## 前置条件

`to-tickets` 发布到你的 issue 跟踪器，所以 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必须预先为这个仓库配置好跟踪器和 triage 标签词汇表。在真正的跟踪器上，它在发布时应用 ready-for-agent 标签。

## 一件产物，两种解读

阻塞边是全部的意义所在。它们让同一组票据有两种解读方式，取决于跟踪器：

- **本地文件** → `.scratch/<feature>/issues/` 下每张票据一个文件，按阻塞者优先编号，阻塞边以文本形式写出。你从上到下手动处理它们，留在循环中。
- **真正的跟踪器（GitHub、Linear）** → 每个票据一个 issue，阻塞边作为原生阻塞链接（或子 issue）。阻塞者全部完成的任何票据处于**前沿**，可以被接走——所以多个 agent 可以同时运行。

阻塞边存在于票据中，不管媒介是什么；媒介只决定是否有人并行处理它们。`to-tickets` 产出产物——你如何运行它（手动串行，还是并行舰队）取决于你。

## 垂直切片，不是水平切片

整个 skill 围绕一个区别展开。一个**水平**切片只交付变更的一层——所有 schema，或所有 API——在所有层都落地之前什么都不能工作。一个**垂直**切片，曳光弹，一次性贯穿*所有*层交付一条狭窄路径，所以它一完成就能演示。

在切片之前，`to-tickets` 寻找预重构——"让变更变得容易，然后做出容易的变更"——并将该工作排在前面。然后它在发布任何内容之前向你询问拆解方案（粒度、阻塞边、合并或拆分什么），并先发布阻塞者，这样每张票据的"被阻塞于"可以引用真实的票据。

## 宽重构例外

有一种形状打破曳光弹规则：**宽重构**——一种机械性变更（重命名列、变更共享符号的类型），其**影响范围**遍布整个代码库，一次编辑就破坏数千个调用点，没有垂直切片能独立通过。`to-tickets` 将其作为**展开——收缩**来切片：展开（在旧形式旁边添加新形式以避免破坏），迁移（按影响范围分批移动调用点，每批一张票据，整个过程中 CI 保持绿色因为旧形式仍然存在），然后收缩（在没有任何调用者后删除旧形式）。当即使批次也无法独立保持绿色时，它们共享一个集成分支，所有批次都阻塞一张最终的集成验证票据，只有在那张那里才承诺绿色。

## 它在哪里嵌入

`to-tickets` 是主构建链中的一步：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它位于 [to-spec](https://aihero.dev/skills-to-spec)（交付一份已确定的 spec 和用户故事作为切片依据）和 [implement](https://aihero.dev/skills-implement)（构建每张票据，内部驱动 [tdd](https://aihero.dev/skills-tdd) 以测试先行方式编写测试，然后经过 [code-review](https://aihero.dev/skills-code-review) 审查）之间。在全新的上下文中一次处理一张前沿票据，票据之间清空上下文。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你导航。
