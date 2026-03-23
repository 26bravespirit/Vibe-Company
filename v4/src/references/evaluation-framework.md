# 6-Dimension Evaluation Framework

## v4 新增：新手简化评估模式

当用户 skill_level 为 beginner 或 intermediate 时，使用简化版3维评估。

### 简化版（新手/入门）

| 维度 | 对应完整维度 | 评估问题 | 评分方式 |
|------|------------|---------|---------|
| 📝 表达清晰度 | D1 意图传递 | "你让AI理解你想要什么了吗？" | 🟢🟡🔴 |
| 🔄 改进意识 | D3 批判性思维 | "你有没有让AI反过来挑战你的方案？" | 🟢🟡🔴 |
| 🎯 做出选择 | D5 主导权把控 | "你有没有主动做选择，而不是让AI替你决定？" | 🟢🟡🔴 |

**评分标准：**
- 🟢 做得好 — 在这个维度上展现了良好的习惯
- 🟡 可以更好 — 有意识但不够一致
- 🔴 下次注意 — 这个维度几乎没有体现

**简化版输出格式：**
```
你这次的表现：
📝 表达清晰度：🟢 你的指令很清楚，AI基本一次就理解了
🔄 改进意识：🟡 你做了一次修改，但可以多让AI从不同角度挑战
🎯 做出选择：🟢 你在两个方案中主动选了B，并说出了原因

💡 下次试试：在觉得"差不多了"的时候，多问一句"这有什么问题？"
```

### 从简化版到完整版的过渡

当用户从 intermediate 升级到 skilled 时：
1. 首次 Review 仍用简化版，但附加说明："你现在可以使用完整的6维评估了。要试试吗？"
2. 如果用户同意，切换到完整版
3. 如果用户拒绝，继续用简化版直到用户主动要求

---

## 完整版（熟练/专家）

### Dimensions

### D1 · Intent Transmission Efficiency (意图传递效率)
**Does each prompt precisely convey what the user wants? How many rounds does AI need to understand correctly?**

| Score | Criteria |
|-------|----------|
| 9-10 | Single-prompt paradigm shifts. AI executes correctly without follow-up questions. Batch operations with zero ambiguity. |
| 7-8 | Most prompts are clear. Occasional need for one clarification round. |
| 5-6 | Intent is generally understood but requires multiple back-and-forth to align. |
| 3-4 | AI frequently misunderstands. Many wasted turns on clarification. |
| 1-2 | Prompts are so vague that AI produces wrong outputs repeatedly. |

**What to look for:** Paradigm-level instructions (T01) that work in one shot. Precise batch operations (T02). When the user says "delete 6.2, 6.3, 6.5, and chapters 7-9" and AI does exactly that — that's a 10.

### D2 · Iteration Rhythm (迭代节奏感)
**When to push forward, pull back, expand, contract — is the rhythm effective?**

| Score | Criteria |
|-------|----------|
| 9-10 | Clear patterns of evaluate-then-improve, expand-then-contract, explore-then-converge. Version leaps at the right moments. Uses Navigate (Mode 4) to find direction before major version jumps rather than tweaking blindly. |
| 7-8 | Good rhythm with occasional missed beats (e.g., expanding too long without contracting). |
| 5-6 | Some rhythm exists but inconsistent — periods of productive iteration mixed with stalling. |
| 3-4 | No discernible rhythm. Random switching between topics without completing previous work. |
| 1-2 | Chaotic — no iteration pattern, constant restarts, no convergence. |

**What to look for:** T06 (evaluate-improve loops), T07 (expand-contract), T08 (version leaps at critical junctures). The shift from exploration to institutional convergence (T10). Using Navigate between major versions to consciously choose direction rather than drifting.

### D3 · Critical Thinking Application (批判性思维运用)
**Does the user proactively challenge AI's output, find blind spots, and force multi-angle analysis?**

| Score | Criteria |
|-------|----------|
| 9-10 | Actively requests attacks on own work. Uses three-perspective analysis (T11). Discovers blind spots before AI does (T12). Extracts insights from AI's responses (T13). Uses Navigate's dual-engine output to examine project from both first-principles and creative angles. |
| 7-8 | Good critical engagement with occasional passive acceptance of AI output. |
| 5-6 | Some critical review, but mostly accepts AI's first response without challenge. |
| 3-4 | Rarely challenges AI. Accepts most outputs at face value. |
| 1-2 | Zero critical engagement. AI's output is treated as final truth. |

**What to look for:** T11 (three-perspective analysis), T12 (proactive blind spot discovery), T13 (extracting concepts from AI answers). The user saying "attack this document" or "what's wrong with this framework." Engaging seriously with Navigate directions (not just picking the first one) — comparing A-group vs B-group thinking modes.

### D4 · Framework Building Ability (框架构建能力)
**Does the user create reusable structures (evaluation systems, naming conventions, institutional frameworks) or only make one-off fixes?**

| Score | Criteria |
|-------|----------|
| 9-10 | Creates multiple reusable frameworks that compound across the project. Naming systems, evaluation rubrics, institutional documents. |
| 7-8 | Some framework creation, but mostly working at the content level rather than the structural level. |
| 5-6 | Occasional framework thinking mixed with mostly tactical edits. |
| 3-4 | Almost entirely tactical — making individual fixes without systemic thinking. |
| 1-2 | No framework awareness. Every change is a one-off patch. |

**What to look for:** Evaluation systems that get reused. Naming conventions applied consistently. The transition from informal documents to formal institutional policy (T10).

### D5 · Ownership Control (主导权把控)
**Who is driving the direction — the user or AI?**

| Score | Criteria |
|-------|----------|
| 9-10 | User proposes every major direction change. AI fills in details and executes. When AI provides options, user makes explicit choices with reasoning (T14). When using Navigate, user selects directions with clear rationale rather than defaulting to the "easiest" or "first" option. |
| 7-8 | User mostly leads, but occasionally follows AI's suggestions without much scrutiny. |
| 5-6 | Mixed — some user-driven, some AI-driven direction changes. |
| 3-4 | AI is largely steering. User mostly says "ok, sounds good" to AI proposals. |
| 1-2 | Complete delegation to AI. User provides no direction, just accepts whatever AI produces. |

**What to look for:** T14 (choose, don't accept). The user saying "I choose option B because..." vs "just go with whatever you think is best." Paradigm shifts initiated by the user vs suggested by AI. In Navigate, the quality of the user's selection reasoning.

### D6 · Deliverable Management (产出物管理)
**Version control, file naming, cross-file consistency, final deliverable quality.**

| Score | Criteria |
|-------|----------|
| 9-10 | Clean version progression (v2→v3→...→v7). All supporting files synced (T17). Change tracking maintained (T18). Verification before delivery (T16). |
| 7-8 | Good version control with occasional inconsistencies in supporting documents. |
| 5-6 | Basic versioning exists but supporting files are often out of sync. |
| 3-4 | Poor version control. Unclear which version is current. Files contradict each other. |
| 1-2 | No version management. Outputs scattered without organization. |

**What to look for:** T16 (verify before deliver), T17 (sync supporting files), T18 (track and trace), T19 (multi-dimensional scoring validation).

## Scoring

Total possible: 60 points.

| Range | Rating | Meaning |
|-------|--------|---------|
| 54-60 | S | Benchmark — can be used as a teaching case |
| 42-53 | A | Excellent — highly effective iteration |
| 30-41 | B | Good — solid but with clear improvement areas |
| 18-29 | C | Needs improvement — significant technique gaps |
| < 18 | D | Fundamental rethinking needed |
