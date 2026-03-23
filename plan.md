<!-- /autoplan restore point: /Users/shiyangcui/.gstack/projects/vibe-iteration-coach/feature-v4-beginner-coach-optimization-autoplan-restore-20260323-150056.md -->
# Plan: Vibe Iteration Coach v4 — 初学者伴随教练优化

## 目标

将 vibe-iteration-coach 从一个面向**熟练迭代者的高级工具**优化为一个**初学者友好的伴随教练**，服务公司内部员工在**首次使用 Claude 进行非代码创作**时的指导需求。

## 背景

当前 v3.1 是一个功能强大但复杂度较高的系统（25 个技巧、6 个模式、6 维评估框架、17 种症状映射）。它的设计假设用户已经有多轮 AI 协作经验，知道什么是"迭代"。但实际部署场景是：**公司内部员工初次使用 Claude 进行文档、方案、分析等非代码工作**，这类用户：

1. 不知道什么是"迭代"——可能只打算用一轮对话完成任务
2. 不理解 T01-T25 的编号系统——看到"T11 三视角分析"会感到困惑
3. 需要的不是"6 种模式选择"——需要教练自动判断当前该做什么
4. 最大的痛点不是"怎么做版本跳跃"——而是"我的第一版为什么不好"
5. 中英双语混用可能增加认知负担

## 核心优化方向

### 1. 降低入门门槛
- 简化触发方式（自然语言识别，不需要记命令）
- 自动模式检测（用户不需要知道有 6 个模式）
- 渐进式技巧引入（第一次只教 3-5 个核心技巧，随使用深度逐步解锁）

### 2. 增加主动干预能力
- 在用户迭代过程中**主动插入教练提示**（而非等用户来问）
- 检测常见初学者模式：一次性完成（不迭代）、全盘接受 AI 输出、跳过验证
- 用简单语言解释为什么要做某件事

### 3. 重新定义成功标准
- 初学者的成功不是"54/60 S 级"——而是"学会了 3 个基本技巧并能独立使用"
- 新增"成长阶段"概念：新手 → 入门 → 熟练 → 专家
- 评估框架需要简化版（3 维度而非 6 维度？）

### 4. 内容本地化与简化
- 统一语言（中文为主 or 英文为主，不混用）
- 技巧名称用直觉可理解的名字（"先看再改" vs "T03 Preview Before Execute"）
- 减少概念密度（Mode/Technique/Dimension/Symptom/Anti-pattern 太多层级）

### 5. 伴随式教练模式
- 新增 "伴随模式"：在用户正常使用 Claude 工作时，教练在旁观察并适时提供建议
- 不打断工作流，用轻量提示（如 tooltips 级别的建议）
- 在关键时刻介入：用户即将提交最终版本时提醒验证，用户反复修改同一处时建议换策略

## 受影响的文件

| 文件 | 变更类型 | 说明 |
|------|---------|------|
| src/SKILL.md | 重构 | 增加初学者分流逻辑、伴随模式、渐进式解锁 |
| src/references/techniques.md | 重构 | 技巧分层（核心 5 + 进阶 10 + 高级 10） |
| src/references/evaluation-framework.md | 新增简化版 | 初学者 3 维评估 |
| src/references/scene-mapping.md | 增加初学者场景 | 首次创作场景映射 |
| src/references/technique-finder.md | 增加初学者症状 | "我不知道怎么开始"等 |
| docs/README.md | 重写 | 面向初学者的使用指南 |
| 新增: src/references/beginner-guide.md | 新增 | 初学者专用快速指南 |
| 新增: src/references/companion-mode.md | 新增 | 伴随模式规范 |

## 开放问题（已由 autoplan 解决）

1. ~~是否保留高级功能？~~ → **保留全部**，通过 Mode 0 拦截层对初学者渐进式解锁
2. ~~伴随模式如何实现？~~ → **重新定义为 "post-mode coaching hook"**，在每个 Mode 执行后增加教练反思步骤，而非被动观察
3. ~~成长阶段如何持久化跟踪？~~ → **扩展 persistence-layer.md**，在 YAML 中增加 skill_level 字段，旧日志缺失时默认 null
4. ~~目标语言？~~ → **DEFERRED** — 需要用户单独确认

## 毕业标准（autoplan 新增）

初学者 → 入门：完成 3 次教练会话 AND 累计使用 5 种不同技巧
入门 → 熟练：完成 8 次教练会话 AND D1-D6 均分 ≥ 6 AND 无重复反模式
熟练 → 专家：完成 15 次教练会话 AND 总分 ≥ 48/60

## Expert Override Triggers（autoplan 新增）

以下触发词绕过 Mode 0，直接进入完整模式：
- "高级模式" / "advanced mode" / "expert mode"
- "跳过新手引导" / "skip beginner" / "skip tutorial"
- 直接使用 T-编号（如 "use T11"、"帮我做 T08"）
- 直接指定 Mode（如 "Mode 4 Navigate"、"Reduction Check"）

Override 不改变 skill_level，仅本次会话绕过。

## Coaching Hook Rules（autoplan 新增）

每个 Mode 执行完成后，检测以下模式并给出 1-2 句提示：

| 检测模式 | 条件 | 教练提示 |
|---------|------|---------|
| 全盘接受 | 用户在 3+ 轮中未对 AI 输出提出任何修改 | "试试让 AI 从不同角度挑战你的方案——好的想法经得住反驳" |
| 缺少验证 | 用户准备交付但未做过一致性检查 | "交付前花 30 秒让 AI 检查全文逻辑一致性——这是最值得的 30 秒" |
| 重复打转 | 用户在同一部分修改了 3+ 次但没有实质进展 | "如果微调解决不了，试试换个角度——有时需要推倒重来而不是修修补补" |
| 格式先行 | 用户在内容未定之前就要求格式化 | "先把内容做对，再管它长什么样——内容和格式分开做效率更高" |

提示用简单中文，不引用 T-编号。在 beginner 阶段结束后（skill_level ≥ intermediate）减少提示频率。

## 选定方案：Approach C — 模式分层

在同一 skill 中增加 Mode 0 "Beginner Coach"，自动拦截新用户进入简化流程。
- Mode 0 核心逻辑放在 beginner-guide.md
- SKILL.md 只保留路由判断
- 伴随模式作为 post-mode coaching hook 嵌入现有流程
- 保留全部高级功能，通过成长阶段渐进解锁

## NOT in scope

| Item | Rationale |
|------|-----------|
| 团队级分析仪表板 | Ocean — 需要后端基础设施 |
| 自适应学习路径 | 依赖成长数据积累，defer to v5 |
| Multi-language support | 先建立单语言基础 |
| Integration with other Claude skills | 平台级关注，非 skill 级 |

## What already exists

| Sub-problem | Existing code | Reuse? |
|-------------|--------------|--------|
| Mode detection | SKILL.md triggers | Extend with beginner triggers |
| Technique prescription | technique-finder.md S01-S17 | Add S18-S20 |
| Logging | persistence-layer.md | Add skill_level field |
| Evaluation | evaluation-framework.md | Add simplified display |
| Scene mapping | scene-mapping.md | Add beginner scene row |

## Failure Modes Registry

| CODEPATH | FAILURE MODE | RESCUED? | USER SEES | CRITICAL? |
|----------|-------------|----------|-----------|-----------|
| skill_level detection | Old log missing field | Y (null) | Normal | No |
| Mode 0 routing | Expert with no log | Y (unknown) | May get Mode 0 once | No |
| Beginner guide ref | File missing | N | Error | **YES** |
| Growth check | Threshold undefined | Fixed (see 毕业标准) | N/A | Fixed |

<!-- AUTONOMOUS DECISION LOG -->
## Decision Audit Trail

| # | Phase | Decision | Principle | Rationale | Rejected |
|---|-------|----------|-----------|-----------|----------|
| 1 | CEO-0C | Choose Approach C (模式分层) over A (Beginner Layer) and B (New Skill) | P4 DRY + P5 Explicit | 统一代码库，不重复核心技巧库，改动最少 | A (too many if/else), B (DRY violation) |
| 2 | CEO-0D | SELECTIVE EXPANSION mode | P1+P6 | 保持当前范围 + 精选扩展 | SCOPE EXPANSION (too ambitious for v4) |
| 3 | CEO-0D | Accept E4 (技巧名称中文化) + E5 (README) + E6 (成长阶段) | P2 Boil lakes | 全部在爆炸半径内，<1天CC工作量 | — |
| 4 | CEO-0D | Defer E1 (统一语言), E2 (仪表板), E3 (自适应) | P3 Pragmatic | E1 需用户确认，E2/E3 超出范围 | — |
| 5 | CEO-S1 | Redefine companion mode as post-mode coaching hook | P5 Explicit | Skill 框架不支持被动观察，改为主动嵌入 | Original passive observation design |
| 6 | CEO-S2 | skill_level missing → default null, not beginner | P5 Explicit | 不假设用户等级，明确标记为未知 | Default to beginner |
| 7 | CEO-S4 | Mode 0 logic in beginner-guide.md, not SKILL.md | P5 Explicit | 保持主文件简洁 | Inline in SKILL.md |
| 8 | CEO-FM | Add graduation criteria: 3 sessions + 5 techniques | P1 Completeness | 补足计划中的关键缺失 | No criteria (never graduate) |
| 9 | ENG-S2 | Core 5 techniques: T03, T06, T11, T14, T15 | P3 Pragmatic | 覆盖最常见初学者错误 | — |
| 10 | ENG-S3 | Must specify expert override triggers | P1 Completeness | Path 4 未定义 | Undefined |
| 11 | ENG-S3 | Must specify coaching hook detection rules | P1 Completeness | Path 6 未定义 | Undefined |

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|--------|---------|-----|------|--------|----------|
| CEO Review | `/plan-ceo-review` | Scope & strategy | 1 | CLEAN | 5 premises challenged, 1 critical gap fixed (graduation criteria), companion mode redefined |
| Codex Review | `/codex review` | Independent 2nd opinion | 0 | UNAVAILABLE | codex not installed |
| Eng Review | `/plan-eng-review` | Architecture & tests | 1 | CLEAN | 3 issues found and resolved (core-5 selection, expert override, coaching hooks) |
| Design Review | `/plan-design-review` | UI/UX gaps | 0 | SKIPPED | No UI scope |

**VERDICT:** APPROVED via `/autoplan`. Plan reviewed through CEO + Eng pipeline with 11 auto-decisions. Ready for implementation.
