# Skill 分享：从 Prompt 到 Agent 能力资产

> 技术分享 PPT 大纲版
> 适合 15~30 分钟内部分享 / 社区分享 / 直播分享

---

## 封面页

**标题**
Skill 分享：从 Prompt 到 Agent 能力资产

**副标题**
为什么 Skill 会成为 Agent 时代最值得沉淀的工作流载体

**可讲点**
- 今天不讲玄学，重点讲 Skill 的本质、设计方法和落地实践
- 目标：听完后大家知道 Skill 是什么、为什么重要、怎么开始做

---

## 第 1 页：先抛结论

**标题**
一句话理解 Skill

**核心要点**
- Skill = 把“某类事情该怎么专业完成”封装成 AI 可复用能力模块
- 它不只是 Prompt 模板，而是流程、知识、脚本、模板的组织方式
- 它解决的是：**如何让 Agent 稳定地做成事**

**可讲金句**
- Prompt 是一次性交代，Skill 是可复用方法论
- MCP 决定 AI 能做什么，Skill 决定 AI 应该怎么做

---

## 第 2 页：为什么 Skill 会火起来

**标题**
Prompt、Rules、Tools 之间，还缺了一层

**核心要点**
- Prompt：每次都要重新说，重复成本高
- Rules / Memory：适合长期约束，不适合复杂 SOP
- Tools / MCP：解决“能不能调用”，不解决“应该怎么组合使用”
- Skill：把经验和流程沉淀下来，让 AI 自动复用

**可讲案例**
- 以前每次都说：总结 → 翻译 → 改公众号风格 → 加标题 → 输出 Markdown
- 有了 Skill 之后，只需要触发一个内容改写 Skill

---

## 第 3 页：Skill 到底是什么结构

**标题**
Skill 的最小结构非常简单

**核心要点**
- 一个 Skill 本质上是一个文件夹
- 核心文件是 `SKILL.md`
- 复杂 Skill 可以增加：
  - `references/`
  - `scripts/`
  - `assets/`

**示意结构**
```text
my-skill/
├── SKILL.md
├── references/
├── scripts/
└── assets/
```

**可讲点**
- Skill 不是一个大模型插件黑盒，本质上是透明、可读、可维护的目录结构

---

## 第 4 页：Skill 最核心的设计哲学

**标题**
按需加载 + 渐进式披露（Progressive Disclosure）

**核心要点**
- L1：只加载 name + description，用来判断是否触发
- L2：任务匹配后，再加载 `SKILL.md` 主体
- L3：执行中按需读取 `references/`、`scripts/`、`assets/`
- 这样可以大幅减少无效上下文占用

**关键价值**
- 降低 token 消耗
- 降低上下文污染
- 让 Skill 具备可扩展性
- 比“超长系统提示词”更优雅

**引用观点（可口播）**
- Anthropic 和 Google 都把 progressive disclosure 当作 Skill 架构的核心原则

---

## 第 5 页：Skill 和 Prompt 的本质区别

**标题**
不是“更长 Prompt”，而是“更好的上下文工程”

**核心要点**
- Prompt 是一次性、会话级、人工重复输入
- Skill 是模块化、可共享、可自动触发
- Prompt 更像临时口头交代
- Skill 更像岗位培训手册 + SOP + 检查清单

**可讲比喻**
- Prompt：你每次都重新教实习生
- Skill：你把培训材料整理成标准包，以后重复使用

---

## 第 6 页：Skill 和 MCP 的关系

**标题**
MCP 给能力，Skill 给方法

**核心要点**
- MCP / Tools：连接外部系统、API、数据库、浏览器、文件系统
- Skill：告诉 Agent 在什么场景下按什么流程去用这些能力
- 没有 Skill，Agent 常常“会调用工具，但不会稳定完成流程”
- Skill + MCP 才是完整工作流

**一句话总结**
- MCP 是手脚
- Skill 是方法论

---

## 第 7 页：什么任务最适合 Skill 化

**标题**
不是所有任务都值得做 Skill

**核心要点**
最适合做 Skill 的任务通常具备三个特征：
- 高频重复
- 有相对稳定的流程
- 普通 Prompt 容易失控或结果不稳定

**典型场景**
- 内容生成与改写
- 代码审查 / PR 总结
- 研究与情报分析
- 冲刺规划 / 任务拆解
- 项目初始化 / 发布前检查
- 合规、法务、安全审计

---

## 第 8 页：Skill 的五种经典设计模式

**标题**
做 Skill，不只是写说明书

**核心要点**
1. **顺序工作流模式**：固定步骤、强依赖顺序
2. **多系统编排模式**：跨多个 MCP / 工具串联
3. **迭代优化模式**：初稿 → 质检 → 修正 → 再校验
4. **决策树路由模式**：根据条件走不同路径
5. **领域知识增强模式**：把行业规则嵌入执行流程

**可讲点**
- Google 的技能设计实践里，对 checklist / pipeline / generator / reviewer / inversion 等模式也做了明确总结

---

## 第 9 页：以内容创作为例，Skill 怎么发挥价值

**标题**
一个“技术文章转公众号”Skill 会长什么样

**流程拆解**
- 读取原文
- 提取核心观点与结构
- 改写成公众号语气
- 增加标题、导语、小结
- 输出 Markdown

**为什么值得做成 Skill**
- 重复率高
- 审美和风格要求稳定
- 每次手写 Prompt 很浪费
- 可以持续迭代成团队资产

---

## 第 10 页：好的 Skill，最关键先写好 description

**标题**
Skill 触发率，往往由这一行决定

**核心要点**
一个好的 `description` 至少要说清：
- 做什么
- 什么时候用
- 用户可能会怎么说

**反例**
```yaml
description: Helps with documents.
```

**正例**
```yaml
description: Rewrites long-form technical content into concise, readable WeChat-style posts. Use when user asks to summarize, rewrite, polish, or adapt articles for公众号/社媒发布.
```

**可讲点**
- `description` 是触发 API，不是文案修辞比赛

---

## 第 11 页：写好 Skill 的方法论

**标题**
先有场景，再有 Skill

**核心步骤**
1. 先找 2~3 个真实任务样本
2. 拆出重复步骤和关键判断
3. 把稳定流程写进 `SKILL.md`
4. 把细节资料移到 `references/`
5. 把确定性逻辑移到 `scripts/`
6. 用真实任务反复测试和迭代

**可讲点**
- 好 Skill 不是脑补出来的，而是从真实工作流里提炼出来的

---

## 第 12 页：Skill 编写的最佳实践

**标题**
少写废话，多写执行约束

**核心要点**
- 保持简洁：只写模型原本不知道、但执行必须知道的内容
- 用动作化语言：明确步骤，而不是泛泛而谈
- 保持 SKILL.md 精瘦：细节放 references
- 能写脚本就别全靠语言：确定性逻辑交给代码
- 给出错误处理：失败时怎么退、怎么查、怎么补救
- 做触发测试：既测“该触发”，也测“不该触发”

---

## 第 13 页：最常见的坑

**标题**
为什么很多 Skill 看起来不错，用起来却很差

**核心要点**
- description 太泛，导致触发不到或乱触发
- SKILL.md 过长，重点被淹没
- 只写“做什么”，不写“怎么判断”
- 把本应脚本化的逻辑全交给模型自由发挥
- 从不做真实任务回归测试

**可讲总结**
- Skill 不是写完就结束，而是需要在使用中持续迭代

---

## 第 14 页：从官方趋势看，Skill 不只是某家私货

**标题**
Skill 正在走向开放标准和跨平台兼容

**核心要点**
- Anthropic 已推动 Agent Skills 作为开放标准
- Google ADK 已明确支持 skill 化和 SkillToolset
- OpenClaw 已兼容 AgentSkills 目录结构
- Cursor、Claude Code、Gemini CLI、OpenClaw 等都在向类似格式靠拢

**结论**
- Skill 正在从“高手私藏 Prompt”变成“跨平台流通的能力资产”

---

## 第 15 页：OpenClaw 视角下的 Skill

**标题**
在 OpenClaw 里，Skill 不只是说明书，也是能力分发机制

**核心要点**
- OpenClaw 使用 AgentSkills 兼容格式
- Skill 可以放在 workspace / personal / shared / plugin 等多个层级
- 有明确优先级和 gating 机制
- 可根据操作系统、依赖、配置、环境变量进行过滤
- 适合在个人、团队、插件市场中分发

**可讲价值**
- Skill 在 OpenClaw 里不是演示功能，而是真正的工程化能力组织方式

---

## 第 16 页：Skill 生态已经出现了什么

**标题**
从“会写”到“会发现、会安装、会复用”

**生态层次**
- 官方 / 半官方技能仓库
- GitHub awesome 列表
- 技能市场与聚合站
- Skill 创建器 / 元技能
- 厂商垂直技能仓库

**可讲点**
- 这意味着未来团队竞争，不只是模型能力竞争，也是 Skill 资产竞争

---

## 第 17 页：我对 Skill 的三个判断

**标题**
为什么它值得团队现在就开始做

**判断 1**
Skill 会成为个人经验产品化的最轻载体

**判断 2**
Skill 会推动 Agent 从“会回答”走向“会稳定做事”

**判断 3**
Skill 会成为组织级工作流沉淀的新形态

**一句话总结**
- 未来有价值的，不只是接了多少模型，而是谁把自己的工作方法沉淀成了 AI 可调用资产

---

## 第 18 页：落地建议

**标题**
如果现在开始做 Skill，第一步该做什么

**建议路径**
- 从自己最痛的重复任务开始
- 先做单点高频，不要一上来大而全
- 先人工跑通 3~5 次，再抽象成 Skill
- 先在小范围使用，再沉淀到团队级
- Skill + MCP 一起设计，不要割裂看

**建议优先级**
1. 内容改写类
2. 代码工作流类
3. 文档与汇报类
4. 研究分析类
5. 业务系统协同类

---

## 第 19 页：结束页

**标题**
最后一句话

**结束语**
- Prompt Engineering 解决的是“怎么说”
- Skill Engineering 解决的是“怎么把方法变成可复用能力”

**收尾金句**
- Skill 不是 Prompt 的小升级，而是 Agent 工程化落地的一块关键拼图

---

## 附录页：可补充展示的参考链接

- Anthropic: Equipping agents for the real world with Agent Skills
- Google: Developer’s Guide to Building ADK Agents with Skills
- OpenClaw Docs: Skills / Creating Skills
- agentskills.io 规范站点
- awesome-agent-skills 资源仓库

---

## 演讲者备注（备选）

### 如果你要压缩成 15 分钟
重点讲：
- 第 1 / 2 / 4 / 6 / 8 / 10 / 17 / 18 页

### 如果你要扩展成 30 分钟
可以增加：
- Skill 示例实操页
- 一个真实 `SKILL.md` 拆解页
- 与 MCP 的完整联动案例页
- OpenClaw / Claude Code / Google ADK 的横向对比页
