# Persistence Layer 设计方案 — 教练日志持久化

## 设计定位

### 不做 Mode 7，做跨 Mode 的基础设施层

日志持久化是一个**横切关注点**，不是用户会主动调用的教练动作。6 个 Mode 各自回答一个教练问题，日志层的职责是"每次教练互动后自动记一笔"。

```
                    ┌─────────────────────────────┐
                    │    Persistence Layer         │
                    │  (自动写入，按需读取)          │
                    └──────────┬──────────────────┘
                               │ 每次 Mode 输出后自动追加
        ┌──────────┬───────────┼───────────┬──────────┐
        ▼          ▼           ▼           ▼          ▼
    Mode 1     Mode 2     Mode 3/4/5    Mode 6    未来 Mode
    Review     Plan       Assist/Nav/   Reduction
    (读+写)    (写)       Toolkit(写)   (写)
       ▲
       │ 历史日志回读，支持长期趋势分析
       └────────────────────────────────────
```

**写入端：** 所有 6 个 Mode 执行完毕后自动追加一条日志
**读取端：** Mode 1 (Review) 增强为可读取历史日志，做长期模式分析

### 与已有技巧的关系

| 已有技巧 | 职责 | 持久化层的区别 |
|----------|------|---------------|
| T18 Track and Trace | 用户主动要求生成变更日志 | 持久化层是**系统自动记录**，不需要用户触发 |
| T22 Session Handoff | 用户在会话结束前生成状态快照 | 持久化层记录的是**教练互动的元数据**，不是项目状态 |
| T23 Context Compression | 压缩对话历史供跨会话使用 | 持久化层是**结构化长期存储**，不是临时压缩 |

简言之：T18/T22/T23 记录的是**项目做了什么**，持久化层记录的是**用户的迭代行为模式**（用了哪些技巧、哪些维度得分高/低、哪些反模式反复出现）。

---

## 持久化格式：方案 C（YAML 头 + Markdown 正文）

### 文件规格

```
文件名：vibe-iteration-log.md
位置：与项目文件同目录（用户 workspace）
编码：UTF-8
追加方式：每条记录前插 ---\n 分隔符
```

### 单条记录结构

```yaml
---
id: "2026-03-23T14:32:00+08:00"
mode: 6                          # 1-6
mode_name: "Reduction Check"
project: "vibe-iteration-coach"  # 用户项目名
version: "v3"                    # 当前版本号（如有）
session: 3                       # 第几次教练会话

# Mode 1 Review 专属字段
scores:                          # D1-D6 得分（仅 Mode 1 填写）
  D1_intent: null
  D2_rhythm: null
  D3_critical: null
  D4_framework: null
  D5_ownership: null
  D6_deliverable: null
  total: null

# Mode 6 Reduction Check 专属字段
saturation_index: 17             # 饱和度指数（仅 Mode 6 填写）
saturation_status: "轻度膨胀"

# 通用字段
techniques_used: ["T07", "T14"]  # 本次使用/推荐的技巧
techniques_missed: ["T06"]       # 本次缺失的技巧（Mode 1 填写）
anti_patterns: ["Complexity Ratchet"]  # 检测到的反模式
core_loop_position: 4            # 用户在 5 步循环的位置（1-5）
coaching_action: "prescribe"     # 本次教练动作类型：
                                 #   review / plan / assist / navigate / prescribe / reduce
---

## Reduction Check · vibe-iteration-coach v3

**诊断摘要：** 饱和度指数 17/100，轻度膨胀。发现 2 个过饱和元素（S01-S16 硬编码、惩罚因子循环引用），已修复。

**关键发现：**
- 层级分布基本健康（L1 23%, L2 33%, L3 37%, L4 7%）
- L3 轻度膨胀但在可控范围
- 框架能自诊断，逻辑自洽

**处方：** 修复数字同步 bug，加入元评估声明，层级健康度改用加权公式
```

### 字段说明

**必填字段（每条记录）：** id, mode, mode_name, project, coaching_action
**按 Mode 填写的字段：**

| 字段 | Mode 1 | Mode 2 | Mode 3 | Mode 4 | Mode 5 | Mode 6 |
|------|--------|--------|--------|--------|--------|--------|
| scores (D1-D6) | ✅ | — | — | — | — | — |
| saturation_index | — | — | — | — | — | ✅ |
| techniques_used | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| techniques_missed | ✅ | — | — | — | — | — |
| anti_patterns | ✅ | — | ✅ | — | ✅ | ✅ |
| core_loop_position | ✅ | — | ✅ | — | ✅ | — |
| version | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| session | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Markdown 正文：** 人类可读的诊断摘要，不超过 5 行，用于快速回顾。

---

## 读取端：Mode 1 (Review) 增强

### 新增能力：历史趋势分析

当 Mode 1 被调用且日志文件存在时，除了评估当前会话，额外执行历史分析：

```
Step 1: 读取 vibe-iteration-log.md
Step 2: Parse 所有 YAML 头，按时间排序
Step 3: 生成长期趋势报告：

  3a. D1-D6 得分趋势（如果有 3+ 次 Review 记录）
      → 哪些维度在进步？哪些维度持续低分？

  3b. 技巧使用频率分布
      → 最常用的 Top 5 技巧
      → 从未使用的技巧（盲区）

  3c. 反模式复发率
      → "你最近 5 次中有 3 次出现 Acceptance Loop"

  3d. 饱和度趋势（如果有 Mode 6 记录）
      → 饱和度是在上升还是下降？

  3e. 核心循环位置热力图
      → 你最常停在哪一步？最常跳过哪一步？
```

### 输出示例（追加到 Review 报告末尾）

```markdown
## 📈 长期趋势（基于 8 次教练记录）

### D1-D6 得分走势
| 维度 | 前3次均分 | 近3次均分 | 趋势 |
|------|----------|----------|------|
| D1 Intent | 6.3 | 8.0 | ⬆️ +1.7 |
| D2 Rhythm | 5.0 | 5.3 | → 持平 |
| D3 Critical | 4.7 | 7.3 | ⬆️ +2.6 |
| D5 Ownership | 7.0 | 6.0 | ⬇️ -1.0 ⚠️ |

### 技巧盲区
从未使用：T10 (Converge), T20 (Delegation), T24 (Modal Sync)
→ 建议：下次项目进入收尾阶段时主动尝试 T10

### 反模式复发
Acceptance Loop: 出现 3/8 次 (38%) ← 最需要关注
→ 你倾向于接受 AI 建议而不做显式选择，建议每次用 T14 强制自己说 "I choose X because Y"

### 核心循环热力图
① PROPOSE ████████ (频繁)
② STRESS  ██████   (频繁)
③ EXTRACT ██       (偶尔) ← 你经常跳过提炼
④ DECIDE  ████     (有时)
⑤ VERIFY  █        (罕见) ← 最大短板
→ 你的模式是 ①②①②④，跳过 ③ 和 ⑤。建议在每次 STRESS 后强制执行一次 EXTRACT。
```

---

## 写入流程

### 自动写入时机

```
用户调用任意 Mode
    │
    ▼
Mode 正常执行，输出教练结果
    │
    ▼
提取元数据（Mode 类型、使用的技巧、得分、反模式等）
    │
    ▼
生成 YAML 头 + Markdown 摘要
    │
    ▼
追加到 vibe-iteration-log.md
    │
    ▼
向用户确认："📝 已记录到教练日志（第 N 条）"
```

### 写入规则

1. **静默追加，一句话确认。** 不打断教练流程，写完后只说一句确认
2. **不记录 partial 交互。** 只在 Mode 完整执行完毕并输出结果后记录；中途取消不记录
3. **项目名自动识别。** 从对话上下文推断 project 字段；如果无法推断，标为 "unnamed"
4. **session 自动递增。** 同一 project 的记录自动递增 session 编号
5. **首次写入自动创建文件。** 如果 vibe-iteration-log.md 不存在，自动创建并写入表头

### 首次创建的文件头

```markdown
# Vibe Iteration Coach — 教练日志

> 此文件由 Vibe Iteration Coach 自动维护。每次教练互动后追加一条记录。
> 用于长期追踪迭代能力的进化，支持 Mode 1 (Review) 的历史趋势分析。
>
> 格式：YAML 头（机器可读）+ Markdown 正文（人类可读）
>
> 手动编辑提示：可以自由编辑 Markdown 正文部分（添加个人笔记），
> 但请勿修改 YAML 头中的字段名和结构，否则会影响趋势分析。
```

---

## 用户交互设计

### 主动调用（可选）

虽然日志写入是自动的，但用户可以主动查看和操作：

| 触发短语 | 动作 |
|----------|------|
| "看看我的教练日志" / "show my coaching log" | 读取日志，输出统计摘要 |
| "我的迭代趋势" / "my iteration trends" | 在 Mode 1 中触发历史趋势分析 |
| "清空日志" / "reset log" | 确认后清空（需二次确认） |
| "导出日志" / "export log" | 原样输出 .md 文件 |

### 隐私考量

- 日志只存在用户的 workspace 文件夹中，不外传
- 只记录教练元数据（用了哪些技巧、得了几分），不记录项目的实际内容
- Markdown 正文中的摘要由 Coach 生成，控制在 5 行以内，不包含敏感项目细节

---

## 实现要点

### 需要新增的文件

1. **`references/persistence-layer.md`** — 日志格式规范 + YAML schema + 写入/读取规则
2. 不需要新增 template（日志格式嵌入 reference 即可）

### 需要修改的文件

| 文件 | 修改内容 |
|------|----------|
| **SKILL.md** | 在 Mode 1 描述中增加"历史趋势分析"步骤；在教练原则中增加第 9 条关于日志的原则；在 Mode 流程图中标注 Persistence Layer |
| **SKILL.md description** | 追加触发短语 "看看我的教练日志", "my iteration trends" |
| **templates/review-template.md** | 增加"长期趋势"输出区块 |

### 不需要修改的文件

- references/techniques.md — T18 保持不变（用户主动 vs 系统自动是不同职责）
- references/techniques-extended.md — T22/T23 保持不变（记录项目状态 vs 记录教练元数据是不同内容）
- 其余所有 reference 和 template 文件

### 新增教练原则（第 9 条）

```
9. **日志自动，分析按需。** 每次教练互动后自动追加日志，但历史趋势分析只在
   Mode 1 Review 中按需呈现。不要在每次交互中都展示历史数据——那会分散用户
   对当前迭代的注意力。日志的价值在"回看"而非"实时"。
```

---

## 版本影响评估

| 影响项 | v3 现状 | v4 预期 |
|--------|--------|--------|
| 模式数量 | 6 | 6（不变） |
| 新增文件 | — | +1（persistence-layer.md） |
| 修改文件 | — | 2（SKILL.md, review-template.md） |
| 技巧数量 | 25 | 25（不变） |
| 教练原则 | 8 条 | 9 条 |
| 描述字符数 | 838 | 需检查（追加触发短语后） |
| 饱和度预估 | 17/100 | ~19/100（新增 1 个 L2 元素 + 2 个 L3 元素） |
