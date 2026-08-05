快速开始：

```bash
npx skills add mattpocock/skills --skill=code-review
```

```bash
npx skills update code-review
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review)

## 作用

`code-review` 审查 `HEAD` 与你提供的某个固定点——一个 commit、分支、tag 或 merge-base——之间的 diff，沿两个**独立的轴**进行：**标准（Standards）**（代码是否遵循此仓库记录在案的约定？）和**规格（Spec）**（它是否实现了起源 issue 或 spec 要求的东西？）。它把每个轴作为各自的并行子 agent 运行，并排呈现结果。它从不合并或重新排序这两组发现——让它们分开正是全部意义所在，因为一项变更可能通过一个轴而失败于另一个轴，而单一的混合裁决会让一个掩盖另一个。

## 何时使用

输入 `/code-review`，或者当你要求审查一个分支、一个 PR、进行中的变更，或任何"自 X 以来"的东西时，agent 会自动调用它。

当存在一个 diff 要对照已知良好点来评判，而你希望那两个问题——*构建得对吗？* 和 *是对的东西吗？*——被独立回答时使用。它在构建循环的末尾运行；要用测试先行方式实际编写代码，使用 [tdd](https://aihero.dev/skills-tdd)，要构建整个 spec 成代码，使用 [implement](https://aihero.dev/skills-implement)，它在提交前会运行自己的一次 `/code-review` 检查。

## 前置条件

**规格**轴需要某个地方来找到起源 spec——commit 消息里的 issue 引用、你传入的一个路径、或 `docs/`/`specs/` 下的一份 spec。那套 issue 跟踪器接线来自 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills)；没有 spec 时，规格轴就直接跳过并如实说明。**标准**轴不需要任何设置——即使在一个没有记录任何约定的仓库里，它也总是携带内置的 Fowler 坏味道基线。

## 两个轴，从不合并

定义性的理念就是**两个轴**。**标准**询问 diff 是否符合这个仓库写代码的方式——它的 `CODING_STANDARDS.md` 或 `CONTRIBUTING.md`，外加一个固定的约 12 个 Fowler 代码坏味道基线（神秘命名、重复代码、依恋情结、数据泥团……）。两条规则保证基线的安全：记录的仓库标准总是覆盖它，而且每个坏味道都是一次判断，绝不是硬性违规。**规格**询问正交的问题——代码是否真正做了 issue 或 spec 要求的事，没有遗漏需求或偷偷塞进范围蔓延。

它们作为并行子 agent 运行，这样任何一个都不会污染另一个的上下文，最终报告在独立的 `## Standards` 和 `## Spec` 标题下呈现它们，并带每个轴的摘要。刻意地，各轴之间没有单一赢家。

## 什么时候算工作正常

- 它首先固定并确认固定点（`git rev-parse`），在坏引用或空 diff 上快速失败，而不是在子 agent 内部失败。
- Standards 和 Spec 的发现分成两个不同的块到达，每个都引用它的来源——一个是仓库标准或基线坏味道，另一个是引用的 spec 行。
- 找不到 spec 时，规格轴报告"无可用 spec"，而不是凭空发明需求。

## 所处位置

`code-review` 是主构建链尾部的审查步骤：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它最近的邻居是 [implement](https://aihero.dev/skills-implement)，后者驱动构建并在提交前把这次审查作为自己的一遍；上游，它所核对的 spec 由 [to-spec](https://aihero.dev/skills-to-spec) 和 [to-tickets](https://aihero.dev/skills-to-tickets) 产出。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你导航。
