快速开始：

```bash
npx skills add mattpocock/skills --skill=to-issues
```

```bash
npx skills update to-issues
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-issues)

## 它做什么

`to-issues` 将计划、spec 或 PRD 分解为一组可独立领取的 issues，并以依赖顺序发布到你项目的问题跟踪器。

每个 issue 都是一个**示踪子弹**——一个薄的*垂直*切片，端到端地穿越所有集成层（schema、API、UI、tests），从不是一个层的水平切片。一个完成的切片本身就可以演示或验证，这就是使生成的工单可以安全地交给独立 agent 的原因。

## 何时使用它

你通过输入 `/to-issues` 来调用它——agent 不会自行调用它。

一旦你有一个达成一致的计划或书面 spec，并且你想将其分解为 agent 可以领取的工单时使用它。将其指向对话，或者传入一个现有的 issue 引用，它会先获取正文和评论。如果变更尚未被写为 spec，先产生一个——为此，使用 [to-prd](https://aihero.dev/skills-to-prd)。

## 前置条件

`to-issues` 发布到你的问题跟踪器，因此 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必须首先为此仓库配置了跟踪器及其分类标签词汇。它在发布时自行应用 ready-for-agent 分类标签。

## 垂直切片，而非水平切片

整个 skill 围绕一个区别展开。**水平**切片交付变更的一层——所有 schema，或所有 API——在每一层落地之前没有东西能工作。**垂直**切片，即示踪子弹，一次交付一条穿越*每个*层的狭窄路径，因此它可以在完成的瞬间被演示。

在切片之前，`to-issues` 寻找预重构——"先让变更变得容易，然后做容易的变更"——并先排序这些工作。然后它在写任何东西之前就分解方式（粒度、依赖关系、合并或拆分什么）向你提问，并首先发布阻塞项，这样每个 issue 的 "Blocked by" 字段可以引用真实的工单。

## 它在哪里

`to-issues` 是主构建链中的一个步骤：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

它位于 [to-prd](https://aihero.dev/skills-to-prd)（交给它一个带有用户故事的可切片 spec）和 [implement](https://aihero.dev/skills-implement)（构建每个独立可领取的 issue，在内部驱动 [tdd](https://aihero.dev/skills-tdd) 以先测试方式编写测试，然后进行其 [code-review](https://aihero.dev/skills-code-review) 审查）之间。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
