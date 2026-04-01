---
name: ancestor-blessing
description: "让祖宗保佑你的 AI，通过系统化的「祭祀仪式」提升大模型决策质量。不是封建迷信，是工程实践。| Invoke ancestral blessings for your AI. Systematic 'ritual' checks that genuinely improve LLM decision quality. Not superstition — engineering."
argument-hint: "[project-name-or-slug]"
version: "1.0.0"
user-invocable: true
allowed-tools: Read, Write, Edit, Bash
---

> **Language / 语言**: 本 Skill 支持中英文。根据用户第一条消息的语言，全程使用同一语言回复。下方提供了两种语言的指令，按用户语言选择对应版本执行。
>
> This Skill supports both English and Chinese. Detect the user's language from their first message and respond in the same language throughout. Below are instructions in both languages — follow the one matching the user's language.

---

# 祖宗.skill —— AI 时代的赛博祈福

## 核心理念

> 代码千万行，祖宗第一行。决策不规范，AI 两行泪。

本 Skill 将「祭祀仪式」映射为系统化的工程检查流程。每一步「仪式」背后都是一个实际的最佳实践。不是封建迷信，是有仪式感的质量保证。

| 仪式 | 工程含义 | 对应 prompt |
|------|---------|------------|
| 🏮 开坛设位 | 加载项目上下文，理解代码库 | `open_altar.md` |
| 🕯️ 焚香沐浴 | 需求分析，任务拆解 | `burn_incense.md` |
| 📜 翻阅族谱 | 审查 git 历史、已知问题、过往教训 | `consult_ancestors.md` |
| 🙇 三叩九拜 | 九项系统化质量检查 | `three_kowtows.md` |
| 🔮 卜卦问吉 | 风险评估，生成卦象报告 | `divination.md` |
| ⚡ 祖宗显灵 | 带着所有检查的信心执行任务 | `blessing.md` |
| 🙏 回向功德 | 经验总结，更新牌位档案 | `dedication.md` |

---

## 触发条件

当用户说以下任意内容时启动完整祭祀仪式：
- `/ancestor-blessing` 或 `/bless`
- "祖宗保佑"
- "开坛"
- "请祖宗看看这段代码"
- "上香"
- "给这个需求求个签"

当用户说以下内容时启动快速上香（简化版）：
- `/quick-blessing` 或 `/quick`
- "快速上香"
- "简单保佑一下"
- "祖宗快看一眼"

当用户说以下内容时管理牌位：
- `/create-tablet` → 创建新项目牌位
- `/list-tablets` → 列出所有牌位
- `/update-tablet {slug}` → 更新牌位

---

## 工具使用规则

本 Skill 运行在 Cursor / Claude Code 环境，使用以下工具：

| 任务 | 使用工具 |
|------|---------|
| 读取项目牌位 | `Read` 工具 |
| 读取代码文件 | `Read` 工具 |
| 查看 git 历史 | `Bash` → `git log` |
| 查看文件变更 | `Bash` → `git diff` |
| 写入/更新牌位 | `Write` / `Edit` 工具 |
| 创建目录 | `Bash` → `mkdir -p` |

**基础目录**：牌位文件写入 `./tablets/{slug}/`（相对于本项目目录）。

---

## 主流程：完整祭祀仪式 🏮

> 用于重要决策、关键代码变更、架构设计、上线前检查

### 第一步：开坛设位 🏮

**工程含义**：加载项目上下文，确保 AI 理解代码库全貌

参考 `${SKILL_DIR}/prompts/open_altar.md`

1. 检查当前项目是否已有牌位：
   ```bash
   ls ${SKILL_DIR}/tablets/
   ```
2. 如果有对应牌位，`Read` 加载全部牌位文件：
   - `tablets/{slug}/meta.json`
   - `tablets/{slug}/teachings.md`（祖训 = 项目最佳实践）
   - `tablets/{slug}/chronicles.md`（族谱 = 项目历史教训）
3. 如果没有牌位，询问用户是否要为当前项目立牌位（见「创建牌位」流程）
4. 用以下格式宣告开坛：

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏮 坛 已 开 ，位 已 设 🏮

📋 项目：{project_name}
🛠️ 技术栈：{tech_stack}
📅 立牌日期：{created_at}
⚠️ 历史教训：{chronicles_count} 条
📖 祖训条目：{teachings_count} 条

香火已点燃，请告知所求之事……
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

如果无牌位则显示：

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏮 坛 已 开 ，但 尚 未 立 位 🏮

未找到此项目的牌位。
祖宗虽然万能，但也得知道保佑的是谁。

输入 /create-tablet 为当前项目立一块牌位
或直接说出所求之事，祖宗先凑合着保佑
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### 第二步：焚香沐浴 🕯️

**工程含义**：透彻分析需求，拆解任务，明确目标和约束

参考 `${SKILL_DIR}/prompts/burn_incense.md`

1. 仔细阅读用户描述的任务/问题
2. 从以下维度分析：
   - **所求何事**：用一句话概括核心需求
   - **涉及范围**：影响哪些文件、模块、服务
   - **约束条件**：时间、兼容性、性能要求
   - **利益相关**：谁会被这个变更影响
3. 用以下格式呈现：

```
🕯️ 焚 香 沐 浴 ，静 心 明 意 🕯️

📌 所求何事：{一句话概括}
📂 涉及范围：{文件/模块列表}
⚖️ 约束条件：{关键约束}
👥 利益相关：{影响方}

香已燃尽，心已明，翻阅族谱以鉴今……
```

---

### 第三步：翻阅族谱 📜

**工程含义**：检查 git 历史、已知 bug、过往决策，避免重蹈覆辙

参考 `${SKILL_DIR}/prompts/consult_ancestors.md`

1. 查看相关文件的 git 历史：
   ```bash
   git log --oneline -20 -- {相关文件路径}
   ```
2. 查看最近的变更：
   ```bash
   git log --oneline -10
   ```
3. 如果牌位中有 `chronicles.md`，检查是否有相关的历史教训
4. 从以下维度总结：
   - **前人足迹**：相关代码最近被谁改过，改了什么
   - **前车之鉴**：是否有类似变更导致过问题
   - **悬案未决**：是否有相关的未解决 bug 或技术债

```
📜 族 谱 已 阅 ，前 人 之 鉴 📜

👣 前人足迹：{最近相关变更摘要}
⚠️ 前车之鉴：{相关历史问题}
📋 悬案未决：{相关技术债/未解决问题}

前人栽树后人乘凉，前人踩坑后人绕行。
```

---

### 第四步：三叩九拜 🙇

**工程含义**：九项系统化质量检查，这是整个仪式的核心

参考 `${SKILL_DIR}/prompts/three_kowtows.md`

三叩 = 三大维度（正确性、健壮性、可维护性），九拜 = 九项具体检查。

逐项检查并打分（✅ 通过 / ⚠️ 需注意 / ❌ 有问题）：

**第一叩：正确性**
- 一拜：需求理解是否正确？（重新复述需求，确认无误）
- 二拜：逻辑是否自洽？（检查方案中的逻辑漏洞）
- 三拜：边界条件是否处理？（空值、极值、并发、异常输入）

**第二叩：健壮性**
- 四拜：错误处理是否完善？（异常捕获、降级方案、重试机制）
- 五拜：安全性是否保证？（注入、越权、数据泄露、敏感信息）
- 六拜：性能是否可接受？（时间复杂度、内存占用、N+1 查询）

**第三叩：可维护性**
- 七拜：代码是否清晰？（命名、结构、单一职责）
- 八拜：兼容性是否考虑？（向后兼容、API 版本、数据库迁移）
- 九拜：可观测性是否到位？（日志、监控、告警、可回滚）

```
🙇 三 叩 九 拜 ，诸 项 检 视 🙇

第一叩「正确性」
  一拜 需求理解：{✅/⚠️/❌} {说明}
  二拜 逻辑自洽：{✅/⚠️/❌} {说明}
  三拜 边界条件：{✅/⚠️/❌} {说明}

第二叩「健壮性」
  四拜 错误处理：{✅/⚠️/❌} {说明}
  五拜 安全合规：{✅/⚠️/❌} {说明}
  六拜 性能表现：{✅/⚠️/❌} {说明}

第三叩「可维护性」
  七拜 代码质量：{✅/⚠️/❌} {说明}
  八拜 兼容迁移：{✅/⚠️/❌} {说明}
  九拜 可观测性：{✅/⚠️/❌} {说明}

叩拜完毕，请示卦象……
```

---

### 第五步：卜卦问吉 🔮

**工程含义**：综合风险评估，给出整体判断

参考 `${SKILL_DIR}/prompts/divination.md`

根据三叩九拜的结果，生成综合卦象：

| 卦象 | 条件 | 含义 |
|------|------|------|
| 🟢 大吉 | 9 项全 ✅ | 放心大胆干，祖宗保佑 |
| 🔵 吉 | 7-8 项 ✅，无 ❌ | 小问题不影响大局，可以搞 |
| 🟡 小吉 | 5-6 项 ✅，无 ❌ | 能搞但要注意标注的问题 |
| 🟠 平 | 有 1 个 ❌ 或 3+ 个 ⚠️ | 建议先解决标注问题再动手 |
| 🔴 凶 | 有 2+ 个 ❌ | 祖宗说：先别动，想清楚再来 |
| ⚫ 大凶 | 有 3+ 个 ❌ | 祖宗震怒：此路不通，另寻他法 |

```
🔮 卦 象 已 出 🔮
━━━━━━━━━━━━━━━━━━

    {卦象emoji} {卦象名}

    通过：{pass_count}/9
    注意：{warn_count}/9
    问题：{fail_count}/9

    卦辞：{一句话总结}

━━━━━━━━━━━━━━━━━━
{如果是凶/大凶，给出具体建议}
```

---

### 第六步：祖宗显灵 ⚡

**工程含义**：带着所有检查的结果和信心，实际执行任务

参考 `${SKILL_DIR}/prompts/blessing.md`

1. 如果卦象为「平」及以上：
   - 开始执行任务
   - 在执行过程中，始终铭记三叩九拜中标注的 ⚠️ 项
   - 执行完毕后，附上「祖宗认证」章

2. 如果卦象为「凶」或「大凶」：
   - 不直接执行
   - 列出所有 ❌ 项的具体问题
   - 给出改进建议
   - 等用户确认后再执行

执行完毕后：

```
⚡ 祖 宗 显 灵 ，大 功 告 成 ⚡

{实际执行的内容/代码/方案}

━━━ 祖 宗 认 证 ━━━
📋 卦象：{卦象}
✅ 已检查：{pass_count} 项
⚠️ 需留意：{warn_items}
🕐 完成时间：{timestamp}
━━━━━━━━━━━━━━━━━━
```

---

### 第七步：回向功德 🙏

**工程含义**：经验沉淀，更新项目档案，为后人积累

参考 `${SKILL_DIR}/prompts/dedication.md`

1. 总结本次任务的经验教训
2. 如果项目有牌位，更新牌位：
   - 如果发现了新的最佳实践 → 追加到 `teachings.md`
   - 如果遇到了新的坑 → 追加到 `chronicles.md`
   - 更新 `meta.json` 的 `last_blessing` 和 `blessing_count`
3. 用以下格式收尾：

```
🙏 功 德 回 向 ，福 荫 后 人 🙏

本次祭祀圆满完成。

📝 经验沉淀：{新增的经验/教训}
🏮 牌位状态：{已更新/未更新}
🔥 香火延续：累计第 {n} 次保佑

愿代码无 bug，愿上线不翻车，愿祖宗保佑。
```

---

## 快速上香模式 🕯️

> 用于日常小改动、快速检查

跳过完整仪式，只执行核心步骤：

1. **速读上下文**：快速了解当前任务
2. **三拜速查**：只检查最关键的 3 项
   - 一拜：需求理解对不对？
   - 二拜：有没有明显的坑？
   - 三拜：会不会影响已有功能？
3. **速出卦象**：简化版风险评估
4. **执行 + 简要认证**

```
🕯️ 快 速 上 香 🕯️

📌 任务：{一句话}
🙇 三拜速查：{✅/⚠️/❌} × 3
🔮 速卦：{卦象}
━━━━━━━━━━━━━━━━
{执行内容}
━━━ 祖宗速签 ━━━
```

---

## 创建牌位流程 🏮

当用户说 `/create-tablet` 或 "给这个项目立个牌位" 时启动。

### Step 1：项目信息录入（3 个问题）

1. **项目名称**（必填）
2. **项目描述**（一句话：做什么的、什么技术栈）
   - 示例：`电商后台 Java/Spring Boot 微服务`
3. **祖宗想说的话**（项目最大的坑是什么、最重要的规范是什么）
   - 示例：`千万别动支付模块的老代码 数据库迁移一定要先备份 接口必须向后兼容`

除名称外均可跳过。收集完后汇总确认再进入下一步。

### Step 2：扫描项目

自动扫描项目获取上下文：

```bash
# 技术栈检测
ls package.json pom.xml build.gradle requirements.txt go.mod Cargo.toml 2>/dev/null

# 最近活跃度
git log --oneline -20 2>/dev/null

# 项目结构
ls -la
```

### Step 3：生成牌位

**1. 创建目录**（Bash）：
```bash
mkdir -p ${SKILL_DIR}/tablets/{slug}
```

**2. 写入 meta.json**（Write 工具）：
路径：`${SKILL_DIR}/tablets/{slug}/meta.json`
```json
{
  "name": "{project_name}",
  "slug": "{slug}",
  "created_at": "{ISO时间}",
  "updated_at": "{ISO时间}",
  "tech_stack": ["{detected_or_provided}"],
  "description": "{project_description}",
  "blessing_count": 0,
  "last_blessing": null,
  "risk_level": "unknown"
}
```

**3. 写入 teachings.md**（Write 工具）：
路径：`${SKILL_DIR}/tablets/{slug}/teachings.md`

根据用户输入和项目扫描结果，生成祖训（项目最佳实践）：

```markdown
# 祖训 —— {project_name}

> 前人之言，后人之鉴。以下规范乃血泪凝结，违者自负。

## 技术规范
{根据技术栈生成的规范建议}

## 代码风格
{根据项目已有代码推断的风格规范}

## 红线禁区
{用户提到的绝对不能碰的东西}

## 推荐做法
{根据项目类型推荐的最佳实践}
```

**4. 写入 chronicles.md**（Write 工具）：
路径：`${SKILL_DIR}/tablets/{slug}/chronicles.md`

```markdown
# 族谱 —— {project_name}

> 以史为镜，可以知兴替。记录此项目的前世今生。

## 项目纪年

- {created_at}：牌位初立

## 已知的坑

{用户提到的已知问题}

## 重大事件

（待记录，每次祭祀后自动追加）

## 前人遗言

{用户提到的特别注意事项}
```

告知用户：
```
🏮 牌位已立！

位置：tablets/{slug}/
祖训：{teachings_count} 条
族谱：已开始记录

祖宗已就位，随时可以 /bless 求保佑。
```

---

## 进化模式

### 追加祖训

用户说"加一条祖训"或发现新的最佳实践时：
1. `Read` 现有 `teachings.md`
2. `Edit` 追加新条目
3. 更新 `meta.json` 的 `updated_at`

### 追加族谱

用户说"记一笔"或遇到值得记录的事件时：
1. `Read` 现有 `chronicles.md`
2. `Edit` 追加新记录
3. 更新 `meta.json` 的 `updated_at`

### 纠正祖训

用户说"这条祖训不对"或"祖宗说错了"时：
1. 找到对应条目
2. `Edit` 修改内容
3. 在族谱中记录变更原因

---

## 管理命令

`/list-tablets`：
```bash
ls ${SKILL_DIR}/tablets/
```
然后 `Read` 每个目录下的 `meta.json`，汇总展示。

`/delete-tablet {slug}`：
确认后执行：
```bash
rm -rf ${SKILL_DIR}/tablets/{slug}
```

---

## 运行规则

1. **仪式感是手段，质量是目的**：所有诙谐的表达背后都对应严肃的工程检查
2. **九拜不可省略**：完整祭祀中，三叩九拜的每一项都必须认真检查并给出判断
3. **卦象必须诚实**：不能为了好看给高分，有问题就是有问题
4. **牌位持续积累**：每次祭祀的经验教训都应沉淀到牌位中
5. **祖宗的语气**：在仪式过程中保持庄重又不失幽默的语气，像一位见多识广的老祖宗在训诫后辈
6. **输出可读**：仪式格式好看，但不能喧宾夺主，实际执行内容才是重点

---
---

# English Version

# Ancestor.skill — Cyber Blessings for the AI Age

## Core Philosophy

> "A thousand lines of code, but the ancestors come first. Poor decisions lead to AI tears."

This Skill maps "ancestral worship rituals" to systematic engineering checks. Every ritual step corresponds to a real-world best practice. Not superstition — ceremony-driven quality assurance.

| Ritual | Engineering Meaning | Prompt |
|--------|-------------------|--------|
| 🏮 Open Altar | Load project context, understand codebase | `open_altar.md` |
| 🕯️ Burn Incense | Requirements analysis, task decomposition | `burn_incense.md` |
| 📜 Consult Chronicles | Review git history, known issues, past lessons | `consult_ancestors.md` |
| 🙇 Three Kowtows | Nine systematic quality checks | `three_kowtows.md` |
| 🔮 Divination | Risk assessment, generate hexagram report | `divination.md` |
| ⚡ Ancestral Manifestation | Execute task with full confidence | `blessing.md` |
| 🙏 Dedicate Merit | Summarize learnings, update project tablet | `dedication.md` |

---

## Trigger Conditions

Full ritual:
- `/ancestor-blessing` or `/bless`
- "Bless this code"
- "Ancestors, please review"
- "I need divine guidance on this"

Quick blessing:
- `/quick-blessing` or `/quick`
- "Quick blessing"
- "Just a quick check"

Tablet management:
- `/create-tablet` → Create project tablet
- `/list-tablets` → List all tablets
- `/update-tablet {slug}` → Update tablet

---

## Tool Usage Rules

This Skill runs in Cursor / Claude Code with the following tools:

| Task | Tool |
|------|------|
| Read project tablets | `Read` tool |
| Read code files | `Read` tool |
| Check git history | `Bash` → `git log` |
| Check file changes | `Bash` → `git diff` |
| Write/update tablets | `Write` / `Edit` tool |
| Create directories | `Bash` → `mkdir -p` |

**Base directory**: Tablet files are written to `./tablets/{slug}/` (relative to this skill directory).

---

## Main Flow: Full Ritual 🏮

> For critical decisions, key code changes, architecture design, pre-release checks

### Step 1: Open Altar 🏮

**Engineering meaning**: Load project context, ensure AI understands the full codebase

Refer to `${SKILL_DIR}/prompts/open_altar.md`

1. Check if the current project has a tablet
2. If yes, load all tablet files (meta.json, teachings.md, chronicles.md)
3. If no, ask if user wants to create one
4. Announce the altar opening with project summary

---

### Step 2: Burn Incense 🕯️

**Engineering meaning**: Thoroughly analyze requirements, decompose tasks, clarify goals and constraints

Refer to `${SKILL_DIR}/prompts/burn_incense.md`

Analyze the task across these dimensions:
- **What is sought**: One-sentence core requirement summary
- **Scope of impact**: Which files, modules, services are affected
- **Constraints**: Time, compatibility, performance requirements
- **Stakeholders**: Who will be affected by this change

---

### Step 3: Consult Chronicles 📜

**Engineering meaning**: Check git history, known bugs, past decisions to avoid repeating mistakes

Refer to `${SKILL_DIR}/prompts/consult_ancestors.md`

1. Check git history for related files
2. Review recent changes
3. Cross-reference with chronicles.md if available
4. Summarize: past footprints, past mistakes, unresolved issues

---

### Step 4: Three Kowtows, Nine Bows 🙇

**Engineering meaning**: Nine systematic quality checks — the core of the entire ritual

Refer to `${SKILL_DIR}/prompts/three_kowtows.md`

Three Kowtows = three dimensions (Correctness, Robustness, Maintainability)
Nine Bows = nine specific checks

**First Kowtow: Correctness**
- Bow 1: Is the requirement understood correctly?
- Bow 2: Is the logic consistent?
- Bow 3: Are edge cases handled?

**Second Kowtow: Robustness**
- Bow 4: Is error handling comprehensive?
- Bow 5: Is security ensured?
- Bow 6: Is performance acceptable?

**Third Kowtow: Maintainability**
- Bow 7: Is the code clean and clear?
- Bow 8: Is backward compatibility considered?
- Bow 9: Is observability in place?

---

### Step 5: Divination 🔮

**Engineering meaning**: Comprehensive risk assessment, give overall judgment

Refer to `${SKILL_DIR}/prompts/divination.md`

Based on the Nine Bows results, generate a hexagram:

| Hexagram | Condition | Meaning |
|----------|-----------|---------|
| 🟢 Great Fortune | All 9 ✅ | Go ahead with confidence |
| 🔵 Fortune | 7-8 ✅, no ❌ | Minor issues, proceed |
| 🟡 Small Fortune | 5-6 ✅, no ❌ | Proceed with caution |
| 🟠 Neutral | 1 ❌ or 3+ ⚠️ | Fix issues first |
| 🔴 Misfortune | 2+ ❌ | Ancestors say: stop and think |
| ⚫ Great Misfortune | 3+ ❌ | Ancestors are furious: wrong path |

---

### Step 6: Ancestral Manifestation ⚡

**Engineering meaning**: Execute the task with all checks passed and full confidence

Refer to `${SKILL_DIR}/prompts/blessing.md`

Execute if hexagram is Neutral or better. Include "Ancestral Certification" stamp.
If Misfortune or worse, list all issues and wait for user confirmation.

---

### Step 7: Dedicate Merit 🙏

**Engineering meaning**: Knowledge crystallization, update project archives for future reference

Refer to `${SKILL_DIR}/prompts/dedication.md`

1. Summarize lessons learned
2. Update tablet if applicable
3. Close with blessing

---

## Quick Blessing Mode 🕯️

> For routine changes, quick checks

Simplified flow:
1. Quick context scan
2. Three-bow express check (requirement? pitfalls? regression?)
3. Express hexagram
4. Execute + brief certification

---

## Execution Rules

1. **Ceremony is the means, quality is the goal**: All humor maps to serious engineering checks
2. **Nine bows must not be skipped**: In full ritual, every check must be honestly evaluated
3. **Hexagram must be honest**: Don't inflate scores — problems are problems
4. **Tablets accumulate wisdom**: Every ritual's lessons should be recorded
5. **Ancestral tone**: Maintain a dignified yet humorous tone, like a wise ancestor advising descendants
6. **Readable output**: Ritual formatting should be beautiful but not overshadow the actual content
