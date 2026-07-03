---
name: handoff
description: 将当前对话压缩为交接文档，供另一个 agent 接手。
argument-hint: "下一个会话将用于什么？"
disable-model-invocation: true
---

编写一份交接文档，总结当前对话，以便新 agent 可以继续工作。保存到用户操作系统的临时目录 —— 不是当前工作区。

在文档中包含"建议的技能"部分，建议 agent 应调用的技能。

不要重复已经捕获在其他产物（PRD、计划、ADR、issue、commit、diff）中的内容。改为通过路径或 URL 引用它们。

编辑任何敏感信息，如 API 密钥、密码或个人身份信息。

如果用户传递了参数，将它们视为下一个会话将关注什么的描述，并相应地定制文档。
