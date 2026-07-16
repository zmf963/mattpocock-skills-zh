---
name: setup-ts-deep-modules
description: 将 dependency-cruiser 接入一个 TypeScript 仓库，使每个包成为一个深模块——实现隐藏在子文件夹中，只能通过入口点文件访问。用户调用。
disable-model-invocation: true
---

# Setup TS Deep Modules

让这个仓库中的每个包都成为一个**深模块**：大量行为藏在小小的接口后面。一个包的公开面是它的**入口点**——包根目录下的文件——其子文件夹中的所有内容都是隐藏的。这个 skill 安装 [dependency-cruiser](https://github.com/sverweij/dependency-cruiser) 和那些使入口点成为唯一进入方式的规则，然后证明这些规则有效。

关于词汇（深模块、接口、接缝、深度），运行 `/codebase-design` skill——全程使用它的语言。

## 这个配置强制执行的结构

```
src/packages/
  <名称>/
    index.ts        ← 一个入口点（公开的）。从外部导入这个。
    client.ts       ← 另一个入口点。包可以暴露多个。
    lib/            ← 实现：对外部隐藏，内部可以自由相互导入。
    tests/          ← 就近测试 + fixtures（子文件夹，所以是私有的）。
```

公开面是包的**根文件**——而不是一个指定的 `index.ts`。按惯例实现放在 `lib/` 中，测试放在 `tests/` 中，给每个包相同的双文件夹结构。但规则本身是通用的：子文件夹中的*任何东西*都是私有的，所以你永远不需要扩展配置来添加文件夹。

四条规则，全部 `error`：

1. **入口点边界**——包外部的代码（应用代码或其他包）只能导入该包的入口点（其根文件），永远不能导入其子文件夹中的任何内容。
2. **包内自由**——包的自身文件可以自由相互导入。
3. **通过入口点测试**——`<pkg>/tests/` 下的文件可以导入任何包的入口点及其自身的 `tests/` fixtures，但永远不能导入任何包的子文件夹内部（甚至不能导入自己的）。跨包的集成测试可以；深层导入不行。
4. **无循环**——没有依赖循环。

**入口点，不是 barrel。** 因为公开面是*每一个*根文件，一个包可以暴露多个小入口点（`index.ts`、`client.ts`、`server.ts`），而不是把所有东西都塞进一个巨大的 `index.ts`。不鼓励重新导出整个子树的 barrel 文件——保持入口点小巧，把实现藏在子文件夹中。

分层（哪些包可以依赖哪些）是*另一个*关注点，在配置中留作注释占位供此仓库填充。

## 步骤

### 1. 检测环境

- **包管理器**——`pnpm-lock.yaml` → pnpm，`yarn.lock` → yarn，`bun.lockb` → bun，否则 npm。用它运行下面的每条命令（`pnpm`/`yarn`/`npm run`/`bunx`）。
- **包根目录**——如果 `src/` 存在则使用 `src/packages`，否则 `packages`。如果仓库已有不同的惯例，与用户确认选择。
- **已有配置**——检查是否存在 `.dependency-cruiser.*` 文件。如果存在，不要覆盖它：将四条规则和选项合并进去，并告诉用户你添加了什么。

**完成标准：** 包管理器、包根目录和已有配置状态全部已知。

### 2. 安装 dependency-cruiser

用检测到的包管理器安装 `dependency-cruiser` 为 devDependency。

**完成标准：** `dependency-cruiser` 在 `devDependencies` 中。

### 3. 编写配置

将 [`dependency-cruiser.config.cjs`](./dependency-cruiser.config.cjs) 复制到仓库根目录为 `.dependency-cruiser.cjs`。将 `PACKAGES_ROOT` 设置到步骤 1 中检测到的根目录。规则基于路径深度且与扩展名无关，所以不需要其他调整。

**完成标准：** `.dependency-cruiser.cjs` 存在且包含正确的 `PACKAGES_ROOT`，四条 forbidden 规则存在。

### 4. 接入检查

- 添加 `lint:boundaries` 脚本：`depcruise <包根目录>`（或 `depcruise src`）。
- 将其折叠进仓库的伞形检查命令——那个已经运行类型检查的命令（例如 `check`/`ci`/`validate` 脚本）。不要动 `tsconfig` 或添加路径别名。
- 如果没有伞形脚本，添加 `lint:boundaries` 并告诉用户将其包含在 CI 中。

**完成标准：** `lint:boundaries` 存在并与类型检查作为同一命令的一部分运行。

### 5. 搭建示例包

创建一个已提交的 `<packages-root>/example/` 作为可复制的模板：

- `index.ts`——一个入口点。导出一个委托给内部文件的函数（这样包在视觉上是*深的*，不是一个透传）。
- `lib/impl.ts`——一个**子文件夹**中的内部文件，被 `index.ts` 导入，外部不可达。
- `tests/example.test.ts`——**只**导入 `../index`（一个入口点），并对公开函数做断言。

告诉用户这是一个可复制或删除的起始模板。

**完成标准：** 示例包存在，通过根入口点暴露其行为，并将 `impl` 藏在子文件夹中。

### 6. 证明规则有效

这是整个 skill 的完成标准——一个不会在违规时失败的配置毫无价值。

1. 运行 `lint:boundaries`。必须在干净示例上**通过**。
2. 临时在 `tests/example.test.ts` 中添加一个深层导入（例如 `import { thing } from "../lib/impl"`）。再次运行 `lint:boundaries`——必须**失败**并显示 `tests-through-entrypoints`。
3. 撤销深层导入。再运行一次——必须**通过**。

**完成标准：** 你观察到通过，然后深层导入失败，然后再通过。如果步骤 2 没有失败，规则没有正确接入——在完成前修复。

### 7. 记录惯例

在包文件夹中写一个 `README.md`（`<packages-root>/README.md`）——放在它治理的包旁边——涵盖：`src/packages/<名称>/` 布局（入口点在根目录，`lib/` 放实现，`tests/` 放测试），"只通过包的入口点（其根文件）导入"，以及如何运行 `lint:boundaries`。**明确不鼓励 barrel 文件**——暴露多个小入口点，而不是通过一个 index 重新导出整个子树。保持为可复制片段加上四条规则各一段。

然后在仓库的 agent 指令文件中添加一个**上下文指针**——如果有 `CLAUDE.md` 则指向它，否则指向 `AGENTS.md`（如果两者都不存在则创建 `AGENTS.md`）。一行即可，例如 `包是深模块——在添加或导入一个包之前参见 [src/packages/README.md](./src/packages/README.md)。` 这是让 agent 发现边界规则而不是撞上去的关键。

**完成标准：** `<packages-root>/README.md` 存在且不鼓励 barrel，仓库的 `CLAUDE.md`/`AGENTS.md` 链接到它。
