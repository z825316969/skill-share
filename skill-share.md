# Skill：从 Prompt 模板到 Agent 能力资产

> 这不是一篇“怎么写几个 YAML 字段”的入门小抄，而是一篇面向技术分享的系统性文章。重点不是 Skill 的表面格式，而是它为什么会在 Agent 时代迅速成为一种关键的工程化抽象，以及我们该如何真正把它用起来。

---

## 一、先从提示词工程说起：为什么 Skill 不是凭空出现的

要真正理解 Skill，最好不要一上来就看目录结构，而是先把它放回 AI 应用演化的上下文里。

在 Skill 大规模进入大家视野之前，AI 交互和 AI 应用优化最核心的方法，其实一直是 **提示词工程（Prompt Engineering）**。

提示词工程解决的是一个非常基础、但又非常关键的问题：

> **当模型本身已经很强时，如何通过更好的输入设计，让它更准确、更稳定、更低成本地完成任务。**

如果用最朴素的话来讲，提示词工程就是：

- 你如何提问
- 你给多少背景
- 你如何限制格式
- 你如何让模型先思考再回答
- 你如何减少跑题、幻觉和格式漂移

这一套方法，本质上是在提升“人和模型之间的对齐度”。

根据你给的菜鸟教程资料，提示词工程里有几个特别重要的原则，我觉得它们几乎就是后来 Skill 设计哲学的前传。

### 1. 清晰比华丽更重要

Prompt Engineering 最重要的一条，不是会不会写 fancy 提示词，而是：

- 说清楚任务
- 说清楚受众
- 说清楚输出格式
- 说清楚不要做什么

### 2. 角色、上下文、约束、格式，本来就是 Prompt 的基本骨架

一个成熟 Prompt 往往包括：

- 角色设定
- 背景知识
- 规则约束
- 输出格式
- 示例

这和一个优秀 Skill 的结构其实是同源的。

区别在于：

- Prompt 是一次性装配
- Skill 是长期模块化沉淀

换句话说，Skill 不是 Prompt Engineering 的反面，而是它的工程化延伸。

### 3. Prompt Chaining 已经隐含了“工作流”的思想

提示词工程后来演化出一个很重要的方法，叫 **Prompt Chaining**：

- 第一步提取信息
- 第二步分析信息
- 第三步生成结果
- 前一步输出作为后一步输入

这个思想已经非常接近 Skill 的工作流设计了。

### 4. 为什么 Prompt Engineering 最终会走向 Skill

因为 Prompt Engineering 虽然强，但它天然有几个局限：

- 它太依赖每次临时写 Prompt
- 很难系统复用
- 复杂场景下上下文会膨胀
- 经验往往留在对话里，而不是沉淀成资产

所以从工程演化角度看，Skill 并不是一个突兀的新发明，而更像是：

> **Prompt Engineering 在 Agent 时代的一次模块化、资产化、工作流化升级。**

---

## 二、从 Prompt、Rules、MCP 到 Skill：中间到底缺了什么

如果我们回看过去一年 AI 应用的演化，大多数增强方式大概可以分成三层。

### 1. Prompt：一次性告诉模型这次怎么做

这是大家最熟悉的方式。

### 2. Rules / Memory：长期约束模型的行为或偏好

它适合解决风格和边界，但不适合承载一个复杂工作流。

### 3. Tools / MCP：让模型拥有能力接入

它解决的是：模型能不能读数据库、调 API、访问外部系统。

但它解决不了：

- 先该做什么
- 后该做什么
- 哪些步骤要校验
- 哪些工具该怎么组合

### 4. Skill：把能力接入提升为工作流能力

所以如果要用一句最简洁的话来概括：

- **Prompt**：这次怎么做
- **Rules**：平时该怎么表现
- **MCP / Tools**：你能调用什么
- **Skill**：遇到这类事，应该按什么专业流程去做

---

## 三、Skill 的本质：不是一个文件，而是一种上下文工程方法

Skill 的真正核心，不在于 `SKILL.md` 这几个字符，而在于一种非常适合 Agent 的上下文组织方式：

> **Progressive Disclosure（渐进式披露 / 按需加载）**

### 1. 为什么“全塞上下文”不是好办法

- token 成本高
- 上下文污染严重
- 模型注意力分散
- 不相关规则也一直占着上下文

### 2. Skill 的三层加载模型

#### 第一层：元数据层
启动时只暴露：
- `name`
- `description`

#### 第二层：主说明层
任务匹配后，再加载 `SKILL.md` 正文。

#### 第三层：资源层
按需读取：
- `references/`
- `scripts/`
- `assets/`

### 3. 这为什么是架构升级

渐进式披露意味着：
- 能力可发现
- 能力可触发
- 信息可按需展开
- 资源可拆分维护
- 工作流可持续演化

---

## 四、一个 Skill 到底长什么样

最小 Skill：

```text
my-skill/
└── SKILL.md
```

更完整的 Skill：

```text
my-skill/
├── SKILL.md
├── references/
├── scripts/
└── assets/
```

---

## 五、完整 Skill 示例：以 `ant-design/antd-skill` 为例

这里直接用一个真实项目来举例：

- `https://github.com/ant-design/antd-skill`

这是一个很好的示范，因为它不是在做 toy demo，而是在做：

> **把一个成熟前端生态（Ant Design）的知识、决策逻辑和工具使用方式，封装成 Agent 可以消费的 Skill。**

### 1. 这个仓库在做什么

根据仓库说明，`antd-skill` 是一个面向 Ant Design 生态的 Agent Skills 集合，里面至少包含两类能力：

- `ant-design`：聚焦 antd v6、Ant Design Pro 5、Ant Design X v2 的决策指导
- `antd`：聚焦离线 Ant Design CLI 工作流，用于 API 查询、调试、迁移和使用分析

### 2. 为什么这个例子很典型

#### 第一，它不是 end-user tutorial，而是 agent decision guide

仓库 README 明确强调，这套 Skill 更关注 **agent decision-making**，不是给终端用户看的教程。

#### 第二，它采用单一 `SKILL.md` 保持核心简洁

这体现了一个高级原则：

> **不是信息越多越好，而是要把最关键的决策路径放在最靠前、最轻量的地方。**

#### 第三，它和工具链能力形成了天然闭环

这点放到 `ant-design-cli` 一起看，会更明显。

---

## 六、真实 `SKILL.md` 拆解：以 `ant-design/antd-skill` 为例逐段分析

如果只停留在“仓库层面”讨论 Skill，其实还不够。真正有说服力的分享，最好直接拆一个真实的 `SKILL.md` 文件。

这里我们直接看：

- `https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/ant-design/SKILL.md`

这个文件很适合拿来做逐段拆解，因为它的结构非常克制，但信息密度很高。

### 1. Frontmatter：不是元数据装饰，而是触发与边界声明

它的开头是：

```md
---
name: ant-design
description: Decision guide for antd 6.x, Ant Design Pro 5/ProComponents, Ant Design X v2, and the offline `@ant-design/cli`. Use for component selection, theming/tokens, SSR, a11y, performance, routing/access/CRUD, AI/chat UI patterns, local API lookup, debugging, migration, and usage analysis.
---
```

这一段特别值得讲。

先看 `name`：
- 没有花哨命名
- 直接对应生态名 `ant-design`
- 稳定、明确、适合长期维护

再看 `description`，它做了几件非常对的事：

#### 第一，先说覆盖范围
- antd 6.x
- Ant Design Pro 5 / ProComponents
- Ant Design X v2
- 以及离线 `@ant-design/cli`

这意味着它不是一个模糊的“前端 UI Skill”，而是一个明确锚定在 Ant Design 生态上的能力模块。

#### 第二，直接说适用场景
它没有只写“帮助使用 Ant Design”，而是明确列出：
- component selection
- theming / tokens
- SSR
- a11y
- performance
- routing / access / CRUD
- AI/chat UI patterns
- local API lookup
- debugging
- migration
- usage analysis

这类写法的好处是：

- 模型知道什么时候该触发
- 也知道什么时候不该触发
- 触发时知道应该优先处理哪类任务

也就是说，这个 `description` 不是在“介绍产品”，而是在做**能力路由声明**。

### 2. S - Scope：先划边界，再谈能力

正文一开始不是立刻开始操作步骤，而是：

```md
## S - Scope
```

下面先定义：
- 目标技术栈
- 工具范围
- 关注重点
- source policy

这是一个很成熟的写法，因为很多 Skill 一上来就讲流程，却没有先划边界，导致后续执行时容易发散。

例如这里明确说：
- Target 是 `antd@^6` + React 18-19
- Tooling 是 `@ant-design/cli`
- Focus 是 decision guidance only
- Source policy 是 official docs only

这等于先告诉 Agent：

> 你不是来写教程的，你是来做决策指导的；你只能依赖官方来源；你要在明确版本语境里工作。

这比很多泛化 Skill 成熟得多。

### 3. Default assumptions：把默认前提显式化

它接着写了：
- Language: TypeScript
- Styling: tokens first, then `classNames` / `styles`
- Provider: one root `ConfigProvider`

这是 Skill 里一个非常值得借鉴的设计点。

很多项目中都有一些“大家默认知道”的前提，比如：
- 默认语言
- 默认架构
- 默认主题方式
- 默认 Provider 组织方式

如果不写，模型就只能猜；
如果写出来，模型的行为就会稳定很多。

所以这一段本质上是在做：

**把隐性团队约定变成显性机器前提。**

### 4. Mandatory rules：这里才是 Skill 最有力量的地方

文件里最强的一段之一，是这一组 Mandatory rules。

例如：

- 在写或改 antd 组件代码前，先用 `antd info <Component> --format json` 查询 API
- 永远使用 `--format json`
- 如果版本重要，就带 `--version`
- 修改 antd 代码后，要运行 `antd lint <changed-path> --format json`
- 如果 CLI 自身出错，应该准备 `antd bug-cli` preview，而不是静默绕过

这一段很能说明什么叫“Skill 不是知识备忘录，而是执行约束”。

好的 Skill 不只是告诉 Agent “可以做什么”，更要告诉它：

- 做之前先查什么
- 做之后要验什么
- 发现工具异常时怎么处理
- 哪些习惯是硬规则，不是建议

这就是 Skill 最有工程价值的部分。

### 5. P - Process：把工作流压缩成可复用的决策路径

接下来它把流程拆成：
- Classify
- Query authoritative sources
- Decide

这种写法很值得借鉴，因为它不是把流程写成特别细碎的流水账，而是抽成 3 个稳定阶段：

#### Classify
先判断：
- 是 core antd、Pro 还是 X
- 确认版本、渲染模式、数据规模
- 判断 CLI 是否应该成为 primary lookup path

#### Query authoritative sources
再决定从哪里查：
- `antd info`
- `antd demo`
- `antd doc`
- `antd token`
- `antd semantic`
- `antd doctor`
- `antd lint`
- `antd usage`
- `antd migrate`
- `antd changelog`

#### Decide
最后才进入方案选择：
- Provider baseline
- Theming baseline
- 风险与验证点

这说明一个成熟 Skill 的流程设计，并不是“想到什么写什么”，而是：

> 先分类，再查权威信息，最后再决策。

这是非常专业的工作流结构。

### 6. O - Output：提前规定输出结构

最后它还定义了 Output 要包含：
- 短决策理由
- provider / theming strategy
- SSR / a11y / perf checks
- Pro 和 X 场景下的额外方向说明

这意味着 Skill 不只是管过程，还把“最后应该交付成什么样”规定清楚了。

这对 Agent 非常重要，因为没有输出约束，模型很容易生成“看起来很多，但不够可用”的答案。

### 7. 为什么这个 `SKILL.md` 是一个很好的示范

我觉得这个例子最值得借鉴的，不是它用了 S / P / O 结构本身，而是它体现了几个成熟特征：

- 先划边界，再给流程
- 强依赖权威来源
- 强约束工具使用方式
- 把“查询 → 决策 → 验证”串成闭环
- 让 Skill 承担规范化执行，而不是泛泛介绍

这类 Skill 才真正接近“给 Agent 的岗位培训手册”。

---

## 七、配套工具链示例：为什么 `ant-design-cli` 是 Skill 生态的理想搭档

另一个非常值得讲的例子，是：

- `https://github.com/ant-design/ant-design-cli`

这个项目非常适合拿来说明一件事：

> **Skill 最强的地方，从来不是独立存在，而是和工具、CLI、MCP 一起构成完整的 Agent 工作流。**

### 1. `ant-design-cli` 做的事情非常 Agent 友好

从仓库介绍来看，这个 CLI 的定位非常明确：

- 在命令行中提供 Ant Design 组件知识查询
- 分析项目使用情况
- 提供迁移指导
- 全离线运行
- 面向 code agents 优化
- 支持结构化 JSON 输出
- 还可以作为 MCP server 启动

### 2. 它为什么特别适合和 Skill 配合

仓库里明确提到，这个 CLI 自带一个 `skills/antd/SKILL.md`，并支持作为 agent skill 安装。

这意味着：
- CLI 负责提供可靠、结构化、可执行的底层能力
- Skill 负责教 Agent **何时、如何、按什么顺序** 去使用这些命令

### 3. 看几个典型命令，就能理解它为什么适合 Agent

例如：
- `antd list`
- `antd info Button`
- `antd doc Button`
- `antd demo Select basic`
- `antd token Button`
- `antd semantic Table`
- `antd changelog 4.24.0 5.0.0 Select`
- `antd doctor`
- `antd usage ./src`
- `antd lint ./src`
- `antd migrate 4 5 --apply ./src`

这些命令天然覆盖了 Agent 最擅长接管的几类任务：
- 查询
- 分析
- 比较
- 检查
- 迁移
- 生成修复路径

---

## 八、再拆一个真实 `SKILL.md`：`ant-design-cli` 自带 Skill 为什么像一份操作手册

除了 `ant-design/antd-skill` 仓库里的 Skill，`ant-design-cli` 自己也带了一个非常值得分析的 `skills/antd/SKILL.md`：

- `https://raw.githubusercontent.com/ant-design/ant-design-cli/main/skills/antd/SKILL.md`

这个文件和前面那个 `ant-design` Skill 的风格很不一样。

前者更像“决策指南”；
后者更像“命令行工作流操作手册”。

这两个示例放在一起看，其实特别能说明：

> **Skill 不是单一写法，而是可以根据场景承担不同层级的职责。**

### 1. 它的 frontmatter 更强烈地绑定了使用触发条件

例如它的 `description` 会明确写：
- 用户任务涉及 Ant Design
- 包括写组件、调试、查询 props/tokens/demos
- 涉及迁移或 usage 分析
- 会被 antd 相关代码、`import from 'antd'`、显式问题触发

这是一种非常典型的“面向任务检测”的 description 写法。

而且它还带了 `allowed-tools`，例如：
- `Bash(antd *)`
- `Bash(antd bug*)`
- `Bash(npm install -g @ant-design/cli*)`
- `Bash(which antd)`

这进一步说明，Skill 在很多实现里不仅是知识模块，也是工具调用边界的一部分。

### 2. Setup 段落体现了“Skill 负责把工具准备好”

这个 `SKILL.md` 的前半部分，就已经非常操作化：

- 先检查 `which antd`
- 没装就自动 `npm install -g @ant-design/cli`
- 如果提示 Update available，就先升级
- 永远使用 `--format json`

这种写法和普通教程最大的差别在于：

它不是在“介绍工具怎么用”，而是在告诉 Agent：

> 进入这个工作域后，先把环境和调用约束处理好，再继续执行。

### 3. Scenarios 段落像一组预置工作流模板

这个 Skill 最大的亮点之一，是它按场景拆了很多 workflow，例如：

- Writing antd component code
- Looking up full documentation
- Debugging antd issues
- Migrating between versions
- Analyzing project usage
- Checking changelogs
- Exploring components
- Collecting environment info
- Reporting antd bugs
- Auto-reporting CLI issues
- Using as MCP server

这已经非常接近一份“Agent 任务剧本”。

每个场景都写了：
- 什么时候用
- 该跑哪些命令
- 命令顺序是什么
- workflow 应该怎么走

例如“写组件代码”场景里，会明确要求：

```bash
antd info Button --format json
antd demo Button basic --format json
antd semantic Button --format json
antd token Button --format json
```

并强调 workflow 是：

> `antd info` → 理解 props → `antd demo` → 取工作示例 → 再写代码

这就是一种非常典型的 Skill 思维：

- 不是让 Agent 自由发挥
- 而是给它一个稳定可复用的工作流骨架

### 4. “Auto-report CLI issues” 这段特别有代表性

我觉得这个 Skill 最妙的一段，是它要求 Agent：

如果在使用 `antd` CLI 的过程中，发现命令崩溃、返回错误数据、行为和文档不一致、不同命令之间出现不一致，就应该主动准备 `antd bug-cli` 报告预览，并征求用户确认后提交。

这一段很有代表性，因为它展示了 Skill 不只是“教你怎么用工具”，还在教 Agent：

- 如何做质量反馈
- 遇到工具异常时不要默默绕过
- 如何形成工具生态的正反馈闭环

这比很多单纯“让 Agent 去调用命令”的方案成熟得多。

### 5. 这个 Skill 的价值，不只是命令清单，而是“行为标准化”

如果你只是看命令本身，会觉得这不过是一份 CLI 使用指南。

但从 Agent 角度看，它更重要的是做了三件事：

- 把命令映射到具体任务场景
- 把命令顺序固化成 workflow
- 把异常处理和质量反馈纳入流程

这就是为什么我会说：

> 一个高质量的 Skill，最终都会从“知识罗列”演化成“行为标准化”。

---

## 九、Skill / CLI / MCP：三层架构应该怎么理解

到这里，我们已经有了两个非常合适的例子：
- `antd-skill`
- `ant-design-cli`

现在可以把它们抽象成一个更通用的三层架构视角。

### 1. 第一层：Skill 层 —— 决策与工作流层

Skill 最适合承载的内容包括：
- 任务分类
- 决策规则
- 步骤顺序
- 输出约束
- 风险检查
- 工具调用时机

它负责回答的是：

- 现在应该做什么
- 下一步该做什么
- 哪个工具该什么时候上场
- 成功和失败如何判断

所以可以把 Skill 看成：

**Agent 的工作流大脑。**

### 2. 第二层：CLI / Script 层 —— 可执行能力层

CLI、脚本、可执行工具最适合承载：
- 查询
- 校验
- lint
- migration
- 数据分析
- 环境诊断
- 结构化输出

它解决的是：

- 怎样高效、确定性地完成某一步
- 怎样避免模型自己“编一个答案”
- 怎样把结果交给后续步骤继续处理

所以 CLI / Script 层更像：

**Agent 的执行器和传感器。**

### 3. 第三层：MCP 层 —— 原生工具暴露与系统接入层

MCP 最适合承载：
- 把能力暴露成原生可调用工具
- 让 IDE / Agent runtime 统一接入
- 让外部系统变成可编排能力源

它解决的是：
- 工具怎么被稳定接入
- 外部系统能力怎么进入 Agent 运行环境
- 多工具如何在统一协议下协同

所以 MCP 更像：

**Agent 的能力接口层。**

### 4. 三层是怎么协同工作的

一个很典型的执行链路会是：

1. 用户提出问题
2. Skill 判断任务类型与执行路径
3. Skill 选择调用 CLI 或 MCP 工具
4. CLI / MCP 返回结构化数据
5. Skill 根据结果继续决策、补充验证、组织输出

这意味着：

- Skill 不负责底层数据细节
- CLI 不负责整体工作流判断
- MCP 不负责业务决策逻辑

它们各自分工明确，但一起才能构成真正稳定的 Agent 系统。

### 5. 为什么这个架构视角很重要

因为很多团队在做 Agent 时容易出现两个极端：

#### 极端一：只有 Prompt / Skill，没有可执行工具
结果是：
- 模型会讲，但做不实
- 流程像样，但结果不够确定

#### 极端二：只有一堆工具，没有 Skill 编排
结果是：
- 工具很多
- 但 Agent 不知道何时用、先后顺序、校验边界
- 最终交付不稳定

真正成熟的方案通常是三层协同：

- **Skill** 负责工作流与决策
- **CLI / Script** 负责执行与校验
- **MCP** 负责标准化接入与工具暴露

这也是为什么 `ant-design/antd-skill + ant-design-cli` 这个组合，值得在技术分享里重点讲。

它不是因为它“是 Ant Design”，而是因为它清楚地把这三层关系都示范出来了。

---

## 十、Skill 与 MCP 的真正关系：不是二选一，而是上下两层

MCP 的核心价值，是把外部系统能力接给 Agent。

Skill 解决的问题则是：
- 遇到这类任务时先做什么
- 哪些工具该按什么顺序调用
- 哪些信息必须校验
- 哪些阶段需要确认
- 产物应该如何串起来

所以更准确地说：
- MCP 给 Agent 提供“器官”
- Skill 给 Agent 提供“神经回路”

---

## 十一、OpenClaw、Claude Code、Google ADK：Skill 生态的横向对比

### 1. Claude Code：Skill 生态的标准化推动者之一

特点：
- Skill 目录结构清晰
- `SKILL.md` + YAML frontmatter 约定明确
- 强调 progressive disclosure
- 很适合以“工作流和知识封装”的方式增强 code agent

### 2. Google ADK：更强调 SkillToolset 和程序化组装

特点：
- inline skills
- file-based skills
- external skills
- skill factory
- 更偏“Agent 架构设计”和“程序化编排”

### 3. OpenClaw：更强调真实运行环境、技能分发与本地工作流落地

特点：
- 兼容 AgentSkills 风格目录
- 多层级加载
- allowlist / precedence / gating
- 非常适合真实生产环境中的 agent automation

### 4. 一个简化对比表

| 维度 | Claude Code | Google ADK | OpenClaw |
|---|---|---|---|
| 核心视角 | 工作流 / 知识封装 | 程序化 SkillToolset | 本地 Agent Harness + 技能分发 |
| Skill 形态 | 文件夹 + `SKILL.md` | Inline / File / External / Factory | AgentSkills 兼容文件夹 |
| 强项 | 技能触发和上下文加载自然 | 架构化、程序化、可扩展 | 真实工作区、本地工具、消息渠道集成 |
| 更适合 | 个人/团队 code agent 增强 | Agent 系统开发者 | 需要运行型 Agent 的团队/个人 |
| 与工具协同 | 强 | 很强 | 很强 |
| 与 MCP 结合 | 有 | 强调工具系统化接入 | 非常贴近真实落地 |

### 5. 我的判断

- **Claude Code** 更像 Skill 生态的范式推动者
- **Google ADK** 更像 Skill 的程序化架构实验场
- **OpenClaw** 更像 Skill 在真实 Agent 运行环境中的落地操作系统

---

## 十二、写 Skill 时最容易踩的坑

### 1. description 太泛，导致触发失败或乱触发
### 2. 把 `SKILL.md` 写成说明书小说
### 3. 只写“做什么”，不写“怎么判断”
### 4. 明明可以脚本化，却全靠模型自由发挥
### 5. 从来不做触发测试与回归测试

---

## 十三、为什么我认为 Skill 会成为一种重要的能力资产

### 1. Skill 让个人经验第一次真正可工程化复用
### 2. Skill 让 Agent 从“会回答”走向“会稳定做事”
### 3. Skill 让组织知识从文档库变成执行资产

---

## 十四、如果今天开始做 Skill，我会怎么建议团队落地

### 1. 从最痛的重复任务开始
### 2. 先做单点高频，不要追求大而全
### 3. 先人工跑通，再抽象成 Skill
### 4. Skill 与 MCP 要一起设计

---

## 十五、结语：Skill 不是 Prompt 的小升级，而是 Agent 工程化的一块关键拼图

> **Prompt Engineering 解决的是“怎么把一句话说清楚”，而 Skill Engineering 解决的是“怎么把一套工作方法沉淀成 Agent 能长期复用的能力”。**

Skill 正好处在一个非常关键的位置：
- 向下连接工具能力
- 向上承载业务工作流
- 横向沉淀组织经验
- 纵向支持持续迭代

所以它更像是：

**Agent 时代把“工作方法”变成“能力资产”的最轻量、最现实、也最容易规模化的一种载体。**

---

## 参考资料

- Prompt Engineering（菜鸟教程）  
  https://www.runoob.com/ai-agent/prompt-engineering.html

- Skills 教程（菜鸟教程）  
  https://www.runoob.com/ai-agent/skills-agent.html

- Anthropic：Equipping agents for the real world with Agent Skills  
  https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills

- Google Developer Blog：Developer’s Guide to Building ADK Agents with Skills  
  https://developers.googleblog.com/developers-guide-to-building-adk-agents-with-skills/

- OpenClaw Docs：Skills  
  https://docs.openclaw.ai/tools/skills

- OpenClaw Docs：Creating Skills  
  https://docs.openclaw.ai/tools/creating-skills

- awesome-agent-skills  
  https://github.com/libukai/awesome-agent-skills

- Claude Skills 完全构建指南  
  https://github.com/libukai/awesome-agent-skills/blob/main/docs/Claude-Skills-%E5%AE%8C%E5%85%A8%E6%9E%84%E5%BB%BA%E6%8C%87%E5%8D%97.md

- Ant Design Skills 仓库  
  https://github.com/ant-design/antd-skill

- Ant Design `ant-design` Skill 原始文件  
  https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/ant-design/SKILL.md

- Ant Design `antd` Skill 原始文件  
  https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/antd/SKILL.md

- Ant Design CLI 仓库  
  https://github.com/ant-design/ant-design-cli

- Ant Design CLI 自带 Skill 原始文件  
  https://raw.githubusercontent.com/ant-design/ant-design-cli/main/skills/antd/SKILL.md
