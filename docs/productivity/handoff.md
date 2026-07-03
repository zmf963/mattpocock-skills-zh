快速开始：

```bash
npx skills add mattpocock/skills --skill=handoff
```

```bash
npx skills update handoff
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff)

## 它做什么

`handoff` 将当前对话压缩为**交接文档**——一个新 agent 可以阅读以从你停下的地方继续工作的单一文档。

它**不**重述已经存在于其他地方的内容。任何已被捕获在 PRD、计划、ADR、issue、commit 或 diff 中的内容通过路径或 URL 引用，从不复制。文档只携带活跃的线索——你在做什么、为什么、以及下一步是什么——并保存到你操作系统的临时目录，而不是工作区，因此它永远不会变成另一个需要维护的产物。

## 何时使用它

你通过输入 `/handoff` 来调用它——agent 不会自行调用它。传递一个关于下一个会话是做什么的说明，文档会为其量身定制。

当一个对话已经进行了足够长的时间，其上下文面临风险时使用它——你接近上下文限制、为当天收尾、或刻意将工作交给另一个 agent——并且你想要在不拖着整个转录的情况下保留线索。

## 文档包含什么

- **活跃线索**——什么是进行中的以及为什么，用对话自己的术语，减去已经在其他地方写下来的任何东西。
- **建议的 skills**——指向下一个 agent 应该使用哪些 skills 来继续的指针。
- **引用，而非副本**——指向保存已确定细节的 PRD、计划、ADR、issues 和 diff 的链接和路径。
- **已脱敏的密钥**——API 密钥、密码和 PII 在文档写入前被剥离。

要抓住的理念是**压缩**：交接是对话被挤压到仅剩其可恢复的核心，因此新 agent 继承的是动力，而非噪音。

## 它在哪里

`handoff` 是一个随时可用的独立 skill——它位于两个会话之间的接缝处，而非构建链内部。它天然地与它指向其输出的产物类 skills 配对：[to-prd](https://aihero.dev/skills-to-prd)，因为一个完成的 PRD 正是交接引用而非重复的那种已确定细节。当你不确定哪个 skill 适合当下时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
