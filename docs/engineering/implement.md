Quickstart:

```bash
npx skills add mattpocock/skills --skill=implement
```

```bash
npx skills update implement
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement)

## 作用

`implement` 构建 PRD 或一组 issue 中所描述的工作——驱动它通过测试驱动开发、类型检查和完整的测试套件，然后交接给审查并提交到当前分支。

它**不决定**要构建什么。规格已经确定，接缝已经达成一致；`implement` 执行该计划，而不是重新讨论它。它是执行的手，而非决策的脑——思考工作已在上游完成。

## 何时使用

你需要通过输入 `/implement` 来调用它——代理不会自行触发。

当工作已被写成 PRD 或拆分为 issue，并且你准备好将其转化为代码时使用它。如果规格还不存在，先编写规格——为此，请使用 [to-prd](https://aihero.dev/skills-to-prd)，或使用 [to-issues](https://aihero.dev/skills-to-issues) 将 PRD 拆分为工单。如果你只想在没有完整规格的情况下测试优先地构建一些东西，直接使用 [tdd](https://aihero.dev/skills-tdd)。

## 预先商定的接缝

`implement` 运行所基于的核心概念是**接缝**——功能在其上进行测试的稳定接口，在编写任何代码之前就选定。它不会在构建过程中发明接缝；它使用已经选好的接缝（在 [to-prd](https://aihero.dev/skills-to-prd) 期间选定），并通过 [tdd](https://aihero.dev/skills-tdd) 针对它们编写测试。在预先商定的接缝上工作是保持实现诚实的关键：测试针对持久的目标，因此底层的代码可以变动而测试无需跟着变动。

围绕这个核心，它保持循环紧凑——频繁进行类型检查、过程中运行单个测试文件、最后运行一次完整测试套件——然后以审查环节和对当前分支的提交来收尾。

## 所处位置

`implement` 是主链接近末尾处的构建步骤，恰在审查之前：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

在工作已被规划和排序之后（而非之前）使用它。它的关键邻居是 [to-issues](https://aihero.dev/skills-to-issues)，后者生成它可以逐个处理的独立可抓取工单；以及 [tdd](https://aihero.dev/skills-tdd)，它在内部驱动以在每个接缝处编写测试，然后运行自身的 [code-review](https://aihero.dev/skills-code-review) 环节并提交。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
