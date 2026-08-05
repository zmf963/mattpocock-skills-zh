<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 给真正工程师用的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

我每天用来做真工程（而不是"氛围编程"）的 agent skills。

开发真正的应用很难。GSD、BMAD、Spec-Kit 这类方案试图通过"接管流程"来帮忙。但与此同时，它们剥夺了你的掌控权，还让流程本身出问题时难以解决。

这些 skills 被设计得小巧、易改造、可组合。它们适用于任何模型。它们建立在数十年的工程经验之上。随便折腾它们，把它们变成你自己的。Enjoy。

如果你想跟上这些 skills 的变动，以及我新做的任何 skill，可以加入我 newsletter 上约 60,000 名其他开发者：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 安装（30 秒配置）

两条路，两种哲学。**[Claude Code 插件](https://code.claude.com/docs/en/plugins)** 将整个 skill 集安装为受管理的只读捆绑包，在我发布新版本时更新——你订阅而非 fork。**[skills.sh](https://skills.sh/mattpocock/skills)** 将可编辑的 skill 文件复制到你的项目中，所以你可以折腾它们，把它们变成自己的。二选一——两者都装会让你把每个 skill 复制两份。

### 1. 获取 skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者，在会话内：

```
/plugin install mattpocock-skills
```

它位于 Claude Code 的官方市场里，所以无需先添加任何东西，更新也会自动到达。

</details>

<details>
<summary><strong>Codex 以及其他 agent</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

选择你想要的 skills，以及想把它们安装到哪些 coding agent 上。**安装器会让你选择要带走哪些 skills——确保 `setup-matt-pocock-skills` 是其中之一。**

原生 Codex 插件在路线图上——参见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

</details>

<details>
<summary><strong>给喜欢折腾的人</strong></summary>

在任意 agent 上使用同一个安装器——包括 Claude Code：

```bash
npx skills@latest add mattpocock/skills
```

它会将 skills 写入你的仓库，作为你拥有且可编辑的普通文件。没有任何东西会在背后自动更新；当你想拉取我的最新变更时，用 `npx skills update`。

</details>

### 2. 运行 `/setup-matt-pocock-skills`

在你的 agent 中，每个仓库运行一次。它会：

- 询问你想用哪个 issue 跟踪器（GitHub、Linear，或本地文件）
- 询问你在 triage（分诊）工单时使用的标签（`/triage` 会用到标签）
- 询问你想把生成的文档保存在哪里

### 3. 搞定——可以开干了。

## 为什么会有这些 Skills

我打造这些 skills，是为了修复我在 Claude Code、Codex 等 coding agent 上常见的失败模式。

### #1：Agent 没按我想要的来做

> "没有人能确切知道他们想要什么"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》(The Pragmatic Programmer)

**问题**。软件开发中最常见的失败模式就是"对不齐"。你以为开发者知道你想要什么。然后你看到他做出来的东西——才意识到他根本没理解你。

AI 时代也一样。你和 agent 之间存在沟通鸿沟。解决办法就是一场 **grilling 会话**——让 agent 就你要构建的东西向你追问大量细节问题。

**解决办法** 是用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) —— 用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) —— 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但附带更多"好东西"（见下）

这是我最受欢迎的 skills。它们能让你在动手前就与 agent 对齐，并深入思考你正在做的改动。每次想做改动时都用它们。

### #2：Agent 太啰嗦

> 有了通用语言（ubiquitous language），开发者之间的对话和代码的表达都源自同一个领域模型。
>
> Eric Evans，《领域驱动设计》(Domain-Driven Design)

**问题**：项目开始时，开发者和他们为之构建软件的人（领域专家）通常说着不同的"语言"。

我和我的 agents 之间也有同样的张力。Agents 通常被直接丢进项目，然后被要求边做边搞懂那些行话。于是它们用 20 个词说 1 个词就能说清的事。

**解决办法** 就是一套共享语言。它是一份文档，帮助 agent 解码项目中使用的行话。

<details>
<summary>
示例
</summary>

这是我的 `course-video-manager` 仓库里一份 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 的示例。哪个更好读？

- **改动前**："当课程里某个 section 下的 lesson 被 'materialized'（即被赋予文件系统里的位置）时，出了个问题"
- **改动后**："materialization cascade 出了问题"

这种简洁在每一轮会话里都回馈给你。

</details>

这内建于 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)。它是一场 grilling 会话，但同时帮你与 AI 共建共享语言，并把难以解释的决策写成 ADR。

很难形容这有多强大。它可能是这个仓库里最酷的单项技巧。试试看就知道了。

> [!TIP]
> 共享语言除了减少啰嗦，还有很多好处：
>
> - **变量、函数和文件的命名更一致**，都使用共享语言
> - 因此，agent **更容易在代码库中导航**
> - agent **思考时消耗的 token 也更少**，因为它有了更简洁的语言

### #3：代码跑不起来

> "永远采取小而审慎的步骤。反馈的速率就是你的速度上限。永远不要接手过于庞大的任务。"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》

**问题**：假设你和 agent 已经对齐了要构建什么。那当 agent *仍然*产出垃圾代码时，会发生什么？

是时候审视你的反馈环了。如果对你产出的代码实际如何运行没有任何反馈，agent 就是在盲飞。

**解决办法**：你需要常规的一整套反馈环：静态类型、浏览器访问，以及自动化测试。

对自动化测试而言，红-绿-重构循环至关重要。也就是 agent 先写一个失败的测试，再去修复它。这能给 agent 持续稳定的反馈，从而产出好得多的代码。

我做了一个可以塞进任何项目的 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**，它倡导红-绿-重构，并给 agent 大量关于"什么是好测试、什么是坏测试"的指导。

对调试，我还做了一个 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md) skill**，把最佳调试实践封装进一个简单的循环。

### #4：我们造了一团乱麻（Ball Of Mud）

> "每天都要投资于系统的设计。"
>
> Kent Beck，《解析极限编程》(Extreme Programming Explained)

> "最好的模块是深的。它们让大量功能通过一个简单的接口被访问。"
>
> John Ousterhout，《软件设计的哲学》(A Philosophy Of Software Design)

**问题**：大多数用 agent 构建的应用都复杂且难以改动。因为 agent 能极大地加速编码，它们也加速了软件的熵增。代码库以空前的速率变得更复杂。

**解决办法** 是一种激进的 AI 驱动开发新思路：在乎代码的设计。

这内建于这些 skills 的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 会在创建 spec 前，就你会碰到哪些模块向你提问

而关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 能帮你挽救一个已经变成乱麻的代码库。我建议每隔几天就在你的代码库上跑一次。

### 总结

软件工程的基本功比以往任何时候都更重要。这些 skills 是我把这些基本功浓缩成可重复实践的最大努力，帮你交付职业生涯中最好的应用。Enjoy。

## 参考

这些 skills 按一个维度划分——谁能调用它们。**用户调用（User-invoked）** skills 只有当你键入时才可达（例如 `/grill-me`）；它们的职责是编排。**模型调用（Model-invoked）** skills 既可由你调用，也可在任务匹配时由 agent 自动选用；它们承载可复用的纪律。用户调用的 skill 可以调用模型调用的 skill，但绝不会调用另一个用户调用的 skill。

### 工程（Engineering）

我每天用于写代码的 skills。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** —— 询问哪个 skill 或流程适合你的情况。本仓库用户调用 skills 之上的一个路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** —— 一场 grilling 会话，同时构建你项目的领域模型，打磨术语，并就地更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** —— 让 issue 流经一套 triage 角色的状态机。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** —— 扫描代码库寻找"加深"机会，以可视化 HTML 报告呈现，然后就你选中的那一个进行 grilling。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** —— 为工程类 skills 配置本仓库（issue 跟踪器、triage 标签、领域文档布局）。使用其他工程类 skills 前，每个仓库运行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** —— 把当前对话转化为一份 spec 并发布到 issue 跟踪器。无需访谈——只是综合你已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** —— 把任意计划、spec 或对话拆成一组曳光弹票据，每张票据声明它的阻塞边——本地文件中以文本形式写出，或在真正的跟踪器上以原生阻塞链接形式。
- **[implement](./skills/engineering/implement/SKILL.md)** —— 构建 spec 或一组票据所描述的工作，在预先商定的接缝处驱动 `/tdd`，提交前用 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** —— 规划一项巨大工作（一个 agent 会话装不下的），在 issue 跟踪器上作为一张调查票据的共享地图——逐一解决它们，直到通往目的地的路径清晰。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)** —— 构建一个一次性原型来回答一个设计问题——针对状态/逻辑问题是一个可运行的终端应用，或从一个路由切换的几种截然不同的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** —— 针对难解 bug 和性能回归的自律诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** —— 针对高可信一手来源调查一个问题，并把发现捕获为仓库中一份带引用的 Markdown 文件，作为后台 agent 运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** —— 测试驱动开发，带红-绿-重构循环。一次一个垂直切片地构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** —— 主动构建并打磨项目的领域模型——用术语表对照检验术语、用边界场景压力测试，并就地更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** —— 设计深模块的一套共享纪律与词汇：大量行为藏在小小的接口之后，放在干净的接缝处，通过该接口可测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)** —— 从两个轴审查自某个固定点以来的 diff：**标准（Standards）**（它是否遵循仓库的编码标准，外加一个 Fowler 坏味道基线？）和 **规格（Spec）**（它是否忠实地实现了原始 issue/PRD？），作为并行子 agent 运行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** —— 逐块处理进行中的 git merge 或 rebase 冲突，通过追溯到每一边的主要来源的意图来解决，然后完成操作——永远不用 `--abort`。

### 效率（Productivity）

通用的流程工具，不特定于代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** —— 就一个计划或设计被 relentless 地采访，直到决策树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** —— 把当前对话压缩成一份 handoff 文档，以便另一个 agent 继续工作。
- **[teach](./skills/productivity/teach/SKILL.md)** —— 在多个会话中教用户一项新技能或概念，把当前目录当作有状态的教学工作区。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** —— 编写和编辑好 skills 的参考：让一个 skill 可预测的词汇与原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** —— relentlessly 地就一个计划、决策或想法采访用户，直到决策树的每个分支都被解决。`grill-me` 和 `grill-with-docs` 背后可复用的循环。
