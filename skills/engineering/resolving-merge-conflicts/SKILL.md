---
name: resolving-merge-conflicts
description: "当你需要解决进行中的 git merge/rebase 冲突时使用。"
---

1. **查看当前状态**的 merge/rebase。检查 git 历史，以及冲突文件。

2. **为每个冲突找到一手来源**。深入理解每个变更是为什么做出的，以及原始意图是什么。阅读 commit 消息，检查 PR，检查原始 issue/ticket。

3. **解决每个 hunk。** 在可能的地方保留两个意图。在不兼容的地方，选择匹配合并的陈述目标的那个并注明权衡。**不要**发明新行为。始终解决；永远不要 `--abort`。

4. 发现项目的**自动化检查**并运行它们 —— 通常是类型检查，然后测试，然后格式化。修复合并破坏的任何东西。

5. **完成 merge/rebase。** 暂存一切并提交。如果正在 rebase，继续 rebase 过程直到所有 commit 都被 rebase。
