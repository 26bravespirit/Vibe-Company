# Technique Finder — 症状→技巧诊断映射

Mode 5 (Toolkit) helps users who are mid-iteration and can't figure out which technique to use. Instead of requiring users to memorize 25 techniques, it works like a symptom checker: describe what's happening → get 2-3 techniques that fit.

## Table of Contents
- [Symptom Map: 17 Common Pain Points](#symptom-map)
- [Core Loop Position Detection](#core-loop-position)
- [Technique Combination Patterns](#combination-patterns)
- [Anti-Pattern Detection](#anti-pattern-detection)

---

## Symptom Map

Each symptom maps to 2-3 techniques ranked by relevance. The coach should identify which symptom best matches the user's situation, then prescribe the top technique with a concrete "do this now" action.

### S01 · "AI keeps misunderstanding what I want"
**Root cause:** Prompt isn't structured at the right abstraction level.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T01 Paradigm-level instructions | You're probably making small edits when you need to restate the whole framework | Rewrite your intent as a single paradigm sentence: "The core concept is X, structured as Y, where Z" |
| ★★ | T03 Preview before execute | AI might be executing before you've aligned on direction | Add "Show me your plan before making changes" to your next prompt |
| ★ | T02 Precise batch operations | If the issue is scattered edits, batch them precisely | List every change with exact locations in one prompt |

### S02 · "I've been going back and forth without progress"
**Root cause:** Stuck in the ①→②→①→② loop — proposing and stressing without extracting or deciding.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T14 Choose, don't accept | You're cycling because you haven't committed to a direction | Stop and say: "Of the options we've discussed, I choose X because Y" |
| ★★ | T06 Evaluate-improve loop | You need to step back and critique what you have | Ask AI: "Attack the current version. What are the 3 biggest weaknesses?" |
| ★ | T08 Version leaps | Maybe small edits can't fix this — you need a paradigm jump | Ask: "If I threw this away and started fresh, what would I build differently?" |

### S03 · "The output feels mediocre but I can't pinpoint why"
**Root cause:** Single-perspective thinking — you haven't examined it from enough angles.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T11 Three-perspective analysis | Mediocrity comes from optimizing one dimension while ignoring others | Ask AI to analyze from 3 angles: creative / first-principles / long-term reliable |
| ★★ | T09 External benchmarking | You have no reference point for "good" | Ask: "Find 3 real-world examples of excellent [X] and compare against my version" |
| ★ | T12 Proactive blind spot discovery | The problem might be something you haven't even considered | List everything your project addresses, then ask: "What important aspects are NOT on this list?" |

### S04 · "The project keeps growing and I can't control the scope"
**Root cause:** All expand, no contract. Missing the contraction half of the rhythm.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T07 Expand-contract rhythm | Time to ruthlessly cut — you've been expanding too long | Say: "We've explored enough. Cut everything that isn't essential. Be brutal." |
| ★★ | T10 Converge to institution | Turn the best ideas into fixed, formal decisions | Pick the 3 most important conclusions and say: "Write these as policy statements" |
| ★ | T05 Separate content from format | You might be conflating content decisions with formatting decisions | Stop worrying about how it looks. Ask: "What are the 5 core points, stripped of all presentation?" |

### S05 · "I have the content right but it doesn't look professional"
**Root cause:** Content and format are entangled, or format hasn't been addressed yet.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T05 Separate content from format | Time to package the content into its final form | Say: "The content is finalized. Now format this as [target format] with [style requirements]" |
| ★★ | T04 Prompt-as-content | If you know exactly what you want, write it yourself and have AI format | Write the actual final text, then say: "Format this exactly as written into [format]" |
| ★ | T16 Verify before deliver | Before formatting, make sure the content is truly consistent | Ask: "Check all sections for logical consistency before we format" |

### S06 · "I'm worried this has gaps I haven't thought of"
**Root cause:** Insufficient critical examination of the work.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T12 Proactive blind spot discovery | Trust your intuition — if you feel gaps exist, they do | List 3 areas where you feel least confident, then ask AI to deep-dive each |
| ★★ | T06 Evaluate-improve loop | Get AI to systematically attack the whole thing | Say: "Pretend you're a hostile reviewer. Find every weakness in this document." |
| ★ | T11 Three-perspective analysis | Gaps often hide in the angle you haven't considered | Ask for analysis from a perspective you haven't used yet |

### S07 · "AI gave me a great idea but I lost it in the conversation"
**Root cause:** Not capturing emergent insights.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T13 Extract concepts from AI's answers | This is exactly what this technique is for | Go back, find the idea, and say: "I want to elevate this into a core principle: [the idea]" |
| ★★ | T18 Track and trace | You need a system to prevent this in the future | Ask: "Generate a running log of all key decisions and insights from this session" |
| ★ | T17 Sync supporting files | If the idea matters, it needs to be reflected across all documents | After extracting it, say: "Update all related documents to include this new principle" |

### S08 · "I just finished a big version, now what?"
**Root cause:** Transition point — need to decide whether to refine or leap.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T06 Evaluate-improve loop | First, understand what you've built | Say: "Score this version on [relevant criteria]. What's the biggest gap?" |
| ★★ | T08 Version leaps | If the evaluation reveals fundamental issues, leap | Consider: does this need refinement or a paradigm shift? |
| ★ | Navigate (Mode 4) | If you need direction for the NEXT major version | Switch to Mode 4 to generate 10 directions |

### S09 · "Multiple things are wrong and I don't know where to start"
**Root cause:** Trying to fix everything at once, creating cascading confusion.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T15 Incremental correction | One change at a time, confirm it works, then next | Pick the single most important issue. Fix only that. Verify. Then move on. |
| ★★ | T03 Preview before execute | Make sure each fix is correct before applying | For each change, say: "Show me what this change would look like before applying it" |
| ★ | T16 Verify before deliver | After each fix, check it didn't break something else | After each change: "Check if this change is consistent with everything else" |

### S10 · "I'm not sure if this is actually good or I've just been staring at it too long"
**Root cause:** Lost objectivity from being too close to the work.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T09 External benchmarking | Get an objective reference point outside your own work | Ask: "Compare this against the best real-world examples of [X]. Where does mine fall short?" |
| ★★ | T19 Multi-dimensional scoring | Quantify quality instead of relying on gut feeling | Create a scoring rubric, then ask AI to score your work on each dimension |
| ★ | T11 Three-perspective analysis | Look at it from angles you haven't tried | Ask: "If this were reviewed by [a very different stakeholder], what would they say?" |

### S11 · "The supporting documents don't match the main document anymore"
**Root cause:** Main document evolved but supporting files are stale.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T17 Sync supporting files | This is exactly the problem this technique solves | Say: "List all supporting documents and flag any inconsistencies with the main document" |
| ★★ | T18 Track and trace | Prevent this from recurring | Ask: "Create a version map showing which documents need updating when the main doc changes" |
| ★ | T16 Verify before deliver | Make sure the sync is complete | After syncing: "Verify all documents are consistent with each other" |

### S12 · "I know what I want but can't explain it to AI"
**Root cause:** The gap between intention and expression.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T04 Prompt-as-content | Skip the meta-instruction — just write the content yourself | Instead of describing what you want, write a rough version of the actual output |
| ★★ | T01 Paradigm-level instructions | Zoom out and define the paradigm, not the details | State the one core principle that governs everything, then let AI derive the details |
| ★ | T03 Preview before execute | Use iteration to close the gap | Say: "Here's a rough sketch of what I mean: [sketch]. Show me your interpretation before proceeding" |

### S13 · "I'm continuing from yesterday but the AI lost all context"
**Root cause:** No handoff protocol between sessions.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T22 Session Handoff | You need a state snapshot to restore context | Before ending ANY session from now on, generate a handoff doc: current state + decisions + open questions + next action |
| ★★ | T23 Context Compression | The old conversation was too long to paste | Compress the previous conversation into 3 layers: Core Decisions / Rationale Map / Evolution Log. Paste Layer 1 into the new session. |
| ★ | T18 Track and trace | Prevent this from recurring | Create a running decision log file that persists across sessions |

### S14 · "I need someone else to review this but they have no context"
**Root cause:** Knowledge is trapped in your head and the conversation history.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T20 Delegation Prompt | Write a structured brief that transfers your context | Write a 5-field brief: Current state / Goal / Constraints / Context / First action |
| ★★ | T21 Review Protocol | If no one is available, simulate the review with AI | Say: "Act as [the person who will review this]. What would they flag?" |
| ★ | T23 Context Compression | Give the reviewer a compressed history | Generate a 3-layer summary they can skim in 2 minutes |

### S15 · "I updated the text but now the charts/code/data are wrong"
**Root cause:** Cross-modality drift — one output type changed, others didn't follow.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T24 Modal Sync | This is exactly the problem this technique solves | Run a sync check: "I changed [X]. Check if charts, code, data, and supporting docs still match." |
| ★★ | T17 Sync supporting files | If it's just documents, not mixed modalities | Say: "List all files and flag any that reference the old version of [X]" |
| ★ | T16 Verify before deliver | Final consistency check across everything | Before any delivery: "Verify all outputs are mutually consistent" |

### S16 · "I feel like I've invested too much to change direction now"
**Root cause:** Sunk cost bias — emotional attachment to prior work overriding rational assessment.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | T25 Sunk Cost Checkpoint | This is the core technique for this exact problem | Prompt: "Pretend you've never seen this. Read it fresh. What would you do completely differently?" |
| ★★ | T08 Version leaps | If the checkpoint confirms you need a new direction, leap | Ask: "If I started from scratch with what I know now, what would I build?" |
| ★ | Navigate (Mode 4) | If you need structured alternatives | Switch to Mode 4 to generate 10 fresh directions |

### S17 · "The output keeps getting more complex but doesn't feel more valuable"
**Root cause:** Iteration is adding complexity without adding value — classic over-saturation signal.
| Priority | Technique | Why | Do This Now |
|----------|-----------|-----|-------------|
| ★★★ | Reduction Check (Mode 6) | You need a quantitative saturation assessment, not guesswork | Switch to Mode 6: "Run a reduction check on this. I think it's over-designed." |
| ★★ | T07 Expand-contract rhythm | If Mode 6 confirms saturation, you need an aggressive contraction phase | After Mode 6 scores, cut everything rated 🟠 or 🔴 |
| ★ | T01 Paradigm-level instructions | If saturation index > 50, rewrite the core framework from scratch | Restate the entire project in one paradigm sentence, then rebuild only what that sentence demands |

---

## Core Loop Position Detection

When the user describes their situation, map it to the 5-step core loop to diagnose where they are and what they're missing:

```
Position → Missing Step → Likely Symptom → Technique

Stuck at ① PROPOSE
  → Can't form a clear direction
  → S12 "can't explain it" or S02 "going in circles"
  → T01, T04, or Navigate (Mode 4)

Stuck at ② STRESS
  → Not getting useful pushback from AI
  → S03 "feels mediocre" or S06 "worried about gaps"
  → T06, T11, T12

Skipping ③ EXTRACT
  → Good AI responses but insights aren't captured
  → S07 "lost a great idea"
  → T13, T18

Skipping ④ DECIDE
  → Lots of exploration but no commitment
  → S02 "back and forth" or S04 "scope keeps growing"
  → T14, T07, T10

Skipping ⑤ VERIFY
  → Decisions made but not checked for consistency
  → S09 "multiple things wrong" or S11 "docs don't match"
  → T16, T17, T19
```

---

## Technique Combination Patterns

Some techniques work powerfully in sequence. When prescribing, suggest the combo if the timing is right:

| Pattern | Sequence | When to use |
|---------|----------|-------------|
| **Critique Sandwich** | T06 → T12 → T11 | After completing a major section — attack it, find blind spots, then multi-angle review |
| **Precision Strike** | T03 → T02 → T15 | When making multiple targeted edits — preview, batch, then verify incrementally |
| **Reset & Rebuild** | T01 → T08 → T14 | When incremental changes aren't working — paradigm reset, version leap, then commit |
| **Ship It** | T16 → T17 → T05 | Final delivery — verify consistency, sync all files, then format for presentation |
| **Direction Finding** | T06 → Navigate → T14 | Between major versions — evaluate current, explore 10 directions, choose and commit |
| **Session Bridge** | T23 → T22 → T20 | Across sessions — compress history, generate handoff, write brief for next session/person |
| **Stakeholder Gauntlet** | T21 → T21 → T21 → T13 | Before major presentations — run 3 role-reviews sequentially, extract insights from each |
| **Reality Check** | T25 → T09 → T11 | When stuck in a local maximum — sunk cost checkpoint, benchmark against external, multi-angle reassessment |
| **Controlled Demolition** | Mode 6 → T07 → T01 | When over-saturated — quantify the problem, contract aggressively, then rewrite core framework |

---

## Anti-Pattern Detection

If you notice the user exhibiting these patterns, proactively flag them and prescribe the antidote:

| Anti-pattern | Signal | Antidote |
|-------------|--------|----------|
| **Acceptance Loop** | User says "ok" or "sounds good" to everything AI suggests | T14 — insist they make an explicit choice with reasoning |
| **Infinite Expand** | 5+ turns of adding new ideas without cutting anything | T07 (contract phase) — "time to cut ruthlessly" |
| **Perfectionism Spiral** | Tweaking the same section for 3+ turns with diminishing returns | T08 — suggest a version leap or T05 — move to formatting |
| **Blind Trust** | User never questions AI's output | T06 + T12 — request an attack on the work |
| **Context Amnesia** | User repeats instructions AI already received | T18 — create a shared context log |
| **Format Fixation** | Spending time on visual formatting before content is stable | T05 — separate content from format, content first |
| **Session Amnesia** | Starting a new session without any context from the previous one | T22 + T23 — generate handoff before ending, compress before starting |
| **Solo Tunnel Vision** | Never getting external perspective on the work, even simulated | T21 — run at least one role-review per major version |
| **Complexity Ratchet** | Every iteration adds new concepts/rules but never removes any | Mode 6 — run a reduction check; the one-way ratchet is the #1 cause of over-saturation |
