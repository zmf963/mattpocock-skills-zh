Skills 组织在 `skills/` 下的桶文件夹中：

- `engineering/` — 日常代码工作
- `productivity/` — 日常非代码工作流工具
- `misc/` — 保留但很少使用，不推广
- `personal/` — 与我的个人设置绑定，不推广
- `in-progress/` — 尚未准备好发布的草稿
- `deprecated/` — 不再使用

`engineering/` 或 `productivity/`（**推广的**桶）中的每个 skill 必须在顶层 `README.md` 中有引用，并在 `.claude-plugin/plugin.json` 中有条目。`misc/`、`personal/`、`in-progress/` 和 `deprecated/` 中的 skills 不得出现在两者中。

顶层 `README.md` 中的每个 skill 条目必须将 skill 名称链接到其 `SKILL.md`。

每个桶文件夹都有一个 `README.md`，列出桶中的每个 skill 并附带一行描述，skill 名称链接到其 `SKILL.md`。推广桶的 `README.md` 和顶层 `README.md` 将条目分组为**用户调用**和**模型调用**；非推广桶的 `README.md`（`misc/`、`personal/`）使用平铺列表。

`engineering/` 和 `productivity/` 中的 skills 还在 `docs/<bucket>/<skill-name>.md` 处有一个面向用户的文档页面（文档树镜像 `skills/` 下的那两个桶文件夹）。无论桶是什么，发布的 URL 都是 `https://aihero.dev/skills-<skill-name>`——文档路径仅用于仓库组织。当你添加、重命名或更改 `engineering/` 或 `productivity/` 中 skill 的行为时，按照 [.agents/writing-docs.md](./.agents/writing-docs.md) 创建或重新同步其文档页面。非推广桶（`misc/`、`personal/`、`in-progress/`、`deprecated/`）中的 skills **不**获取文档页面。

每个 `SKILL.md` 要么是用户调用的（`disable-model-invocation: true`，只能由人类访问），要么是模型调用的（模型或用户可访问）。参见 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是映射每个用户可访问 skill 及其关系的路由器。重新同步文档页面的相同触发器也适用于它：每当你添加、重命名、删除或更改用户可访问 skill 如何适配流程时，重新阅读 `ask-matt` 的 `SKILL.md` 并更新它，以便映射保持准确——一个它从未提及的新 skill，或一个它仍然路由到的过时 skill，都是撒谎的路由器。

要（重新）将每个 skill 链接到本地 harness skill 目录（`~/.claude/skills`、`~/.agents/skills`），运行 `scripts/link-skills.sh`。每个条目都是指向此仓库的符号链接，因此 `git pull` 可以保持已安装的 skills 最新；在添加、删除或重命名 skill 后重新运行该脚本。
