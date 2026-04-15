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
### 2. Rules / Memory：长期约束模型的行为或偏好
### 3. Tools / MCP：让模型拥有能力接入
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
#### 第二层：主说明层
#### 第三层：资源层

### 3. 这为什么是架构升级
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
#### 第二，它采用单一 `SKILL.md` 保持核心简洁
#### 第三，它和工具链能力形成了天然闭环

---

## 六、真实 `SKILL.md` 拆解：以 `ant-design/antd-skill` 为例逐段分析

这里我们直接看：

- `https://raw.githubusercontent.com/ant-design/antd-skill/main/skills/ant-design/SKILL.md`

### 1. Frontmatter：不是元数据装饰，而是触发与边界声明
### 2. S - Scope：先划边界，再谈能力
### 3. Default assumptions：把默认前提显式化
### 4. Mandatory rules：这里才是 Skill 最有力量的地方
### 5. P - Process：把工作流压缩成可复用的决策路径
### 6. O - Output：提前规定输出结构
### 7. 为什么这个 `SKILL.md` 是一个很好的示范

它体现了几个成熟特征：
- 先划边界，再给流程
- 强依赖权威来源
- 强约束工具使用方式
- 把“查询 → 决策 → 验证”串成闭环
- 让 Skill 承担规范化执行，而不是泛泛介绍

---

## 七、配套工具链示例：为什么 `ant-design-cli` 是 Skill 生态的理想搭档

- `https://github.com/ant-design/ant-design-cli`

这个项目非常适合拿来说明一件事：

> **Skill 最强的地方，从来不是独立存在，而是和工具、CLI、MCP 一起构成完整的 Agent 工作流。**

### 1. `ant-design-cli` 做的事情非常 Agent 友好
### 2. 它为什么特别适合和 Skill 配合
### 3. 看几个典型命令，就能理解它为什么适合 Agent

---

## 八、再拆一个真实 `SKILL.md`：`ant-design-cli` 自带 Skill 为什么像一份操作手册

这里看：

- `https://raw.githubusercontent.com/ant-design/ant-design-cli/main/skills/antd/SKILL.md`

### 1. 它的 frontmatter 更强烈地绑定了使用触发条件
### 2. Setup 段落体现了“Skill 负责把工具准备好”
### 3. Scenarios 段落像一组预置工作流模板
### 4. “Auto-report CLI issues” 这段特别有代表性
### 5. 这个 Skill 的价值，不只是命令清单，而是“行为标准化”

---

## 九、Skill / CLI / MCP：三层架构应该怎么理解

### 1. 第一层：Skill 层 —— 决策与工作流层
### 2. 第二层：CLI / Script 层 —— 可执行能力层
### 3. 第三层：MCP 层 —— 原生工具暴露与系统接入层
### 4. 三层是怎么协同工作的
### 5. 为什么这个架构视角很重要

真正成熟的方案通常是三层协同：

- **Skill** 负责工作流与决策
- **CLI / Script** 负责执行与校验
- **MCP** 负责标准化接入与工具暴露

---

## 十、Skill 与 MCP 的真正关系：不是二选一，而是上下两层

- MCP 给 Agent 提供“器官”
- Skill 给 Agent 提供“神经回路”

---

## 十一、OpenClaw、Claude Code、Google ADK：Skill 生态的横向对比

### 1. Claude Code：Skill 生态的标准化推动者之一
### 2. Google ADK：更强调 SkillToolset 和程序化组装
### 3. OpenClaw：更强调真实运行环境、技能分发与本地工作流落地

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

### 1. description 太泛，导致触发失败或乱触发
### 2. 把 `SKILL.md` 写成说明书小说
### 3. 只写“做什么”，不写“怎么判断”
### 4. 明明可以脚本化，却全靠模型自由发挥
### 5. 从来不做触发测试与回归测试

---

## 十四、为什么我认为 Skill 会成为一种重要的能力资产

### 1. Skill 让个人经验第一次真正可工程化复用
### 2. Skill 让 Agent 从“会回答”走向“会稳定做事”
### 3. Skill 让组织知识从文档库变成执行资产

---

## 十五、如果今天开始做 Skill，我会怎么建议团队落地

### 1. 从最痛的重复任务开始
### 2. 先做单点高频，不要追求大而全
### 3. 先人工跑通，再抽象成 Skill
### 4. Skill 与 MCP 要一起设计

---

## 十六、结语：Skill 不是 Prompt 的小升级，而是 Agent 工程化的一块关键拼图

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
