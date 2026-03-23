# Extended Techniques (T20-T25) — 协同扩展

These 6 techniques address blind spots in the core library (T01-T19). The core techniques cover how to communicate with AI, manage iteration rhythm, think critically, and control quality — all within a single person × single AI × single session context. The extended techniques break out of that box: they handle collaboration, memory across sessions, multi-modal work, and the psychological traps that derail even skilled iterators.

Read `references/techniques.md` for the core 19 techniques first. These extended techniques build on top of them.

---

## Collaboration & Delegation (T20-T21)

### T20 · Delegation Prompt (委托指令)
**Write a structured "task brief" so someone else — another person or another AI session — can pick up your work without losing context.**

Use when: You need to hand off part of the project to a colleague, or you want a fresh AI session to continue work without starting from scratch. Also useful when splitting a large project into parallel workstreams.

How to do it: Write a brief with these 5 fields:
```
1. Current state: What exists now (version, key files, overall structure)
2. Goal: What the next person/session should accomplish
3. Constraints: What must NOT change (decisions already locked in)
4. Context: Why we're at this point (key decisions and their rationale)
5. First action: The specific thing to do first
```

Example: "Here's the brief for the data analysis section: We're on v4 of the org design. The structure is finalized (3 tiers, flat within each tier — DON'T change this). Your job is to design the performance evaluation framework for this structure. Start by analyzing how Anthropic and Stripe evaluate performance in flat orgs."

Anti-pattern: Saying "continue where I left off" in a new session with zero context — the AI will hallucinate the context or ask 10 clarifying questions.

**Relationship to core techniques:** T20 is the multi-session/multi-person version of T01 (paradigm-level instructions). Just as T01 resets the AI's understanding in one prompt, T20 resets a new collaborator's understanding in one brief.

### T21 · Review Protocol (角色审阅)
**Have AI adopt a specific stakeholder role to review your work — simulating a team review without needing an actual team.**

Use when: You want diverse feedback but don't have team members available to review. Or when you want to stress-test against a specific audience before presenting to them.

How to do it: Name a specific role and ask AI to stay fully in character while reviewing:
```
"Review this document as if you are:
- A skeptical CFO who only cares about ROI
- A first-week employee trying to understand the org
- A competitor analyzing this for weaknesses
Stay in character. Don't break role. Give me your honest reaction."
```

Run 2-3 roles sequentially. After each role-review, extract the insights (T13) before moving to the next role.

Example: "Act as a hostile venture capitalist reading this business plan for the first time. What questions would you ask in the first 3 minutes? What would make you pass?"

Anti-pattern: Asking AI to "review as several people at once" — it produces mushy, uncommitted feedback. One role at a time, deep in character.

**Relationship to core techniques:** T21 is a structured extension of T11 (three-perspective analysis). T11 asks for three thinking modes (creative / first-principles / reliable); T21 asks for specific human perspectives with emotional and professional stakes.

---

## Cross-Session Memory (T22-T23)

### T22 · Session Handoff (会话交接)
**At the end of every working session, generate a structured "state snapshot" that allows the next session to resume without information loss.**

Use when: Your project spans multiple days or sessions. Any time you're about to close a conversation that you plan to continue later.

How to do it: Before ending a session, prompt:
```
"Generate a session handoff document:
1. Current version: [what exists now]
2. Key decisions made this session: [list with rationale]
3. Open questions: [unresolved items]
4. Next session priority: [the #1 thing to do first]
5. Danger zones: [things that are fragile or might break]"
```

Save this as a file (e.g., `handoff-v4-session3.md`). Start the next session by feeding this document as context.

Example: "Handoff: v4 of the org policy is complete. Key decision: we chose the 'hat not chair' metaphor for roles (T14). Open question: we haven't resolved the conflict resolution process in Chapter 8. Next session: tackle Chapter 8 first. Danger zone: if you change the role definitions in Chapter 3, Chapters 5 and 7 will break."

Anti-pattern: Ending a session with "we'll continue tomorrow" and hoping you'll remember. You won't. The AI definitely won't.

**Relationship to core techniques:** T22 extends T18 (track and trace) from within-session to across-session. T18 logs what changed; T22 packages the current state + intent for continuity.

### T23 · Context Compression (上下文压缩)
**Compress a long conversation history into a structured summary that preserves decisions and rationale while shedding the noise.**

Use when: The conversation has grown so long that the AI is losing early context, or you're starting a new session and need to inject history efficiently. Also useful when you need to explain the project state to someone unfamiliar.

How to do it: Ask AI to create a tiered summary:
```
"Compress our entire conversation into three layers:
Layer 1 — Core Decisions (≤10 items): The key choices that define the current version
Layer 2 — Rationale Map (≤20 items): Why each decision was made
Layer 3 — Evolution Log: v1→v2→...→vN, one line per version describing the paradigm shift"
```

Use Layer 1 as the "always include" context. Add Layer 2 when decisions are being questioned. Layer 3 is for traceability.

Example output:
```
Layer 1: (1) Flat structure, no hierarchy (2) Roles are hats, not chairs (3) 33-article policy format...
Layer 2: Flat structure chosen because v2's hierarchy created bottlenecks (see T08 version leap)...
Layer 3: v1=traditional hierarchy → v2=three-tier → v3=Member+Role flat → v4=institutional policy...
```

Anti-pattern: Pasting the entire raw conversation history into a new session — it wastes tokens and the AI can't distinguish important decisions from casual chatter.

**Relationship to core techniques:** T23 is the information-management companion to T22. T22 captures the handoff state at a point in time; T23 compresses the full history into reusable context. Together they solve the cross-session memory problem.

---

## Multi-Modal Coordination (T24)

### T24 · Modal Sync (模态同步)
**Whenever one modality changes (text, data, visuals, code), explicitly check whether other modalities need updating.**

Use when: Your project involves multiple output types — a document + a chart, a policy + a visualization, a dataset + a report, code + documentation. Any time you make a significant change to one modality.

How to do it: After any major change, run a sync check:
```
"I just updated [text/data/visual/code]. Check if any of these need updating as a result:
- [ ] Charts/diagrams — do they still reflect the current data/structure?
- [ ] Supporting documents — do they reference the old version?
- [ ] Code/formulas — do they use outdated assumptions?
- [ ] Visual layouts — do they match the current content hierarchy?"
```

Example: After rewriting the org structure from 3 tiers to flat, ask: "I changed the org structure. Does the org chart HTML still match? Does the evaluation framework still reference 'tier-based' roles? Does the compensation model still assume reporting layers?"

Anti-pattern: Updating the main document and assuming everything else automatically adjusts. It doesn't. Charts still show old data, code still uses old variables, visuals still reflect the old structure.

**Relationship to core techniques:** T24 is the multi-modal extension of T17 (sync supporting files). T17 syncs text documents with each other; T24 syncs across fundamentally different output types (text ↔ data ↔ visual ↔ code).

---

## Cognitive Self-Management (T25)

### T25 · Sunk Cost Checkpoint (沉没成本检查点)
**At regular intervals, deliberately ask yourself: "If I saw this project for the first time today, would I still choose the current direction?"**

Use when: You've invested 5+ versions into a direction and feel reluctant to change course even though something feels off. Also useful as a scheduled checkpoint every 3-5 major iterations.

How to do it: Pause the iteration and prompt:
```
"Pretend you've never seen this project before. I'm going to show you the current version.
Read it fresh. Then answer honestly:
1. What's the strongest aspect of this approach?
2. What would you do completely differently if starting from scratch?
3. Is there a simpler way to achieve the same goal?
Don't be polite. Be honest."
```

The key insight: if what AI "would do differently" overlaps with your own nagging doubts, that's a strong signal you're clinging to a direction because of sunk cost, not because it's the best path.

When to act: If the "do differently" answer describes a fundamentally different approach, seriously consider a version leap (T08) or running Navigate (Mode 4) to explore alternatives. The courage to throw things away is the single most important skill in iteration.

Example: On v5 of a business plan, after weeks of work: "Read this fresh. If you were an advisor seeing this for the first time, what would you tell the founder to change?" → AI says "the revenue model is the weakest part" → you realize you've been avoiding that because it would require rewriting 3 chapters.

Anti-pattern: Never questioning the overall direction because you've "already put so much work in." This is the #1 way talented iterators produce mediocre outcomes — they optimize a local maximum instead of searching for the global one.

**Relationship to core techniques:** T25 addresses the psychological blind spot that T12 (proactive blind spot discovery) can't reach. T12 finds gaps in the content; T25 finds gaps in your judgment caused by emotional attachment to prior work.

---

## Quick Reference Card

| # | Name | One-liner | Category |
|---|------|-----------|----------|
| T20 | Delegation Prompt | Write a task brief for handoff | Collaboration |
| T21 | Review Protocol | AI role-plays a specific stakeholder to review | Collaboration |
| T22 | Session Handoff | Generate a state snapshot before ending a session | Memory |
| T23 | Context Compression | Compress conversation history into structured layers | Memory |
| T24 | Modal Sync | Check cross-modality consistency after changes | Multi-Modal |
| T25 | Sunk Cost Checkpoint | "Would I still choose this direction if I started today?" | Cognitive |
