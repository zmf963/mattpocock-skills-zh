快速开始：

```bash
npx skills add mattpocock/skills --skill=wayfinder
```

```bash
npx skills update wayfinder
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder)

## 它做什么

`wayfinder` 处理一次 agent 会话装不下的任务——笼罩在迷雾中，从当前位置到目标的路径尚不可见——将其绘制为 issue 跟踪器上的一张**决策票据**的**共享地图**，然后逐一解决它们直到路径清晰。它**规划，不执行**：每张票据解决一个决策——一个待确定的问题，而非待执行的构建切片——当地图完成时，在有人去实际构建之前没有剩余决策要做，所以它产出的是决策，不是交付物。

## 何时使用

你通过输入 `/wayfinder` 来调用它——agent 不会自己触发它。

当一项任务的规模**超出一个 agent 会话能容纳的范围**，且通往其**目的地**的路线仍然模糊时使用——你能感觉到工作的形状，但还无法将其写成 spec 或计划。对于将*已经清晰*的线索转化为 spec，使用 [to-spec](https://aihero.dev/skills-to-spec)；对于将已理解的计划切分为可构建的票据，使用 [to-tickets](https://aihero.dev/skills-to-tickets)。Wayfinder 位于这两者的上游：当迷雾太多无法直接写 spec 时运行它。

## 前置条件

地图及其票据存在于仓库的 issue 跟踪器上，所以 wayfinder 需要 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 铺设的跟踪器接线——它播种了一个"Wayfinding 操作"部分，描述地图、子票据、阻塞和前沿查询在 GitHub、GitLab 或本地 markdown 中如何表达。缺少该文档时，wayfinder 默认使用本地 markdown 地图。

## 地图是索引，迷雾是前沿

**地图**是一个 `wayfinder:map` issue，其票据是它的子 issue——整个团队可以关注的一个共享 URL。它是一个**索引，不是存储**：每个决策只存在于一个位置（其票据），地图只做摘要和链接，从不复述。会话加载地图的低分辨率视图，并按需放大到各个票据。

活跃票据之外是**战争迷雾**——你能感觉到即将到来但还无法确定的决策。判断某物是票据还是迷雾的测试标准是你现在能否*精确陈述问题*，而不是能否回答它。解决一张票据会清除它前方的迷雾，将现在可细化的任何内容**升级**为新的票据。**前沿**是未关闭、未阻塞、未认领的票据——已知区域的边缘——跟踪器的原生阻塞关系将其可视化地呈现，让你无需打开地图就能看到哪些可以接。迷雾只朝**目的地**方向聚集；超出目的地的工作被划为**范围外**，关闭，永不升级。

每张票据是 **HITL**（人类在环——grilling、prototype）或 **AFK**（agent 独自——research）；HITL 票据只有通过实时交流才能解决，所以 agent 从不回答自己的问题。Research 保持为一张真正的票据——下游决策依赖的一个共享阻塞者——但因为它属于 AFK，会话不会停下来阅读：它启动一个 `/research` **子 agent** 并行烧掉这张票据，保持前沿快速推进，并将发现捕获在一次性 `research/<名称>` 分支上。

## 它有效的标志

- 命名**目的地**是第一步——在任何票据存在之前——因为它确定了所有票据都被衡量的范围。
- 一张地图是一个 `wayfinder:map` issue；票据是其子 issue，按**名称**引用，永远不是裸的 `#42`。
- 一次会话**最多解决一张**票据（research 票据例外），将答案记录为一条结论评论，关闭票据，并在"截至目前决策"中追加一行指针。
- 如果开场 grilling 浮现**没有迷雾**，它停下来告诉你旅程小到可以跳过地图。

## 它在哪里嵌入

`wayfinder` 是一个大想法的**入口匝道**：一个太大太模糊无法一次写成 spec 的任务生成一张清理过的决策地图，然后汇入主构建流程。当迷雾被推进、路径清晰时，移交给 [to-spec](https://aihero.dev/skills-to-spec) 来安排多会话构建（或者，如果任务原来很小，直接实施）。它依赖 [grilling](https://aihero.dev/skills-grilling) 和 [domain-modeling](https://aihero.dev/skills-domain-modeling) 来解决各个票据，依赖 [prototype](https://aihero.dev/skills-prototype) 和 [research](https://aihero.dev/skills-research) 来处理需要它们的票据类型。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你导航。
