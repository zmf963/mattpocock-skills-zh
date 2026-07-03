快速开始：

```bash
npx skills add mattpocock/skills --skill=prototype
```

```bash
npx skills update prototype
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype)

## 它做什么

`prototype` 构建一个小型、一次性程序，其唯一工作是回答一个设计问题——这个状态模型感觉对吗，或者这个 UI 应该长什么样。

代码从第一天起就是**一次性的**，并如此标记。它没有测试、没有超出使其运行所需的错误处理、没有抽象、没有持久化。重点是快速学到东西然后删除它——所以在你开始加固它的那一刻，你就停止了原型设计。

## 何时使用它

输入 `/prototype`，或者 agent 在任务匹配时自动调用它。

当你有一个难以在纸上解决的设计问题时使用它——一个有你不能在脑中持有的分支的状态机，或者一个直到你看到几个版本并排才能想象的屏幕。如果相反，某物已经构建但行为异常，你需要找出原因，使用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)；原型探索要构建什么，而不是为什么已构建的东西坏了。

## 两个分支

问题决定形态，有两种形态：

- **"这个逻辑/状态模型感觉对吗？"** — 一个微型交互式终端应用，将状态机推过尴尬的情况，在每个动作后打印完整状态，这样你可以观察什么变了。
- **"这应该长什么样？"** — 一个路由上的几个截然不同的 UI 变体，可从浮动栏切换，这样你可以比较真实渲染而不是想象它们。

选错分支会浪费整个原型，所以问题先来。两个分支都将状态保留在内存中，从一个命令运行，并在每一步显示完整状态。

## 答案就是产物

代码是一次性的；**答案**是唯一值得保留的东西。当原型解决了其问题，将结论捕获到某个持久的地方——一条 commit 消息、一个 ADR、一个 issue，或旁边的 `NOTES.md`——连同它回答的问题，然后删除或吸收代码。一个留在仓库中腐烂的原型已经超出了其目的。

## 它在哪里

`prototype` 是一个随时可用的独立 skill：你进入它来解决一个设计问题，然后退出。它的答案通常为下一步提供输入——一个验证过的状态模型或 UI 方向成为 [to-prd](https://aihero.dev/skills-to-prd) 要写出的确定输入，或通过 [domain-modeling](https://aihero.dev/skills-domain-modeling) 值得记录的架构决策。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
