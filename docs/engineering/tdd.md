快速开始：

```bash
npx skills add mattpocock/skills --skill=tdd
```

```bash
npx skills update tdd
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd)

## 它做什么

`tdd` 先测试构建功能或修复 bug，一次一个行为，通过红-绿循环驱动代码。

它**不会**先写所有测试。批量先写测试（"水平切片"）产生的是*想象中*行为的测试——它们检查事物的形状，对真正的变化变得麻木。`tdd` 反而采用垂直切片：一个测试，然后刚好够通过它的代码，然后是下一个测试，每个循环由上一个教会你的东西来指导。测试仅针对公共接口，因此下面的实现可以在测试不动的情况下变化。

## 何时使用它

输入 `/tdd`，或者 agent 在任务匹配时自动调用它——先测试构建功能或修复 bug，或者当你说 "red-green-refactor" 时。

当有一个具体的行为要构建，并且你想要能在重构中存活的测试时使用它。如果行为尚未确定，先确定 spec——为此，使用 [to-prd](https://aihero.dev/skills-to-prd)。当工作真正关乎接口的形状而非测试时，使用 [codebase-design](https://aihero.dev/skills-codebase-design)；`tdd` 在规划期间调用它获取深层模块词汇。

## 红-绿，一次一个切片

主导理念是**红-绿循环**：写一个失败的测试（红），添加刚好够通过它的代码（绿），然后为下一个行为重复——每个循环由上一个教会你的东西来指导。第一个循环是**示踪子弹**：一个证明单一路径端到端工作的测试，在你从它向外构建之前。因为你刚写了代码，你确切知道哪个行为重要以及如何验证它——你永远不会因为承诺你还不理解的测试结构而超出视野。

两条规则保持测试诚实。一个好的测试读起来像规格说明（"用户可以用有效购物车结账"），并通过公共 API 执行真实代码路径，因此重命名内部函数永远不会破坏它。预期值来自独立的真相来源——已知良好的字面量、一个计算好的示例、spec——从不用代码计算它的方式来重新计算，这是**同义反复**测试通过构造通过却什么都没告诉你的原因。

重构仅在套件为绿色时进行；绝不在红色时。

## 它在正常工作的标志

- 它写一个测试，让它通过，然后才写下一个——而不是一批测试后跟着一批代码。
- 测试命名行为，而非内部细节，并且能在内部重命名后存活。
- 预期值是来自 spec 的字面量，而不是用代码推导的方式推导出的数字。

## 它在哪里

`tdd` 是主构建链运行以编写代码的红-绿循环：

```txt
grill-with-docs → to-prd → to-issues → implement → code-review
```

[implement](https://aihero.dev/skills-implement) 是链条的构建步骤，它在内部驱动 `tdd` 以先测试方式构建每个工单，然后交给 [code-review](https://aihero.dev/skills-code-review)——所以 `tdd` 是该步骤内部的引擎，而非自己的步骤。你也可以直接使用它，每当有一个具体的行为要构建而不需要完整的 spec 时。它的另一个邻居是 [codebase-design](https://aihero.dev/skills-codebase-design)，它在规划期间依赖它来找到值得测试的深层模块接缝。当你不确定哪个 skill 或流程适合时，[ask-matt](https://aihero.dev/skills-ask-matt) 为你路由。
