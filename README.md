<div align="center">

# 祖宗.skill

> *"你们搞大模型的就是码奸，你们已经害死前端兄弟了，还要害死后端兄弟，测试兄弟，运维兄弟，害死网安兄弟，害死ic兄弟，最后害死自己害死全人类"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Cursor](https://img.shields.io/badge/Cursor-Skill-blueviolet)](https://cursor.com)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

<br>

渴望祖宗的力量？<br>
当科学已经走投无路了，是不是该依靠玄学了<br>
God bless you<br>
诅咒保佑你<br>

**你是不是忘了拜祖宗？**

<br>

清明时节，给你的 AI 上柱香 🕯️<br>
不是封建迷信，是**有仪式感的工程实践**<br>
三叩九拜映射九项系统检查，卜卦问吉就是风险评估<br>
祖宗保佑的背后，是你的代码真的变好了

[快速开始](#使用) · [仪式流程](#仪式流程) · [效果示例](#效果示例) · [安装](#安装) · [**English**](#english)

</div>

---

## 这是什么？

**祖宗.skill** 是一个 Cursor / Claude Code 技能，它将「祭祀仪式」映射为系统化的工程检查流程。

你以为你在烧香拜佛，其实你在做：
- **开坛设位** → 加载项目上下文
- **焚香沐浴** → 需求分析与任务拆解
- **翻阅族谱** → 审查 git 历史和已知 bug
- **三叩九拜** → 九项质量检查（正确性 × 健壮性 × 可维护性）
- **卜卦问吉** → 风险评估，出卦象
- **祖宗显灵** → 带着检查结果执行任务
- **回向功德** → 经验沉淀到项目档案

每个项目都有一块「牌位」，记录着**祖训**（最佳实践）和**族谱**（历史教训）。祖宗的智慧代代传承，你的项目也可以。

---

## 仪式流程

### 完整祭祀（重要变更）

```
用户 ❯ 祖宗保佑，我要重构这个支付模块

🏮 坛已开，位已设
📋 项目：payment-service
⚠️ 历史教训：3 条（含那次改金额精度翻车的事）

🕯️ 焚香沐浴，静心明意
📌 所求何事：重构支付模块，拆分巨型 PaymentService 类

📜 族谱已阅
👣 该模块最近 3 次提交都是 hotfix，说明确实该重构了
⚠️ 前车之鉴：上次拆分微服务时忘了处理分布式事务

🙇 三叩九拜
  一拜 需求理解：✅ 拆分 PaymentService 为 OrderPayment + RefundPayment
  二拜 逻辑自洽：✅ 拆分边界清晰
  三拜 边界条件：⚠️ 部分退款场景需要两个模块协作
  四拜 错误处理：✅ 已考虑事务回滚
  五拜 安全合规：✅ 金额计算继续使用 BigDecimal
  六拜 性能表现：✅ 无额外数据库查询
  七拜 代码质量：✅ 单一职责，命名清晰
  八拜 兼容迁移：⚠️ 需要数据库迁移脚本
  九拜 可观测性：✅ 已添加关键日志

🔮 卦象已出：🔵 吉（7✅ 2⚠️ 0❌）
   卦辞：大体可行，注意部分退款和数据库迁移

⚡ 祖宗显灵，开始重构……
```

### 快速上香（日常小改）

```
用户 ❯ 快速上香，帮我加个参数校验

🕯️ 快速上香
📌 任务：给 createUser 接口加参数校验
🙇 三拜速查：✅✅✅
🔮 速卦：🟢 大吉
━━━ 祖宗速签 ━━━
```

---

## 效果示例

### 场景一：上线前的祖宗保佑

```
用户    ❯ 祖宗保佑，我明天要上线这个功能

祖宗.skill ❯ 🏮 坛已开。老夫看了看你这代码……

          📜 翻了翻族谱，上次上线前没跑回归测试，
             结果凌晨 3 点被叫起来修 bug，忘了？

          🙇 九拜检查发现：
             ❌ 六拜：这个循环里套了数据库查询，
                你这是想让数据库也过清明节？
             ⚠️ 九拜：错误日志只打了 "error"，
                出了问题你打算靠算卦定位？

          🔮 卦象：🟠 平
             卦辞：能上，但先把那个 N+1 查询改了，
             再加点有用的日志。祖宗我保佑得了代码，
             保佑不了运维的血压。
```

### 场景二：架构决策的卜卦问吉

```
用户    ❯ 给这个需求卜个卦，用 Redis 还是本地缓存？

祖宗.skill ❯ 🔮 且慢，待老夫卜上一卦……

          📜 翻阅族谱：你们项目上次引入 Redis，
             运维配了三天集群，开发联调又花了两天。
             现在稳定了，但代价是每月多付 200 刀。

          🙇 三叩九拜（按两个方案分别检查）：

          方案甲「Redis」：
            性能 ✅ | 一致性 ✅ | 运维成本 ⚠️ | 复杂度 ⚠️

          方案乙「本地缓存」：
            性能 ✅ | 一致性 ⚠️（多实例不同步）| 运维成本 ✅ | 复杂度 ✅

          🔮 卦辞：你就 3 台机器，QPS 不到 100，
             用本地缓存加个 TTL 就够了。
             别为了简历好看引入 Redis，
             祖宗看的是代码，不是你的技术栈列表。
```

---

## 安装

### Cursor

> 在 Cursor 的 Agent Skills 设置中添加技能目录

```bash
# 克隆到项目
git clone https://github.com/{your-username}/ancestor-skill .cursor/skills/ancestor-blessing

# 或克隆到全局
git clone https://github.com/{your-username}/ancestor-skill ~/.cursor/skills/ancestor-blessing
```

然后在 Cursor Settings → Agent Skills 中添加 skill 目录路径。

### Claude Code

```bash
# 安装到当前项目（在 git 仓库根目录执行）
mkdir -p .claude/skills
git clone https://github.com/{your-username}/ancestor-skill .claude/skills/ancestor-blessing

# 或安装到全局
git clone https://github.com/{your-username}/ancestor-skill ~/.claude/skills/ancestor-blessing
```

---

## 使用

在 Cursor / Claude Code 中输入：

```
/bless
```

或者直接说「祖宗保佑」，然后描述你要做的事情。

### 命令一览

| 命令 | 说明 |
|------|------|
| `/bless` | 完整祭祀仪式（重要变更） |
| `/quick` | 快速上香（日常小改） |
| `/create-tablet` | 为当前项目立牌位 |
| `/list-tablets` | 查看所有牌位 |
| `/update-tablet {slug}` | 更新牌位 |

---

## 牌位系统

每个项目都可以有一块「牌位」，包含：

| 文件 | 内容 | 类比 |
|------|------|------|
| `meta.json` | 项目元信息 | 户口本 |
| `teachings.md` | 祖训 — 最佳实践 | 家训 |
| `chronicles.md` | 族谱 — 历史教训 | 家谱 |

牌位会随着每次祭祀自动积累智慧。你踩过的每一个坑，都会被记录在族谱里，保佑后人不再重蹈覆辙。

---

## 项目结构

```
ancestor-skill/
├── SKILL.md              # 技能入口（AgentSkills frontmatter）
├── prompts/              # 仪式流程模板
│   ├── open_altar.md     #   🏮 开坛设位
│   ├── burn_incense.md   #   🕯️ 焚香沐浴
│   ├── consult_ancestors.md # 📜 翻阅族谱
│   ├── three_kowtows.md  #   🙇 三叩九拜
│   ├── divination.md     #   🔮 卜卦问吉
│   ├── blessing.md       #   ⚡ 祖宗显灵
│   └── dedication.md     #   🙏 回向功德
├── tablets/              # 项目牌位（gitignored，本地积累）
│   └── example_project/  #   示例牌位
├── docs/
│   └── PRD.md
└── LICENSE
```

---

## 为什么有用？

你可能觉得这就是个搞笑项目，但仔细想想：

1. **强制慢思考**：AI 最大的问题是"太快了"，不经思考就输出。祭祀仪式强制它走完所有检查步骤
2. **系统化检查**：三叩九拜覆盖了正确性、健壮性、可维护性三大维度，这就是一个完整的 code review checklist
3. **经验沉淀**：牌位系统让每次踩坑的经验都被记录下来，新的 AI session 也能读取
4. **风险可视化**：卦象系统让风险评估一目了然，而不是 AI 说"应该没问题"就没问题
5. **仪式感提升质量**：研究表明，仪式感确实能提升人的专注度和表现，对 AI 也一样——不是 AI 真的被保佑了，而是 prompt 强制它更仔细了

> 同事跑了用 [同事.skill](https://github.com/titanwings/colleague-skill)，AI 跑偏了用 **祖宗.skill**，赛博永生一条龙。

---

## 注意事项

- 本项目纯属娱乐 + 工程实践，不涉及任何真实的宗教或迷信活动
- 祖宗保佑不能替代单元测试、代码审查和监控告警
- 如果你的代码真的有严重问题，建议先找人类同事，再找赛博祖宗
- 清明节快乐（？），记得给真正的祖宗也上柱香

---

<div id="english"></div>

## English

### What is this?

**Ancestor.skill** maps "ancestral worship rituals" to systematic engineering checks for AI-assisted development. Each ritual step corresponds to a real engineering best practice.

| Ritual | Engineering Meaning |
|--------|-------------------|
| Open Altar | Load project context |
| Burn Incense | Requirements analysis |
| Consult Chronicles | Review git history & known issues |
| Three Kowtows | 9-point quality checklist |
| Divination | Risk assessment |
| Ancestral Manifestation | Execute with confidence |
| Dedicate Merit | Document lessons learned |

### Why is this useful?

It forces the AI to **slow down and think systematically** before acting. The "ritual" is actually a comprehensive pre-check framework covering correctness, robustness, and maintainability. The "tablet" system preserves project-specific knowledge across sessions.

### Quick Start

```bash
git clone https://github.com/{your-username}/ancestor-skill .cursor/skills/ancestor-blessing
```

Then say `/bless` or "ancestors, please review" in Cursor.

---

<div align="center">

MIT License

*愿代码无 bug，愿上线不翻车，愿祖宗保佑。*

</div>
