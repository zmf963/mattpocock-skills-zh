Quickstart:

```bash
npx skills add mattpocock/skills --skill=code-review
```

```bash
npx skills update code-review
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review)

## 作用

`code-review` 审查 `HEAD` 与你提供的某个固定点（提交、分支、标签或 merge-base）之间的 diff，沿着两条独立的维度进行：**标准**（代码是否遵循此仓库的文档化约定？）和 **规格**（代码是否实现了原始 issue 或 PRD 的要求？）。它让每个维度作为自己的并行子代理运行，并排呈现结果。它从不合并或重新排序这两组发现——保持它们分离正是关键所在，因为一个变更可能通过一个维度却失败于另一个，而单一的混合结论会让一个维度掩盖另一个。

## 何时使用

输入 `/code-review`，或者当你要求审查某个分支、PR、进行中的变更或"自 X 以来"的任何内容时，代理会自动调用它。

当存在一个需要对照已知良好点进行评判的 diff，并且你希望两个问题——*构建得是否正确？* 和 *是否构建了正确的东西？*——得到独立回答时使用。它在构建循环的末尾运行；对于实际编写测试优先的代码，请使用 [tdd](https://aihero.dev/skills-tdd)；对于将整个规格构建为代码，请使用 [implement](https://aihero.dev/skills-implement)，它会在提交前自行运行 `/code-review` 环节。

## 前置条件

**规格**维度需要能找到原始规格——可以是提交消息中的 issue 引用、你传入的路径，或位于 `docs/`/`specs/` 下的 PRD。这个 issue-tracker 连线来自 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills)；如果没有规格，规格维度会直接跳过并如实说明。**标准**维度不需要任何设置——即使在没有文档化约定的仓库中，它也始终携带内置的 Fowler 坏味道基线。

## 两个维度，从不合并

核心思想是**两个维度**。**标准**询问 diff 是否符合此仓库的代码编写方式——其 `CODING_STANDARDS.md` 或 `CONTRIBUTING.md`，加上约 12 个 Fowler 代码坏味道的固定基线（神秘命名、重复代码、依恋情结、数据泥团等）。两条规则保护基线的安全性：文档化的仓库标准始终覆盖基线，且每个坏味道都是判断性调用，而非硬性违规。**规格**询问正交的问题——代码是否真正做了 issue 或 PRD 所要求的事情，既不遗漏需求也不夹带范围蔓延。

它们作为并行的子代理运行，这样任何一个都不会污染另一个的上下文，最终报告在独立的 `## Standards` 和 `## Spec` 标题下呈现，每个维度有各自的摘要。故意不设统一的跨维度胜者。

## 验证标准

- 它首先定位并确认固定点（`git rev-parse`），遇到错误的引用或空的 diff 时快速失败，而不是在子代理内部才失败。
- 标准和规格的发现结果分为两个不同的区块呈现，每个区块引用其来源——对于标准，引用仓库标准或基线坏味道；对于规格，引用规格中的具体行。
- 当找不到规格时，规格维度报告"无可用规格"，而不是凭空想出需求。

## 所处位置

`code-review` 是主构建链末尾的审查步骤：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

它最近的邻居是 [implement](https://aihero.dev/skills-implement)，后者驱动构建并在提交前将本技能作为自身的审查环节调用；上游，它检查的规格由 [to-prd](https://aihero.dev/skills-to-prd) 和 [to-issues](https://aihero.dev/skills-to-issues) 生成。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
