Skills 按 bucket（桶）文件夹组织在 `skills/` 之下：

- `engineering/` —— 日常的写代码工作
- `productivity/` —— 日常的非代码流程工具
- `misc/` —— 保留着但很少用，不推广
- `personal/` —— 绑定我自己的环境，不推广
- `in-progress/` —— 尚未准备发布的草稿
- `deprecated/` —— 不再使用

`engineering/` 或 `productivity/`（**推广**桶）中的每个 skill 都必须在顶层 `README.md` 中有一条引用，并在 `.claude-plugin/plugin.json` 的 `skills` 数组中有一个条目（Claude Code 插件只发布推广集）。位于 `misc/`、`personal/`、`in-progress/`、`deprecated/` 中的 skills 不得出现在二者任何一处。

仓库本身也是自己的单插件 Claude Code 市场：`.claude-plugin/marketplace.json` 列出了唯一的 `mattpocock-skills` 插件。当 bump 发布版本时，保持 `.claude-plugin/plugin.json` 的 `version` 与 `package.json` 的 `version` 同步——Claude 使用插件 `version` 来决定已安装用户何时看到更新。修改任一 manifest 后运行 `claude plugin validate . --strict`。为什么有 Claude 插件但（尚未）有 Codex 插件，记录在 [.agents/adr/0002-ship-as-a-claude-code-plugin.md](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

顶层 `README.md` 中每条 skill 条目都必须把 skill 名称链接到它的 `SKILL.md`。

每个 bucket 文件夹都有一个 `README.md`，用一行描述列出该 bucket 中的每个 skill，skill 名称链接到其 `SKILL.md`。推广桶的 `README.md` 与顶层 `README.md` 会把条目分组为 **用户调用（User-invoked）** 和 **模型调用（Model-invoked）**；非推广 bucket 的 `README.md`（`misc/`、`personal/`）使用扁平列表。

`engineering/` 和 `productivity/` 中的 skills 在 `docs/<bucket>/<skill-name>.md` 还有一份面向人类的文档页（docs 树镜像 `skills/` 下这两个 bucket 文件夹）。无论属于哪个 bucket，发布后的 URL 都是 `https://aihero.dev/skills-<skill-name>` —— docs 路径只是仓库的组织方式。当你在 `engineering/` 或 `productivity/` 中新增、重命名或改变某个 skill 的行为时，要按照 [.agents/writing-docs.md](./.agents/writing-docs.md) 创建或重新同步它的文档页。非推广 bucket（`misc/`、`personal/`、`in-progress/`、`deprecated/`）中的 skills **不**生成文档页。

每个 `SKILL.md` 要么是用户调用的（`disable-model-invocation: true` 加上 `agents/openai.yaml` 中的 `policy.allow_implicit_invocation: false`，只有人类可达），要么是模型调用的（模型或用户均可达）。见 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是路由器，映射每个用户可达的 skill 以及它们之间的关系。重新同步文档页时适用的同一触发条件也适用于它：每当你新增、重命名、移除或改变某个用户可达 skill 如何融入流程时，重新读取 `ask-matt` 的 `SKILL.md` 并更新它，使这张地图保持准确——一个它从未提及的新 skill，或一个它仍在路由到的过时 skill，都是会说谎的路由器。

要把每个 skill（重新）链接进本地 harness 的 skill 目录（`~/.claude/skills`、`~/.agents/skills`），运行 `scripts/link-skills.sh`。每个条目都是指向本仓库的符号链接，因此 `git pull` 就能让已安装的 skills 保持最新；在新增、移除或重命名 skill 后重新运行该脚本。
