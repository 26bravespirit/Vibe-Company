# Persistence Layer — 教练日志持久化规范

教练日志是一个跨 Mode 的基础设施层，在每次教练互动完成后自动追加一条记录，用于长期追踪用户迭代能力的进化。

## Table of Contents
- [日志文件规格](#file-spec)
- [单条记录格式](#record-format)
- [写入规则](#write-rules)
- [读取与分析（Mode 1 增强）](#read-rules)

---

## 日志文件规格 {#file-spec}

```
文件名：vibe-iteration-log.md
位置：与项目文件同目录（用户 workspace）
编码：UTF-8
分隔：每条记录前用 --- 分隔
```

### 首次创建的文件头

当日志文件不存在时，自动创建并写入以下文件头：

```markdown
# Vibe Iteration Coach — 教练日志

> 此文件由 Vibe Iteration Coach 自动维护。每次教练互动后追加一条记录。
> 用于长期追踪迭代能力的进化，支持 Mode 1 (Review) 的历史趋势分析。
>
> 格式：YAML 头（机器可读）+ Markdown 正文（人类可读）
> 手动编辑：可以自由编辑 Markdown 正文（添加个人笔记），请勿修改 YAML 字段名和结构。
```

---

## 单条记录格式 {#record-format}

每条记录由 YAML 头（机器可读）和 Markdown 正文（人类可读）组成：

```yaml
---
id: "2026-03-23T14:32:00+08:00"   # ISO 8601 时间戳
mode: 6                             # 1-6
mode_name: "Reduction Check"
project: "项目名"                    # 从上下文推断，无法推断则 "unnamed"
version: "v3"                       # 当前版本号（如有）
session: 3                          # 同一 project 的第几次教练会话，自动递增

# === Mode 1 Review 专属 ===
scores:                             # D1-D6 得分，仅 Mode 1 填写
  D1_intent: null
  D2_rhythm: null
  D3_critical: null
  D4_framework: null
  D5_ownership: null
  D6_deliverable: null
  total: null

# === Mode 6 Reduction Check 专属 ===
saturation_index: null              # 0-100，仅 Mode 6 填写
saturation_status: null             # 精简/轻度膨胀/中度过饱和/重度过饱和/系统性危机

# === 通用字段 ===
techniques_used: []                 # 本次使用或推荐的技巧编号
techniques_missed: []               # 本次缺失的技巧（主要由 Mode 1 填写）
anti_patterns: []                   # 检测到的反模式名称
core_loop_position: null            # 用户在 5 步循环的位置（1-5），Mode 3/5 填写
coaching_action: ""                 # review / plan / assist / navigate / prescribe / reduce
---

## [Markdown 正文：≤5 行的人类可读摘要]
```

### 字段填写矩阵

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

不适用的字段保留 null 或空列表 []，不要省略字段。

---

## 写入规则 {#write-rules}

### 写入时机

每个 Mode **完整执行并输出结果后**自动追加一条记录。

### 写入原则

1. **静默追加，一句话确认。** 写完后只输出一句："📝 已记录到教练日志（第 N 条）"，不打断教练流程
2. **不记录 partial 交互。** 中途取消、用户未等到完整输出的情况不记录
3. **project 自动识别。** 从对话上下文推断项目名；无法推断则标为 "unnamed"
4. **session 自动递增。** 同一 project 的记录自动递增 session 编号（读取已有记录中的最大 session +1）
5. **首次写入自动创建文件。** 如果 vibe-iteration-log.md 不存在，先写入文件头再追加记录
6. **只记录元数据，不记录项目内容。** YAML 中只有技巧编号、得分、反模式等元数据；Markdown 正文限制在 5 行以内，不含敏感项目细节

---

## 读取与分析（Mode 1 增强）{#read-rules}

当 Mode 1 (Review) 被调用且日志文件存在时，在常规评估之后**额外执行历史趋势分析**。

### 分析流程

```
Step 1: 读取 vibe-iteration-log.md
Step 2: Parse 所有 YAML 头，按 id（时间戳）排序
Step 3: 生成趋势报告（需要 ≥3 条记录才有统计意义）
```

### 五项趋势指标

**3a. D1-D6 得分趋势**（需要 ≥3 次 Mode 1 记录）
- 计算前半段均分 vs 后半段均分
- 标注上升 ⬆️ / 持平 → / 下降 ⬇️
- 对持续低分（≤5）的维度发出预警

**3b. 技巧使用频率分布**
- 统计 techniques_used 中每个技巧出现的次数
- 列出 Top 5 最常用 + 从未使用的技巧（盲区）
- 盲区技巧配合场景建议

**3c. 反模式复发率**
- 统计 anti_patterns 中每个模式出现的次数和比率
- 复发率 >30% 的反模式标为"需重点关注"

**3d. 饱和度趋势**（需要 ≥2 次 Mode 6 记录）
- 饱和度指数是在上升还是下降
- 如果连续上升，建议安排一次专门的精简迭代

**3e. 核心循环位置热力图**
- 统计 core_loop_position 的分布
- 识别最常停留和最常跳过的步骤
- 给出针对性建议

### 趋势报告最低数据要求

| 指标 | 最低记录数 | 不足时处理 |
|------|-----------|-----------|
| D1-D6 趋势 | 3 条 Mode 1 | 跳过，提示"再积累 N 次 Review 后可解锁趋势分析" |
| 技巧频率 | 3 条任意 Mode | 跳过 |
| 反模式复发 | 5 条任意 Mode | 跳过 |
| 饱和度趋势 | 2 条 Mode 6 | 跳过 |
| 循环热力图 | 3 条 Mode 3/5 | 跳过 |

### 用户主动查看

| 触发短语 | 动作 |
|----------|------|
| "看看我的教练日志" / "show my coaching log" | 读取日志，输出统计摘要 |
| "我的迭代趋势" / "my iteration trends" | 触发完整趋势分析 |
| "清空日志" / "reset log" | 二次确认后清空 |
