<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 给真正工程师的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

我每天都在用的 agent skills，用来做真正的工程——不是 vibe coding。

开发真实应用很难。像 GSD、BMAD 和 Spec-Kit 这样的方法试图通过掌控流程来帮忙。但这样做的同时，它们剥夺了你的控制权，并让流程中的 bug 难以解决。

这些 skills 被设计为小巧、易于适配且可组合的。它们适用于任何模型。它们基于数十年的工程经验。随意修改它们。把它们变成你自己的。享受吧。

如果你想跟进这些 skills 的变化以及我创建的新 skills，可以加入我 newsletter 上的约 60,000 名其他开发者：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 快速开始（30 秒设置）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的 skills，以及要安装到哪些编程 agent 上。**确保选择 `/setup-matt-pocock-skills`**。

3. 在你的 agent 中运行 `/setup-matt-pocock-skills`。它会：
   - 询问你想使用哪个问题跟踪器（GitHub、Linear 或本地文件）
   - 询问你在分类时为工单应用什么标签（`/triage` 使用标签）
   - 询问你想将我们创建的任何文档保存在哪里

4. 搞定——你就可以开始了。

## 为什么要有这些 Skills

我构建这些 skills 是为了解决我在 Claude Code、Codex 和其他编程 agent 中看到的常见失败模式。

### #1：Agent 没按我想的做

> "没有人确切知道自己想要什么"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》

**问题**。软件开发中最常见的失败模式是认知偏差。你以为开发者知道你想要什么。然后你看到他们构建的东西——你意识到它完全没理解你的意图。

在 AI 时代也是一样。你与 agent 之间存在沟通鸿沟。解决方法是进行**深入追问**——让 agent 就你正在构建的东西向你提出详细问题。

**解决方案**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) - 用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) - 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但增加了更多好东西（见下文）

这些是我最受欢迎的 skills。它们帮助你在开始之前与 agent 对齐，并深入思考你正在做的变更。**每次**你想做变更时都使用它们。

### #2：Agent 太啰嗦了

> 有了通用语言，开发者之间的对话和代码的表达都源自同一个领域模型。
>
> Eric Evans，《领域驱动设计》

**问题**：在项目开始时，开发者和他们为其构建软件的人（领域专家）通常说着不同的语言。

我对我的 agent 也有同样的感受。Agent 通常被丢进一个项目，被要求边做边理解术语。所以它们用 20 个词来表达 1 个词就能说清楚的事情。

**解决方案**是共享语言。这是一个帮助 agent 解码项目中使用的术语的文档。

<details>
<summary>
示例
</summary>

这是来自我的 `course-video-manager` 仓库的一个 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪个更容易阅读？

- **之前**："课程中某个章节的课程被设为'真实'（即在文件系统中分配了位置）时出现问题"
- **之后**："物化级联有问题"

这种简洁性在一次又一次的会话中都会带来回报。

</details>

这已内置在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 中。这是一次深入追问，但帮助你与 AI 建立共享语言，并将难以解释的决策记录在 ADR 中。

很难解释这有多强大。它可能是这个仓库中最酷的技术。试试看吧。

> [!TIP]
> 共享语言除了减少冗余之外还有很多好处：
>
> - **变量、函数和文件命名一致**，使用共享语言
> - 因此，**代码库对 agent 来说更容易导航**
> - agent 在思考上**花费更少的 token**，因为它可以使用更简洁的语言

### #3：代码不工作

> "始终采取小而审慎的步骤。反馈的速度就是你的速度上限。永远不要承担太大的任务。"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》

**问题**：假设你和 agent 在要构建什么上已经对齐。当 agent 仍然产出垃圾代码时会发生什么？

是时候审视你的反馈循环了。如果对代码实际运行情况没有反馈，agent 就是在盲目飞行。

**解决方案**：你需要通常的反馈循环组合：静态类型、浏览器访问和自动化测试。

对于自动化测试，红-绿-重构循环至关重要。这就是 agent 先写一个失败的测试，然后修复测试。这有助于给 agent 提供一致水平的反馈，从而产生更好的代码。

我构建了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**，你可以插入到任何项目中。它鼓励红-绿-重构，并给 agent 提供大量关于好测试和坏测试的指导。

对于调试，我还构建了一个 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill，将最佳调试实践包装成一个简单的循环。

### #4：我们构建了一个泥球

> "每天都要投资于系统的设计。"
>
> Kent Beck，《解析极限编程》

> "最好的模块是深的。它们允许通过简单的接口访问大量功能。"
>
> John Ousterhout，《软件设计的哲学》

**问题**：大多数用 agent 构建的应用复杂且难以更改。因为 agent 可以极大地加速编码，它们也加速了软件熵增。代码库以前所未有的速度变得更加复杂。

**解决方案**是采用一种全新的 AI 驱动开发方法：关心代码的设计。

这已内建在这些 skills 的每一层中：

- [`/to-prd`](./skills/engineering/to-prd/SKILL.md) 在创建 PRD 之前询问你将触及哪些模块

而且关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 帮助你拯救一个已经变成泥球的代码库。我建议每隔几天在你的代码库上运行一次。

### 总结

软件工程基础知识比以往任何时候都更重要。这些 skills 是我将这些基础知识浓缩为可重复实践的最佳努力，帮助你在职业生涯中交付最好的应用。享受吧。

## 参考

这些 skills 在一个轴上划分——谁能调用它们。**用户调用**的 skills 只有在你输入时才能访问（例如 `/grill-me`）；它们的工作是编排。**模型调用**的 skills 可以由你调用，也可以由 agent 在任务匹配时自动调用；它们包含可复用的规则。一个用户调用的 skill 可以调用模型调用的 skills，但不能调用另一个用户调用的 skill。

### 工程

我每天用于代码工作的 skills。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** — 询问哪个 skill 或流程适合你的情况。是此仓库中用户调用 skills 的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — 深入追问，同时构建你项目的领域模型，精炼术语并内联更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 将 issues 移过一个分类角色状态机。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 扫描代码库寻找深化机会，以可视化 HTML 报告呈现，然后对你选择的那一个进行深入追问。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 为此仓库配置工程 skills（问题跟踪器、分类标签、领域文档布局）。在使用其他工程 skills 之前，每个仓库运行一次。
- **[to-issues](./skills/engineering/to-issues/SKILL.md)** — 将任何计划、spec 或 PRD 分解为使用垂直切片可独立领取的 issues。
- **[to-prd](./skills/engineering/to-prd/SKILL.md)** — 将当前对话转换为 PRD 并发布到问题跟踪器。无需面试——只是综合你已经讨论过的内容。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)** — 构建一个一次性原型来回答设计问题——一个可运行的终端应用用于状态/逻辑问题，或几个可从同一路由切换的截然不同的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** — 针对困难 bug 和性能回归的有纪律的诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** — 针对高信任度的主要来源调查问题，并将发现捕获为仓库中的带引用 Markdown 文件，作为后台 agent 运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 带有红-绿-重构循环的测试驱动开发。一次一个垂直切片地构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** — 积极构建和精炼项目的领域模型——用术语表挑战术语，用边界场景进行压力测试，并内联更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** — 设计深层模块的共享规则和词汇：大量行为通过小型接口暴露，放置在干净的接缝处，可通过该接口测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)** — 从固定点开始的 diff 双轴审查：**标准**（是否遵循仓库的编码标准，加上 Fowler 坏味道基线？）和**规格**（是否忠实实现了原始 issue/PRD？），作为并行子 agent 运行，互不污染。

### 生产力

通用工作流工具，不特定于代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 对计划或设计进行无情的面试，直到决策树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 将当前对话压缩为交接文档，以便另一个 agent 可以继续工作。
- **[teach](./skills/productivity/teach/SKILL.md)** — 通过多个会话教授用户新技能或概念，使用当前目录作为有状态的教学工作区。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** — 编写和编辑 skills 的参考：使 skill 可预测的词汇和原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** — 对计划或设计进行无情的面试，直到决策树的每个分支都被解决。`grill-me` 和 `grill-with-docs` 背后的可复用循环。
