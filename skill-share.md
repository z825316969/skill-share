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

比如：

- “帮我写一篇关于猫的文章” 是模糊提示
- “请以轻松幽默的口吻，为养猫新手写一篇 800 字文章，重点介绍接猫回家前三天要做的准备，包含 3 个小标题，结尾附 checklist” 就是更高质量的提示

这件事非常重要，因为 Skill 后来做的，其实是把这种“说清楚任务”的能力，从一次性交互提升成了可复用结构。

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

也就是说，在 Prompt Chaining 里，大家已经意识到：

> 复杂任务不能只靠一条“超级提示词”完成，而应该被拆成多个阶段。

Skill 只是把这个思想继续推进了一步：

- 不再只是临时串 Prompt
- 而是把这套工作流固化成可触发、可维护、可共享的能力模块

### 4. 为什么 Prompt Engineering 最终会走向 Skill

因为 Prompt Engineering 虽然强，但它天然有几个局限：

- 它太依赖每次临时写 Prompt
- 很难系统复用
- 复杂场景下上下文会膨胀
- 经验往往留在对话里，而不是沉淀成资产

所以从工程演化角度看，Skill 并不是一个突兀的新发明，而更像是：

> **Prompt Engineering 在 Agent 时代的一次模块化、资产化、工作流化升级。**

理解这一点很重要，因为它能帮我们避免把 Skill 看成一个孤立概念。

---

## 二、从 Prompt、Rules、MCP 到 Skill：中间到底缺了什么

如果我们回看过去一年 AI 应用的演化，大多数增强方式大概可以分成三层。

### 1. Prompt：一次性告诉模型这次怎么做

这是大家最熟悉的方式。

比如你想让模型把一篇技术文章改成公众号风格，于是你会写一大段：

- 先总结文章
- 再提炼观点
- 再改成更口语化的中文
- 增加标题和导语
- 输出 Markdown

这种方式的问题很明显：

- 每次都要重写
- 一旦漏掉要求，结果就漂
- 随着任务变复杂，Prompt 会越来越长
- 很多隐性经验无法稳定复现

所以 Prompt 更像是一次性的口头交代。

### 2. Rules / Memory：长期约束模型的行为或偏好

第二层常见增强方式是记忆、规则、系统提示中的偏好配置。

它适合解决：

- 输出风格
- 基本行为边界
- 常驻偏好
- 长期上下文

例如：

- 默认优先用中文回答
- 默认先给结论
- 默认搜索时优先某个来源
- 某些信息不允许外发

但 Rules 不适合承载一个复杂工作流。

因为它更像“行为约束”，而不是“任务执行方法”。

### 3. Tools / MCP：让模型拥有能力接入

第三层是工具和 MCP。

它解决的是：

- 模型能不能读数据库
- 能不能调 API
- 能不能操作浏览器
- 能不能访问 Notion / Linear / Slack / GitHub

这一步非常关键，因为没有工具，Agent 很多时候只是会说，不会做。

但这里马上出现另一个问题：

> 给了模型工具，不等于给了它稳定完成复杂任务的能力。

一个典型例子是：

你把 Linear、Slack、Drive、Figma 都接给了 Agent，它确实“能调用”这些工具，但你让它做一次完整的设计交付流程，它未必知道：

- 先该读什么
- 后该创建什么
- 哪些字段必须校验
- 设计稿和任务之间如何挂接
- 成功和失败的判定条件是什么

也就是说，Tools / MCP 解决的是“可达性”，不是“方法论”。

### 4. Skill：把能力接入提升为工作流能力

Skill 的价值就在这里。

它把“调用能力”进一步提升成“执行方法”。

所以如果要用一句最简洁的话来概括：

- **Prompt**：这次怎么做
- **Rules**：平时该怎么表现
- **MCP / Tools**：你能调用什么
- **Skill**：遇到这类事，应该按什么专业流程去做

这就是 Skill 诞生的背景，也是它为什么会突然重要起来。

---

## 三、Skill 的本质：不是一个文件，而是一种上下文工程方法

很多介绍 Skill 的文章，会先告诉你目录结构。我也会讲结构，但我更想先讲它背后的方法。

Skill 的真正核心，不在于 `SKILL.md` 这几个字符，而在于一种非常适合 Agent 的上下文组织方式：

> **Progressive Disclosure（渐进式披露 / 按需加载）**

这个概念几乎可以说是理解 Skill 的钥匙。

### 1. 为什么“全塞上下文”不是好办法

过去 Prompt Engineering 里一个常见做法，是把所有规则、流程、案例、格式要求一次性塞进系统提示词或用户提示里。

短任务还行，复杂任务就会很快出现问题：

- token 成本高
- 上下文污染严重
- 模型注意力分散
- 不相关规则也一直占着上下文

举个简单的例子。

如果一个 Agent 同时具备：

- 写技术文章
- 做 PR Review
- 生成周报
- 处理财务报销
- 做设计交付

你总不能把这 5 套完整 SOP 永久塞在系统提示里。那不是增强，是噪音。

### 2. Skill 的三层加载模型

Skill 优雅的地方在于，它把上下文加载分成了几层。

#### 第一层：元数据层

在启动时，Agent 只需要知道每个 Skill 的最小信息，通常包括：

- `name`
- `description`

这层的目标非常克制：

**只负责让模型知道“什么时候可能该用这个 Skill”。**

它不承担执行细节。

#### 第二层：主说明层

只有当模型判断当前任务与某个 Skill 匹配时，才去读取这个 Skill 的 `SKILL.md` 正文。

这部分通常包含：

- 核心流程
- 阶段步骤
- 输出标准
- 错误处理
- 对参考资料和脚本的调用提示

也就是说，真正的 SOP 不是常驻的，而是在需要时才加载。

#### 第三层：资源层

如果 Skill 更复杂，还可以继续往下拆：

- `references/`：风格规范、案例、术语表、API 文档
- `scripts/`：确定性脚本、检查工具、格式转换器
- `assets/`：模板、样板、图标、结构化资源

这层更进一步，把“不是每次都需要”的内容从主说明里移出去。

结果就是：

- 日常上下文更轻
- 复杂 Skill 也能做大
- 模型在执行时不会被无关细节淹没

### 3. 为什么这不是“小技巧”，而是一种重要架构

我觉得很多人还没有意识到，渐进式披露不是一个简单的 token 优化技巧，而是一种非常关键的 Agent 架构设计原则。

它意味着我们不再把 Agent 能力看成一段巨大、静态、全量加载的说明书，而是把能力拆成：

- 可发现
- 可触发
- 可按需展开
- 可组合
- 可演化

这就是 Skill 真正和“长 Prompt 模板”拉开差距的地方。

---

## 四、一个 Skill 到底长什么样

说完理念，再回到最表层的结构。

一个最小 Skill 目录通常是这样：

```text
my-skill/
└── SKILL.md
```

一个更完整、工程化的 Skill，通常会长这样：

```text
my-skill/
├── SKILL.md
├── references/
├── scripts/
└── assets/
```

其中：

- `SKILL.md` 是入口文件
- `references/` 放按需参考资料
- `scripts/` 放需要执行的脚本
- `assets/` 放模板或静态资源

### 一个最小可用的 `SKILL.md`

下面是一个非常简单但有效的例子：

```md
---
name: article-to-wechat
description: Rewrite long-form technical content into concise WeChat-style posts. Use when user asks to summarize, rewrite, polish, or adapt articles for公众号/社媒发布.
---

# Article to WeChat

## Instructions

1. Read the source content first.
2. Extract key观点、结论与结构。
3. Rewrite into a punchier WeChat style.
4. Add标题、导语、小结。
5. Output clean Markdown.
```

这个 Skill 很短，但它已经具备了最重要的几个元素：

- 有明确名字
- 有可触发的描述
- 有清晰的执行步骤
- 没有废话

### 为什么很多 Skill 写得很长，反而变差

一个常见误区是：为了让 Skill 看起来“专业”，把大量背景、解释、概念介绍塞进 `SKILL.md`。

结果通常是反效果。

因为模型本来就已经很懂通用知识。Skill 最应该提供的是：

- 模型原本不知道的业务知识
- 该场景特有的判断标准
- 输出要求
- 执行顺序
- 失败处理方式

所以一个好 Skill 的原则通常是：

> **只补模型本来不知道、但做这件事必须知道的内容。**

---

## 五、完整 Skill 示例：以 `ant-design/antd-skill` 为例

如果前面讲的都还偏抽象，那么一个真正好的例子，应该来自真实项目，而不是临时虚构的 toy demo。

这里我想直接用你指定的公开仓库来举例：

- [Ant Design Skills 仓库](https://github.com/ant-design/antd-skill)

这是一个非常好的示范，因为它不是单纯在讲“怎么写一个 Skill”，而是在做一件更有代表性的事：

> **把一个成熟前端生态（Ant Design）的知识、决策逻辑和工具使用方式，封装成 Agent 可以消费的 Skill。**

### 1. 这个仓库在做什么

根据仓库说明，`antd-skill` 是一个面向 Ant Design 生态的 Agent Skills 集合，里面至少包含两类能力：

- `ant-design`：聚焦 antd v6、Ant Design Pro 5、Ant Design X v2 的决策指导
- `antd`：聚焦离线 Ant Design CLI 工作流，用于 API 查询、调试、迁移和使用分析

这点特别值得注意。

因为它说明一个成熟 Skill 仓库，不一定只封装“静态知识”，它可以同时封装：

- 决策逻辑
- 文档路径
- 版本语义
- CLI 使用方式
- 迁移流程
- 调试和诊断路径

换句话说，这已经非常接近“领域专家 onboarding 包”了。

### 2. 为什么这个例子很典型

它典型在三件事上：

#### 第一，它不是 end-user tutorial，而是 agent decision guide

仓库 README 明确强调，这套 Skill 更关注 **agent decision-making**，不是给终端用户看的教程。

这一点很关键。

因为 Skill 的本质从来不是“给人看文档”，而是：

**给 Agent 一套在该生态里做决策时应该遵循的路径。**

#### 第二，它采用单一 `SKILL.md` 保持核心简洁

仓库描述里提到，这些 Skill 采用的是“single SKILL.md”导向，强调简洁，并通过链接或官方文档引用保持内容聚焦。

这刚好体现了 Skill 设计中的一个高级原则：

> **不是信息越多越好，而是要把最关键的决策路径放在最靠前、最轻量的地方。**

#### 第三，它和工具链能力形成了天然闭环

这点我们放到下一节和 `ant-design-cli` 一起讲，会更清楚。

### 3. 从这个示例里可以学到什么

`antd-skill` 最值得借鉴的，不只是它写了一个 Skill，而是它展示了一种很成熟的 Skill 设计思路：

- 不是泛泛介绍框架
- 而是明确区分场景
- 明确区分“生态决策指导”和“离线 CLI 工作流”
- 用 Skill 来承接真正高频、复杂、容易出错的任务

这也是我认为一个好 Skill 示例应该具备的特征：

- 有真实使用背景
- 有明确边界
- 有版本意识
- 有与工具协同的能力

---

## 六、真实 `SKILL.md` 拆解：以 `ant-design/antd-skill` 为例逐段分析

如果只停留在“仓库层面”讨论 Skill，其实还不够。真正有说服力的分享，最好直接拆一个真实的 `SKILL.md` 文件。

这里我们直接看：

- [Ant Design `ant-design` Skill 原始文件](https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/ant-design/SKILL.md)

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

如果说 `antd-skill` 体现的是“知识和决策的封装”，那另一个非常值得讲的例子，就是它配套的：

- [Ant Design CLI 仓库](https://github.com/ant-design/ant-design-cli)

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

这里面每一点都非常关键。

因为一个适合 Agent 使用的 CLI，不只是“功能强”，更重要的是：

- 输出要结构化
- 错误要可程序化处理
- 响应要快
- 最好脱离网络依赖
- 能嵌入 IDE / Agent runtime

`ant-design-cli` 几乎就是照着这些原则设计的。

### 2. 它为什么特别适合和 Skill 配合

仓库里明确提到，这个 CLI 自带一个 `skills/antd/SKILL.md`，并支持通过 agent skill 方式安装。

这意味着它不是把 CLI 和 Skill 当两套分离系统，而是把它们视为一体：

- CLI 负责提供可靠、结构化、可执行的底层能力
- Skill 负责教 Agent **何时、如何、按什么顺序** 去使用这些命令

这就是一个特别标准的“Skill + 工具链”组合范式。

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

你会发现，这些命令天然就覆盖了 Agent 最擅长接管的几类任务：

- 查询
- 分析
- 比较
- 检查
- 迁移
- 生成修复路径

---

## 八、再拆一个真实 `SKILL.md`：`ant-design-cli` 自带 Skill 为什么像一份操作手册

除了 `ant-design/antd-skill` 仓库里的 Skill，`ant-design-cli` 自己也带了一个非常值得分析的 `skills/antd/SKILL.md`：

- [Ant Design CLI 自带 Skill 原始文件](https://raw.githubusercontent.com/ant-design/ant-design-cli/main/skills/antd/SKILL.md)

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
- 没装就自动安装
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

讨论 Skill 时，另一个经常被问到的问题是：

> Skill 和 MCP 到底谁更重要？

我觉得这个问题本身就不太对。

因为这两者根本不是一个层面上的东西。

### 1. MCP 解决的是“能力接入”

MCP 的核心价值，是把外部系统能力接给 Agent。

例如：

- GitHub MCP：读 issue、开 PR、看 CI
- Linear MCP：查项目、建任务、更新状态
- Slack MCP：发消息、读频道
- Figma MCP：取设计资源
- 数据库 MCP：查数据

### 2. Skill 解决的是“工作流编排”

Skill 解决的问题则是：

- 遇到这类任务时先做什么
- 哪些工具该按什么顺序调用
- 哪些信息必须校验
- 哪些阶段需要确认
- 产物应该如何串起来

所以更准确地说：

- MCP 给 Agent 提供“器官”
- Skill 给 Agent 提供“神经回路”

### 3. 一个完整案例：设计交付流程

假设有这样一套工具能力：

- Figma MCP：读取设计稿、组件、资源
- Drive MCP：存放导出的交付文件
- Linear MCP：创建任务并关联研发流程
- Slack MCP：通知团队

现在需求是：

> 把一个设计稿转成研发可执行的交付包，并同步给工程团队。

如果你只有 MCP，没有 Skill，会发生什么？

Agent 可能确实知道这些工具“能用”，但它并不知道完整流程该怎么组织。它未必知道：

- 应该先从 Figma 拿到哪些内容
- 设计说明应该怎么组织
- Drive 里交付包目录怎么建
- Linear 任务字段如何填写
- Slack 通知里该带哪些链接
- 失败时应在哪一步中止

所以，只有 MCP，你拿到的是散装能力；
有了 Skill，你才能把这些散装能力组装成一个稳定工作流。

---

## 十一、OpenClaw、Claude Code、Google ADK：Skill 生态的横向对比

到了这里，一个很自然的问题是：

> 大家都在讲 Skill，那 OpenClaw、Claude Code、Google ADK 到底有什么差别？

我觉得可以从三个维度来看：

- Skill 的定位是什么
- Skill 和工具如何协同
- Skill 更偏“使用型”还是“开发型”

### 1. Claude Code：Skill 生态的标准化推动者之一

从外界认知上看，Claude / Claude Code 是最早让大量开发者开始正视 Skill 的平台之一。

它的特点是：

- Skill 目录结构清晰
- `SKILL.md` + YAML frontmatter 约定明确
- 与 Claude 的上下文加载机制结合紧密
- 强调 progressive disclosure
- 非常适合以“工作流和知识封装”的方式增强 code agent

你可以理解为：

**Claude Code 更像是让 Skill 成为“Agent 时代 SOP 模块”的标准化土壤。**

### 2. Google ADK：更强调 SkillToolset 和程序化组装

Google ADK 讲 Skill 时，往往不是从“写一个文件夹”开始，而是从：

- inline skills
- file-based skills
- external skills
- skill factory

这些模式切入。

它的特点是：

- 非常强调 Skill 作为程序化组件
- 更适合构建多 Agent / 多能力组合系统
- 有更鲜明的 toolset、resource loading、runtime integration 视角
- 特别适合工程团队把 Skill 当作系统设计的一部分

换句话说：

**Google ADK 的 Skill 视角更偏“Agent 架构设计”和“程序化编排”。**

### 3. OpenClaw：更强调真实运行环境、技能分发与本地工作流落地

OpenClaw 的独特之处在于，它并不只是一个“让模型读 Skill”的环境，而是一个实际运行在本地工作区、能连接消息渠道、能调工具、能跑外部流程的 Agent Harness。

它的 Skill 特点包括：

- 兼容 AgentSkills 风格目录
- 有 workspace / personal / shared / plugin 多层级加载
- 有 allowlist、precedence、gating 等机制
- 能结合本地工具、外部技能市场、插件系统一起工作
- 非常适合真实生产环境中的 agent automation

你可以把 OpenClaw 看成：

**把 Skill 从“模型增强模块”推进到了“可分发、可管理、可运行”的本地 Agent 能力系统。**

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

如果简单总结：

- **Claude Code** 更像 Skill 生态的范式推动者
- **Google ADK** 更像 Skill 的程序化架构实验场
- **OpenClaw** 更像 Skill 在真实 Agent 运行环境中的落地操作系统

这三者不是互斥关系，而更像同一趋势的不同切面。

---

## 十二、Skill 设计 checklist / 最佳实践清单

如果前面所有内容都要收敛成一个真正能落地的 takeaway，我觉得最适合的形式就是一份 checklist。

因为很多团队听完 Skill 分享之后，最容易卡住的不是“听不懂”，而是：

- 不知道从哪开始
- 不知道什么算好 Skill
- 不知道如何评审 Skill
- 不知道如何把 Skill 从 demo 做成可复用资产

下面这份清单，可以直接作为你做 Skill 设计、评审、迭代时的实操基线。

### A. 触发设计清单

- [ ] `name` 是否简洁、稳定、语义明确？
- [ ] `description` 是否明确写清楚“做什么 + 什么时候用 + 用户可能怎么说”？
- [ ] `description` 是否避免过于宽泛，降低误触发风险？
- [ ] 是否包含足够的任务关键词，而不是只写技术实现？
- [ ] 是否明确了 Skill 的作用边界，避免和其他 Skill 冲突？

### B. 内容结构清单

- [ ] `SKILL.md` 是否只保留核心流程，而不是堆满背景说明？
- [ ] 是否把细节资料拆到了 `references/`？
- [ ] 是否把确定性逻辑拆到了 `scripts/`？
- [ ] 是否把模板或静态资源放到了 `assets/`？
- [ ] 主文件是否足够短，方便模型快速抓住重点？

### C. 工作流设计清单

- [ ] 是否先定义了 Skill 的适用场景，再设计流程？
- [ ] 流程是否明确区分阶段，而不是平铺一堆动作？
- [ ] 是否写清楚每一步的输入、输出和判断条件？
- [ ] 是否明确哪些步骤必须先完成，哪些步骤可以跳过？
- [ ] 是否有失败中止、回退或补救路径？

### D. 工具协同清单

- [ ] Skill 是否明确了应该调用哪些 CLI / MCP / 内置工具？
- [ ] 是否规定了工具调用顺序，而不是交给模型自由猜测？
- [ ] 是否要求优先查询权威来源，而不是凭记忆生成？
- [ ] 是否优先采用结构化输出（如 JSON）供后续步骤消费？
- [ ] 是否对工具异常做了处理策略，而不是静默绕过？

### E. 输出质量清单

- [ ] 是否规定了最终输出结构，而不只是规定过程？
- [ ] 是否定义了结果最少应该包含哪些部分？
- [ ] 是否明确了质量检查项（如 SSR / a11y / performance / migration risk）？
- [ ] 是否给出了可验证的检查点，而不是抽象要求？
- [ ] 是否保证输出结果对人类用户“可直接使用”，而不是只对模型有意义？

### F. 测试与迭代清单

- [ ] 是否测试过明显应该触发的场景？
- [ ] 是否测试过换一种说法的场景？
- [ ] 是否测试过明显不该触发的场景？
- [ ] 是否在真实任务中观察过 Skill 的执行轨迹？
- [ ] 是否根据失败案例持续优化 description、流程和资源结构？

### G. 工程化与长期维护清单

- [ ] 这个 Skill 是否来源于真实高频任务，而不是拍脑袋设计？
- [ ] Skill 是否能被团队成员复用，而不是只适合作者本人？
- [ ] 是否有版本意识，能适配技术栈或依赖版本差异？
- [ ] 是否具备扩展空间，而不是一改就崩？
- [ ] 是否能作为团队的长期能力资产，而不只是短期 demo？

### 一句话版最佳实践

如果把所有 checklist 再压缩成最短的一句话，我会这样总结：

> **一个好 Skill，应该触发准确、边界清晰、流程稳定、工具协同自然、输出可验证，并且能在真实任务中持续迭代。**

这句话几乎可以作为你评审任何 Skill 的总纲。

---

## 十三、写 Skill 时最容易踩的坑

讲完方法和案例，再说点实际的。

因为 Skill 这个东西门槛低，导致很多人很快就能“写出来”；但真正好用的 Skill，其实很容易踩坑。

### 1. description 太泛，导致触发失败或乱触发

这是最常见、也最隐蔽的问题。

如果描述太泛，模型就不知道什么时候该触发；
如果描述太宽，它又会在无关任务里乱触发。

所以 description 的目标不是优雅，而是可路由。

### 2. 把 `SKILL.md` 写成说明书小说

Skill 不是写给人读的长文章，而是给 Agent 执行的操作说明。

如果主文件里充满大量背景解释，往往会导致：

- 重点不突出
- token 成本高
- 模型忽略关键步骤

正确做法是：

- 核心流程留在主文件
- 细节挪到 `references/`

### 3. 只写“做什么”，不写“怎么判断”

比如你写：

- 先检查质量
- 再修复问题

这种话对人都不够，对 Agent 更不够。

应该写成：

- 检查是否缺少标题、摘要、结论
- 检查段落是否过长
- 检查 Markdown 结构是否完整
- 不满足则逐项修正并重新校验

### 4. 明明可以脚本化，却全靠模型自由发挥

凡是确定性逻辑，都应该优先考虑写进 `scripts/`。

例如：

- 格式校验
- 文件结构检查
- 规则扫描
- 静态分析

原因很简单：

**代码比自然语言稳定。**

### 5. 从来不做触发测试与回归测试

Skill 不是写完即用完。

至少应该测试三类问题：

- 明显该触发的请求能不能触发
- 换个说法还能不能触发
- 明显不该触发的请求会不会误触发

如果一个 Skill 连触发边界都没测过，那大概率在真实环境里很不稳定。

---

## 十四、为什么我认为 Skill 会成为一种重要的能力资产

如果只从“是否方便”来看 Skill，它当然有价值；但我觉得它更大的价值，远不止方便。

### 1. Skill 让个人经验第一次真正可工程化复用

过去很多高手的优势，是隐性的。

他们知道：

- 怎么写一篇好文章
- 怎么做一次好的 review
- 怎么拆一个需求
- 怎么判断风险

但这些东西往往存在脑子里，很难复制。

Skill 的意义，就是把这些经验第一次压缩成 Agent 能直接使用的形态。

### 2. Skill 让 Agent 从“会回答”走向“会稳定做事”

很多 AI 系统的问题不是不会说，而是不会做。

Skill 的真正价值，不是让模型显得更聪明，而是让它在一个场景里更稳定、更一致、更可预期。

这对真正要交付结果的 Agent 来说，比“偶尔惊艳”重要得多。

### 3. Skill 让组织知识从文档库变成执行资产

传统知识库的一个问题是：

它能被搜索，但不一定能被执行。

Skill 则把知识从“文档形态”往“执行形态”推进了一步。

未来一个团队真正应该沉淀的不只是文档，而是：

- 文档 + 流程 + 校验 + 模板 + 调用方式

也就是 Skill 这种更接近可执行工作流的形态。

---

## 十五、如果今天开始做 Skill，我会怎么建议团队落地

最后落回到实操。

如果一个团队今天想开始做 Skill，我不建议上来就做一个“万能大脑”，而是建议这样推进。

### 1. 从最痛的重复任务开始

优先找那些你已经重复说过很多遍的话：

- 帮我把这篇文章改成公众号风格
- 帮我总结这个 PR 的风险点
- 帮我整理会议纪要成行动项
- 帮我按我们团队规范写发布说明

这种任务最值得优先 Skill 化。

### 2. 先做单点高频，不要追求大而全

Skill 成功的关键，是单点做透。

一上来就做“全能办公 Skill”，通常很快会失控。

更好的方式是先做：

- `article-to-wechat`
- `pr-review-summary`
- `meeting-notes-to-actions`
- `design-handoff`

把一个个高频场景打透，再逐渐形成技能库。

### 3. 先人工跑通，再抽象成 Skill

最稳的方法通常不是闭门造 Skill，而是：

1. 先用普通对话把这类任务做成功几次
2. 记录最有效的流程
3. 抽出稳定步骤和判断标准
4. 再写成 Skill
5. 用真实任务继续迭代

### 4. Skill 与 MCP 要一起设计

如果一个场景需要外部系统参与，那 Skill 和 MCP 最好一起设计。

不要先盲目把一堆工具接进来，再希望模型自己悟出流程。

正确做法应该是：

- 先定义业务目标
- 再设计工作流
- 然后看每一步需要哪些工具
- 最后把流程写进 Skill

这样落地效率会高得多。

---

## 十六、结语：Skill 不是 Prompt 的小升级，而是 Agent 工程化的一块关键拼图

如果要用一句话收束全文，我会这样说：

> **Prompt Engineering 解决的是“怎么把一句话说清楚”，而 Skill Engineering 解决的是“怎么把一套工作方法沉淀成 Agent 能长期复用的能力”。**

这两者当然不是敌对关系。

Prompt 仍然重要，MCP 仍然重要，Rules 也仍然重要。

但当我们真正开始构建可交付、可维护、可扩展的 Agent 系统时，Skill 这一层几乎是绕不过去的。

因为它正好处在一个非常关键的位置：

- 向下连接工具能力
- 向上承载业务工作流
- 横向沉淀组织经验
- 纵向支持持续迭代

所以我对 Skill 的判断一直很明确：

它不是一个小功能，也不是 Prompt 的文件化替代品。

它更像是：

**Agent 时代把“工作方法”变成“能力资产”的最轻量、最现实、也最容易规模化的一种载体。**

---

## 参考资料

- [Prompt Engineering（菜鸟教程）](https://www.runoob.com/ai-agent/prompt-engineering.html)
- [Skills 教程（菜鸟教程）](https://www.runoob.com/ai-agent/skills-agent.html)
- [Anthropic：Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [Google Developer Blog：Developer’s Guide to Building ADK Agents with Skills](https://developers.googleblog.com/developers-guide-to-building-adk-agents-with-skills/)
- [OpenClaw Docs：Skills](https://docs.openclaw.ai/tools/skills)
- [OpenClaw Docs：Creating Skills](https://docs.openclaw.ai/tools/creating-skills)
- [awesome-agent-skills](https://github.com/libukai/awesome-agent-skills)
- [Claude Skills 完全构建指南](https://github.com/libukai/awesome-agent-skills/blob/main/docs/Claude-Skills-%E5%AE%8C%E5%85%A8%E6%9E%84%E5%BB%BA%E6%8C%87%E5%8D%97.md)
- [Ant Design Skills 仓库](https://github.com/ant-design/antd-skill)
- [Ant Design `ant-design` Skill 原始文件](https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/ant-design/SKILL.md)
- [Ant Design `antd` Skill 原始文件](https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/antd/SKILL.md)
- [Ant Design CLI 仓库](https://github.com/ant-design/ant-design-cli)
- [Ant Design CLI 自带 Skill 原始文件](https://raw.githubusercontent.com/ant-design/ant-design-cli/main/skills/antd/SKILL.md)
