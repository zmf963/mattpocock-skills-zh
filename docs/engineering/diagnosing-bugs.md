Quickstart:

```bash
npx skills add mattpocock/skills --skill=diagnosing-bugs
```

```bash
npx skills update diagnosing-bugs
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs)

## 作用

`diagnosing-bugs` 针对棘手的 bug 和性能回归问题运行一套严谨的诊断循环——构建重现步骤、最小化它、对假设排序、添加检测手段，然后修复并附带回归测试。

它拒绝在你拥有**紧凑反馈循环**之前提出假设——即一个可运行的命令，已经能在*这个* bug 上显示红色。在拥有该命令之前阅读代码来构建理论，正是此技能要防止的错误。没有可触发红色的循环，就没有诊断。

## 何时使用

输入 `/diagnosing-bugs`，或者当任务适当时代理会自动调用它——在你说"诊断"/"调试"或报告某物损坏、抛出异常、失败或缓慢时会触发。

在棘手的 bug 上使用它：一眼看不出原因的 bug、间歇性闪退、在两个已知良好状态之间悄悄溜进来的回归问题。如果是快速验证设计问题而非追踪缺陷，请使用 [prototype](https://aihero.dev/skills-prototype)。

## 紧凑循环就是技能本身

一旦你有了信号，其他所有事情——二分查找、假设检验、添加检测——都是机械性的。因此，该技能将不成比例的努力投入到第一阶段：构建一个通过/失败的命令，该命令驱动实际的 bug 代码路径并断言用户的确切症状，然后**收紧**它，直到它快速、确定且可由代理运行。一个 30 秒的不稳定循环几乎不比没有好；一个 2 秒的确定性循环则是调试的超能力。

它为你提供了一系列构建该循环的方法——失败的测试、curl 脚本、CLI diff、无头浏览器、重放跟踪、一次性测试工具、模糊循环、`git bisect run`、差异运行——以及作为最后手段的包含人工参与的 bash 脚本。对于非确定性 bug，目标不是干净的重现步骤，而是**更高的重现率**：循环触发、并行化、增加压力，直到闪退变得可调试。

## 验证标准

- 它在提出理论*之前*就构建并运行重现命令——并粘贴调用命令及其红色输出。
- 循环断言的是你实际报告的症状，而不是附近的某个失败。
- 假设以排序的、可证伪的列表形式呈现，并在进行任何测试之前展示给你。
- 调试检测标记为（`[DEBUG-...]`），在声明完成之前通过 grep 清理干净。

## 所处位置

`diagnosing-bugs` 是一个**随时可调用的独立技能**——一旦出现问题你就切入它，修复和回归测试完成后就退出。当真正的发现是没有好的接缝来锁定 bug——问题在于代码而非 bug 本身时，它会交接给 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。当你不确定哪个技能合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
