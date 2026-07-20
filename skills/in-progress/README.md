# 开发中

仍在开发中的 Skills。尚未准备发布——预期会有粗糙的边缘、破坏性变更和被放弃的实验。它们在毕业进入稳定桶之前被排除在插件和顶层 README 之外。

- **[batch-grill-me](./batch-grill-me/SKILL.md)** —— 以轮次而非单问推进设计树的不懈访谈——每轮一次性提问所有前置条件已经确定的前沿决策，再根据你的回答重新计算。用户调用。
- **[loop-me](./loop-me/SKILL.md)** —— 在多个会话中向自己追问出可实施的工作流 spec，使用当前目录作为有状态的工作区。用户调用。
- **[wizard](./wizard/SKILL.md)** —— 生成一个交互式 bash 向导，引导人类完成一个手动流程（设置、一次性迁移、状态转换）——打开 URL、捕获值、写入 `.env` 和 GitHub Actions secrets。用户调用。
- **[writing-beats](./writing-beats/SKILL.md)** —— 将一篇文章塑造为一段节拍之旅，自选冒险风格。选择一个起始节拍，只写那个节拍，然后转向下一个，直到文章达到自然的结局。
- **[writing-fragments](./writing-fragments/SKILL.md)** —— Grilling 会话，挖掘你的片段——异质的写作碎片——并将它们追加到单个文档中作为未来文章的原材料。
- **[writing-shape](./writing-shape/SKILL.md)** —— 取一个原始材料的 markdown 文件，逐段将其塑造成一篇文章，在每个步骤论证格式选择。
- **[claude-handoff](./claude-handoff/SKILL.md)** —— 将当前对话交接给一个新的后台 agent，该 agent 立即接手工作，通过 `claude --bg` 以交接摘要作为种子。用户调用。
- **[setup-ts-deep-modules](./setup-ts-deep-modules/SKILL.md)** —— 将 dependency-cruiser 接入一个 TypeScript 仓库，使每个包成为一个深模块——实现隐藏在子文件夹中，只能通过入口点文件访问，测试通过这些入口点进行。用户调用。
- **[to-questionnaire](./to-questionnaire/SKILL.md)** —— 将你无法完全回答的决策转化为一份 Markdown 问卷，让其他人异步填写，或在会议中填写。它向你追问发送过程（发给谁、你需要拿回什么），而非主题本身。用户调用。
