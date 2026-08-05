快速开始：

```bash
npx skills add mattpocock/skills --skill=resolving-merge-conflicts
```

```bash
npx skills update resolving-merge-conflicts
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/resolving-merge-conflicts)

## 作用

`resolving-merge-conflicts` 逐块处理一个进行中的 git merge 或 rebase 冲突，然后完成操作——已解决、已检查、已提交。

它按**意图**而非按文本来解决。在触碰一个 hunk 之前，它把每一边追溯到它的**一手来源**——commit 消息、PR、起源 issue——以理解这项变更是为什么做的，然后在两边兼容时保留双方的意图。它从不发明新行为来掩盖冲突，也从不伸手去拿 `--abort`：merge 总是会被完成。

## 何时使用

输入 `/resolving-merge-conflicts`，或者当任务匹配时 agent 会自动调用它。

当你在 merge 或 rebase 中途，git 停在它自己无法解决的冲突上时使用。它针对的是你眼前的冲突——不是用来计划 merge，也不是用来调试事后坏掉的行为。如果 merge 已完成，但某事现在因你看不见的原因而失败，改用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)。

## 按意图解决

冲突里的陷阱是把它当作一个文本问题——选"ours"或"theirs"让标记消失。这个 skill 把它当作一个**意图**问题。一个 hunk 的每一边之所以存在，是因为有人想要某样东西；解决方案必须在能兼顾的地方尊重两种想要，在它们真正不兼容的地方，选择符合 merge 声明的目标的那一边，并把权衡公开说出来。

这就是为什么一手来源很重要。你无法保留一个你还没读过的意图，所以工作从历史开始——commits、PRs、tickets——而不是从 diff 开始。

## 什么时候算工作正常

- 每个已解决的 hunk 都保留两边的行为，或在无法保留时说出权衡。
- 没有出现两边分支上都不存在的新行为。
- 项目自己的检查——类型检查、测试、格式化——在提交前被找到并跑绿。
- merge 或 rebase 被一直带到完成的提交，绝不中止。

## 所处位置

一个随时可以调用的独立技能：你在 merge 或 rebase 停滞的那一刻调用它，它会交回一棵干净、已提交的树。它自然的邻居是 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)，因为一个干净解决但事后表现异常的 merge 是诊断问题，不是冲突问题。当你不确定哪个 skill 适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你导航。
