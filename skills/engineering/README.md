# 工程

我每天用于代码工作的 Skills。

## 用户调用

只能在你输入时访问（`disable-model-invocation: true`）。

- **[ask-matt](./ask-matt/SKILL.md)** — 询问哪个 skill 或流程适合你的情况。是此仓库中用户调用 skills 的路由器。
- **[grill-with-docs](./grill-with-docs/SKILL.md)** — 深入追问，同时构建你项目的领域模型，精炼术语并内联更新 `CONTEXT.md` 和 ADR。
- **[triage](./triage/SKILL.md)** — 将 issues 移过一个分类角色状态机。
- **[improve-codebase-architecture](./improve-codebase-architecture/SKILL.md)** — 扫描代码库寻找深化机会，以可视化 HTML 报告呈现，然后对你选择的那一个进行深入追问。
- **[setup-matt-pocock-skills](./setup-matt-pocock-skills/SKILL.md)** — 为此仓库配置工程 skills（问题跟踪器、分类标签、领域文档布局）。每个仓库运行一次。
- **[to-issues](./to-issues/SKILL.md)** — 将任何计划、spec 或 PRD 分解为使用垂直切片可独立领取的 issues。
- **[to-prd](./to-prd/SKILL.md)** — 将当前对话转换为 PRD 并发布到问题跟踪器。

## 模型调用

模型或用户可访问（丰富的触发措辞让模型可以找到它们）。

- **[prototype](./prototype/SKILL.md)** — 构建一个一次性原型来回答设计问题：一个可运行的终端应用用于状态/逻辑，或几个可切换的 UI 变体。

- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)** — 针对困难 bug 和性能回归的有纪律的诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./research/SKILL.md)** — 针对高信任度的主要来源调查问题，并将发现捕获为仓库中的带引用 Markdown 文件，作为后台 agent 运行。
- **[tdd](./tdd/SKILL.md)** — 带有红-绿-重构循环的测试驱动开发。一次一个垂直切片地构建功能或修复 bug。
- **[domain-modeling](./domain-modeling/SKILL.md)** — 积极构建和精炼项目的领域模型——挑战术语，用场景进行压力测试，内联更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./codebase-design/SKILL.md)** — 设计深层模块的共享规则和词汇：小型接口、干净接缝、可通过接口测试。
- **[code-review](./code-review/SKILL.md)** — 从固定点开始的 diff 双轴审查：**标准**（是否遵循仓库的编码标准，加上 Fowler 坏味道基线？）和**规格**（是否忠实实现了原始 issue/PRD？），作为并行子 agent 运行。
