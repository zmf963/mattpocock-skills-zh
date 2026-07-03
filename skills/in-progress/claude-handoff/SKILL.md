---
name: claude-handoff
description: 将当前对话移交给一个立即接手工作的新后台 agent。
argument-hint: "下一个会话将用于什么？"
disable-model-invocation: true
---

编写当前对话的交接摘要，以便新 agent 可以继续工作。不是保存它，而是启动一个后台 agent，以摘要作为其提示：`claude --bg --name "<descriptive name>" "<handoff summary>"`。它在当前工作目录中启动并立即返回；用户通过 `claude agents` 管理它。

始终传递 `-n`/`--name` 并带有描述性名称（例如 `--name "Fix login bug"`）—— 它设置显示在作业列表、会话选择器和终端标题中的显示名称。

在摘要中包含"建议的技能"部分，建议 agent 应调用的技能。

不要重复已经捕获在其他产物（PRD、计划、ADR、issue、commit、diff）中的内容。改为通过路径或 URL 引用它们。

编辑任何敏感信息，如 API 密钥、密码或个人身份信息 —— 摘要成为 agent 的提示。

如果用户传递了参数，将它们视为下一个会话将关注什么的描述，并相应地定制摘要。
