Quickstart:

```bash
npx skills add mattpocock/skills --skill=grill-with-docs
```

```bash
npx skills update grill-with-docs
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs)

## 作用

`grill-with-docs` 会不断地就某个计划或设计向你提问，一次一个问题，直到你和代理达成共同理解——并且它会边走边记录词汇和决策。

盘问**留下可追溯的记录**。单纯的访谈能帮你理清思路，但随着会话结束就消失了；这个工具会在每个术语一旦明确时就将其捕获到 `CONTEXT.md` 词汇表中，并将困难、单向的决策记录为 ADR。对齐结果在对话结束后依然存在，而不仅仅存在你的脑海中。

## 何时使用

你需要通过输入 `/grill-with-docs` 来调用它——代理不会自行触发。

在变更的最初阶段、计划仍然模糊、领域语言尚未确定时使用它，并且你希望在编写任何代码之前对两者都进行压力测试。如果你只想要访谈而不需要产物，请使用 [grilling](https://aihero.dev/skills-grilling)；如果计划已经很清晰，你只需要确定或记录术语，请使用 [domain-modeling](https://aihero.dev/skills-domain-modeling)。

## 前置条件

此技能是有状态的——它在盘问过程中写入你的仓库。已解决的术语会写入根目录下的 `CONTEXT.md` 词汇表（如果 `CONTEXT-MAP.md` 标记了多上下文仓库，则写入对应上下文的 `CONTEXT.md`），真正难以逆转的决策会作为 ADR 记录在 `docs/adr/` 下。两者都是惰性创建的——在第一个术语或决策明确之前什么都不存在——所以你不需要预先搭建任何东西，但你需要处于一个可以安全写入这些文件的位置。

## 盘问过程

引擎是一个**盘问**：一次一个问题，沿着设计树逐步向下，在继续之前解决决策之间的依赖关系，每个问题都附带推荐答案。代码库能够回答的问题通过阅读代码库来回答，而不是通过问你。

使这个变体成为独立技能的原因在于答案的去向。随着盘问的进行，模糊的语言会被精炼为规范术语并立即写入词汇表——而非在最后批量处理。词汇表始终是词汇表：纯粹的词汇，没有实现细节，没有规格。ADR 被谨慎提供，仅当决策难以撤销、在没有上下文的情况下令人惊讶、且是真正权衡的结果时。大多数会话产生的是更精确的词汇表和很少或没有 ADR，这正是预期的形态。

## 验证标准

- 它一次只问一个问题并等待回答，而不是一次性抛出问卷。
- 术语一旦明确就被写入 `CONTEXT.md`，使用项目自己的语言。
- 它尽可能深入代码库来回答自己的问题。
- ADR 保持稀少——你不会被要求为可逆的选择盖章。

## 所处位置

`grill-with-docs` 是主构建链的开端步骤：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

它在任何东西被写成规格之前出现：它产生共同理解和确定的词汇表，然后 [to-prd](https://aihero.dev/skills-to-prd) 在这些基础上合成 PRD 而无需重新访谈你。它的近邻是 [grilling](https://aihero.dev/skills-grilling)（同样的访谈但不产生文档）和 [domain-modeling](https://aihero.dev/skills-domain-modeling)（它所驱动的词汇表和 ADR 实践）。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
