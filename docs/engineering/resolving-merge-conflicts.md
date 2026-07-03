快速开始：

```bash
npx skills add mattpocock/skills --skill=resolving-merge-conflicts
```

```bash
npx skills update resolving-merge-conflicts
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/resolving-merge-conflicts)

## 它做什么

`resolving-merge-conflicts` 逐块处理进行中的 git merge 或 rebase 冲突，并完成操作——已解决、已检查、已提交。

它通过**意图**解决，而非文本。在接触一个块之前，它将每一方追溯到其**主要来源**——commit 消息、PR、原始 issue——以理解为什么要做这个变更，然后在它们兼容的地方保留双方的意图。它从不发明新行为来掩盖冲突，也从不使用 `--abort`：merge 总是被完成。

## 何时使用它

输入 `/resolving-merge-conflicts`，或者 agent 在任务匹配时自动调用它。

当你处于 merge 或 rebase 中间，而 git 停在了它无法自行解决的冲突上时使用它。它是为了你面前的冲突——不是为了计划 merge 或调试之后出问题的行为。如果 merge 已完成但某物现在以你看不到的原因失败了，改用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)。

## 通过意图解决

冲突中的陷阱是将其视为文本问题——选择 "ours" 或 "theirs" 来让标记消失。此 skill 将其视为**意图**问题。一个块的每一方存在是因为某人想要某物；解决方案必须在可以的地方尊重双方的意图，而在它们真正不兼容的地方，选择匹配 merge 声明目标的那一个并公开说明权衡。

这就是为什么主要来源很重要。你无法保留你没有阅读过的意图，所以工作从历史开始——commits、PR、工单——而不是 diff。

## 它在正常工作的标志

- 每个已解决的块保留双方的行为，或在无法保留时指明权衡。
- 没有出现不属于任一分支的新行为。
- 项目自己的检查——typecheck、tests、format——被找到并在提交前运行通过。
- merge 或 rebase 被一路带到完成的 commit，永不中止。

## 它在哪里

一个随时可用的独立 skill：你在 merge 或 rebase 停滞时调用它，它将一个干净、已提交的树交还给你。它的天然邻居是 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)，因为一个解决干净但之后行为异常的 merge 是诊断问题，而非冲突问题。当你不确定哪个 skill 适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
