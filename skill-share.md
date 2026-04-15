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

Skill 的真正核心，不在于 `SKILL.md` 这几个字符，而在于一种非常适合 Agent 的上下文组织方式：

> **Progressive Disclosure（渐进式披露 / 按需加载）**

### 1. 为什么“全塞上下文”不是好办法

过去 Prompt Engineering 里一个常见做法，是把所有规则、流程、案例、格式要求一次性塞进系统提示词或用户提示里。

短任务还行，复杂任务就会很快出现问题：

- token 成本高
- 上下文污染严重
- 模型注意力分散
- 不相关规则也一直占着上下文

### 2. Skill 的三层加载模型

#### 第一层：元数据层
启动时只暴露：
- `name`
- `description`

作用只有一个：
**告诉模型什么时候该考虑使用这个 Skill。**

#### 第二层：主说明层

当任务匹配时，再加载 `SKILL.md` 正文。

这部分通常包含：
- 核心流程
- 输出标准
- 错误处理
- 资源引用提示

#### 第三层：资源层

再往下按需读取：
- `references/`
- `scripts/`
- `assets/`

这让 Skill 可以很大，但不需要一次性把所有东西灌进上下文。

### 3. 这为什么是架构升级

渐进式披露不是小技巧，而是一种 Agent 架构原则：

- 能力可发现
- 能力可触发
- 信息可按需展开
- 资源可拆分维护
- 工作流可持续演化

这就是 Skill 和“长 Prompt 模板”真正拉开差距的地方。

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

其中：
- `SKILL.md` 是入口
- `references/` 放按需参考资料
- `scripts/` 放可执行脚本
- `assets/` 放模板或静态资源

### 一个最小可用的 `SKILL.md`

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

这个 Skill 很短，但已经具备最重要的几个元素：
- 有明确名字
- 有可触发的描述
- 有清晰的执行步骤
- 没有废话

---

## 五、完整 Skill 示例：以 `ant-design/antd-skill` 为例

如果前面讲的都还偏抽象，那么一个真正好的例子，应该来自真实项目，而不是临时虚构的 toy demo。

这里我想直接用你指定的公开仓库来举例：

- `https://github.com/ant-design/antd-skill`

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

## 六、配套工具链示例：为什么 `ant-design-cli` 是 Skill 生态的理想搭档

如果说 `antd-skill` 体现的是“知识和决策的封装”，那另一个非常值得讲的例子，就是它配套的：

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

这里面每一点都非常关键。

因为一个适合 Agent 使用的 CLI，不只是“功能强”，更重要的是：

- 输出要结构化
- 错误要可程序化处理
- 响应要快
- 最好脱离网络依赖
- 能嵌入 IDE / Agent runtime

`ant-design-cli` 几乎就是照着这些原则设计的。

### 2. 它为什么特别适合和 Skill 配合

仓库里明确提到，这个 CLI 自带一个 `skills/antd/SKILL.md`，并支持通过：

```bash
npx skills add ant-design/ant-design-cli
```

作为 agent skill 安装。

这意味着它不是把 CLI 和 Skill 当两套分离系统，而是把它们视为一体：

- CLI 负责提供可靠、结构化、可执行的底层能力
- Skill 负责教 Agent **何时、如何、按什么顺序** 去使用这些命令

这就是一个特别标准的“Skill + 工具链”组合范式。

### 3. 看几个典型命令，就能理解它为什么适合 Agent

例如：

- `antd list`：列出所有组件和版本
- `antd info Button`：查看 Button 的 props、类型、默认值
- `antd doc Button`：输出完整 markdown 文档
- `antd demo Select basic`：取 demo 源码
- `antd token Button`：查 design token
- `antd semantic Table`：查语义 classNames / styles 结构
- `antd changelog 4.24.0 5.0.0 Select`：做跨版本 API diff
- `antd doctor`：做项目诊断
- `antd usage ./src`：分析项目里的 antd 用法
- `antd lint ./src`：检查 deprecated API、a11y、性能问题
- `antd migrate 4 5 --apply ./src`：生成迁移清单和 agent-ready migration prompt

你会发现，这些命令天然就覆盖了 Agent 最擅长接管的几类任务：

- 查询
- 分析
- 比较
- 检查
- 迁移
- 生成修复路径

### 4. 它怎么和 MCP 打通

`ant-design-cli` 还有一个非常值得强调的点：

它可以通过：

```json
{
  "mcpServers": {
    "antd": {
      "command": "antd",
      "args": ["mcp"]
    }
  }
}
```

作为一个 MCP server 暴露能力。

仓库里提到，它可以暴露多个 tools，比如：

- `antd_list`
- `antd_info`
- `antd_doc`
- `antd_demo`
- `antd_token`
- `antd_semantic`
- `antd_changelog`

也就是说：

- 同一套底层元数据和能力
- 既可以通过 CLI 被 Agent 调用
- 也可以通过 MCP 以原生工具方式接入 IDE / Agent runtime

这是非常典型、也非常现代的一种 Agent 生态设计方式。

### 5. 这个案例最值得我们学的是什么

我觉得这个案例最有启发的一点是：

> **一个优秀的 Skill，不应该只是一份知识说明，它最好能有可执行、可校验、可结构化调用的配套能力面。**

而 `ant-design-cli + antd-skill` 这组组合，恰好把这件事展示得很完整：

- Skill 承接决策与流程
- CLI 承接可执行与结构化输出
- MCP 承接原生工具暴露和 IDE 集成

这三层叠起来，才是真正有工程感的 Agent 能力栈。

---

## 七、再看一个简单 Skill：为什么 `description` 本质上是技能路由 API

很多人第一次写 Skill，注意力会放在正文怎么写。但在实际使用中，最容易被低估、同时又最关键的，往往是 frontmatter 里的 `description`。

为什么？

因为在大多数 Skill 机制里，模型最先看到的，正是这行描述。

换句话说，它不是简单简介，而更接近：

**Skill 的路由规则。**

### 糟糕的写法

```yaml
description: Helps with documents.
```

这种描述几乎没有触发价值。

### 好一点的写法

```yaml
description: Rewrites long-form technical content into concise, readable WeChat-style posts. Use when user asks to summarize, rewrite, polish, or adapt articles for公众号/社媒发布.
```

这类写法至少说清楚了：

- 它做什么
- 什么时候用
- 用户可能会怎么表达需求

这也是为什么我会建议把 `description` 当成：

> **Skill 的触发 API，而不是产品文案。**

---

## 八、Skill 与 MCP 的真正关系：不是二选一，而是上下两层

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

需求是：

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

## 九、OpenClaw、Claude Code、Google ADK：Skill 生态的横向对比

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

## 十、写 Skill 时最容易踩的坑

### 1. description 太泛，导致触发失败或乱触发

如果描述太泛，模型就不知道什么时候该触发；
如果描述太宽，它又会在无关任务里乱触发。

所以 description 的目标不是优雅，而是可路由。

### 2. 把 `SKILL.md` 写成说明书小说

Skill 不是写给人读的长文章，而是给 Agent 执行的操作说明。

如果主文件里充满大量背景解释，往往会导致：
- 重点不突出
- token 成本高
- 模型忽略关键步骤

### 3. 只写“做什么”，不写“怎么判断”

例如只写：
- 先检查质量
- 再修复问题

这对 Agent 来说远远不够。

### 4. 明明可以脚本化，却全靠模型自由发挥

凡是确定性逻辑，都应该优先考虑写进 `scripts/`。

例如：
- 格式校验
- 文件结构检查
- 规则扫描
- 静态分析

### 5. 从来不做触发测试与回归测试

至少应该测试：
- 明显该触发的请求能不能触发
- 换个说法还能不能触发
- 明显不该触发的请求会不会误触发

---

## 十一、为什么我认为 Skill 会成为一种重要的能力资产

### 1. Skill 让个人经验第一次真正可工程化复用

过去很多高手的优势，是隐性的。

他们知道：
- 怎么写一篇好文章
- 怎么做一次好的 review
- 怎么拆一个需求
- 怎么判断风险

Skill 的意义，就是把这些经验第一次压缩成 Agent 能直接使用的形态。

### 2. Skill 让 Agent 从“会回答”走向“会稳定做事”

很多 AI 系统的问题不是不会说，而是不会做。

Skill 的真正价值，不是让模型显得更聪明，而是让它在一个场景里更稳定、更一致、更可预期。

### 3. Skill 让组织知识从文档库变成执行资产

传统知识库能被搜索，但不一定能被执行。

Skill 则把知识从“文档形态”往“执行形态”推进了一步。

未来一个团队真正应该沉淀的不只是文档，而是：

- 文档 + 流程 + 校验 + 模板 + 调用方式

也就是 Skill 这种更接近可执行工作流的形态。

---

## 十二、如果今天开始做 Skill，我会怎么建议团队落地

### 1. 从最痛的重复任务开始

优先找那些你已经重复说过很多遍的话：

- 帮我把这篇文章改成公众号风格
- 帮我总结这个 PR 的风险点
- 帮我整理会议纪要成行动项
- 帮我按我们团队规范写发布说明

### 2. 先做单点高频，不要追求大而全

更好的方式是先做：

- `article-to-wechat`
- `pr-review-summary`
- `meeting-notes-to-actions`
- `design-handoff`

### 3. 先人工跑通，再抽象成 Skill

最稳的方法通常是：
1. 先用普通对话把这类任务做成功几次
2. 记录最有效的流程
3. 抽出稳定步骤和判断标准
4. 再写成 Skill
5. 用真实任务继续迭代

### 4. Skill 与 MCP 要一起设计

如果一个场景需要外部系统参与，那 Skill 和 MCP 最好一起设计。

不要先盲目把一堆工具接进来，再希望模型自己悟出流程。

---

## 十三、结语：Skill 不是 Prompt 的小升级，而是 Agent 工程化的一块关键拼图

如果要用一句话收束全文，我会这样说：

> **Prompt Engineering 解决的是“怎么把一句话说清楚”，而 Skill Engineering 解决的是“怎么把一套工作方法沉淀成 Agent 能长期复用的能力”。**

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

- Ant Design CLI 仓库  
  https://github.com/ant-design/ant-design-cli
