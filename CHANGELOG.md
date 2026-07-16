# mattpocock-skills

## 1.1.0

### Minor Changes

- [#406](https://github.com/mattpocock/skills/pull/406) — 更新 **`ask-matt`** 路由器映射完整 skill 集，新增 5 个缺失 skills 的路由。
- [#464](https://github.com/mattpocock/skills/pull/464) — 推广并加固 **`code-review`**，从 `in-progress/` 移至 `engineering/`，新增 Fowler 代码坏味道基线。
- [#464](https://github.com/mattpocock/skills/pull/464) — 改进 **`grilling`**：新增确认门槛（达成共识前不执行计划），区分*事实*（探索代码库查找）与*决策*（向人类提问）。
- [#463](https://github.com/mattpocock/skills/pull/463) — **`writing-great-skills`** 新增两个 Steering 失败模式：**Negation**（否定语义会引导 agent 走向被禁止的行为）和 **Negative Space**（遗漏的决策被委托给 agent 的先验知识）。
- [`850873c`](https://github.com/mattpocock/skills/commit/850873cd) — 将 **`prototype`** 改为模型调用 skill。
- [#409](https://github.com/mattpocock/skills/pull/409) — 新增 **`research`** skill，作为后台 agent 针对一手来源调查问题。
- [#469](https://github.com/mattpocock/skills/pull/469) — **`to-issues`** 增加宽重构支持（展开—收缩策略），重构流程文档结构。
- [#464](https://github.com/mattpocock/skills/pull/464) — 统一规划 skills：**`to-prd` 重命名为 `to-spec`**，**`to-plan` 和 `to-issues` 合并为 `to-tickets`**。`to-tickets` 产出带阻塞边的曳光弹票据，支持本地文件和真正跟踪器两种发布模式。
- [#464](https://github.com/mattpocock/skills/pull/464) — **`wayfinder`** 从 `in-progress/` 毕业进入 `engineering/`：`decision-mapping` 重命名为 `wayfinder`，以"目的地"为主导词，默认"规划不执行"，地图是索引而非存储，新增第四种 `task` 票据类型和 HITL/AFK 分类。

### Patch Changes

- [#464](https://github.com/mattpocock/skills/pull/464) — 重构 **`tdd`** 为纯参考 skill，新增同义反复测试反模式。
- [`e00eadb`](https://github.com/mattpocock/skills/commit/e00eadb) — 扩展 **`triage`** 以支持外部 PR 的 triage。
- [#472](https://github.com/mattpocock/skills/pull/472) — 修复 **`wayfinder`** 硬编码 issue 跟踪器文档路径的问题。

## 1.0.1

### Patch Changes

- [`d20ee26`](https://github.com/mattpocock/skills/commit/d20ee2684e2a9442698ac3c1e0f2c5b68c4cf296) Thanks [@mattpocock](https://github.com/mattpocock)! - Make the **`teach`** skill reuse-first. Lessons are now built from reusable **components** in `./assets/` — stylesheets, quiz widgets, simulators, diagram helpers. Reuse is the default: the agent reads `./assets/` before authoring a lesson, builds from what's there, and extracts anything new and reusable into a component rather than inlining it.

## 1.0.0

### Major Changes

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Add the **`ask-matt`** skill — a user-invoked router that points you at the right skill or flow for your situation.

  **Breaking:** `ask-matt` routes over the other user-invoked skills in this repo, so it expects them to be installed.

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Add the shared design skills and rewire existing skills onto them.

  - New **`codebase-design`** skill — the deep-module vocabulary (module, interface, depth, seam, adapter) and the principles for putting a lot of behaviour behind a small interface. The language that previously lived in `improve-codebase-architecture/LANGUAGE.md` now lives here, generalized for reuse across skills.
  - New **`domain-modeling`** skill — actively build and sharpen a project's domain model, stress-testing terms against the glossary and keeping `CONTEXT.md` and ADRs current.
  - `improve-codebase-architecture` now draws its architecture vocabulary from `/codebase-design` and its domain model from `/domain-modeling`.
  - `tdd` now leans on `/codebase-design` for interface-design guidance — its inline `deep-modules.md` / `interface-design.md` notes were removed in favour of the shared skill.
  - `grill-with-docs` now builds the domain model inline via `/domain-modeling`.

  **Breaking:** these skills now depend on the new `codebase-design` / `domain-modeling` skills, so you must install them too.

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Remove the **`caveman`** and **`zoom-out`** skills.

  - `caveman` was a duplicate of another skill I was testing and was never meant to be public.
  - `zoom-out` went unused in practice, so it's been removed from the repo.

  **Breaking:** both skills have been removed.

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Rename the **`diagnose`** skill to **`diagnosing-bugs`**.

  **Breaking:** invoke it as `/diagnosing-bugs` — the old `/diagnose` name no longer exists.

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Replace **`write-a-skill`** with **`writing-great-skills`**.

  - Removed `write-a-skill`.
  - Added `writing-great-skills` (plus its `GLOSSARY.md`) — a reference for writing and editing skills well: the vocabulary and principles that make a skill predictable, hunting no-ops down to the sentence level.
  - Exposed `grilling` as a model-invoked skill — the reusable interview loop behind `grill-me` and `grill-with-docs`.

  **Breaking:** `write-a-skill` has been removed; use `writing-great-skills` instead.

### Minor Changes

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Add the **`resolving-merge-conflicts`** skill — a loop for resolving an in-progress git merge or rebase conflict. Standalone, with no dependencies on other skills.

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Rename the skill taxonomy from **Commands / Skills** to **User-invoked / Model-invoked** across the docs, and add `docs/invocation.md` defining the split: user-invoked skills are reachable only when you type them and exist to orchestrate; model-invoked skills can also be reached automatically when the task fits. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one.

### Patch Changes

- [`47bde84`](https://github.com/mattpocock/skills/commit/47bde84da032afb2e5058f997f3bbca47d321dbd) Thanks [@mattpocock](https://github.com/mattpocock)! - Tighten the **`review`** skill: fail-fast ref check, single-sourced rules, and no-op cuts.
