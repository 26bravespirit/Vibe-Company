# Scene → Technique Mapping

When coaching a user, first identify their project type, then recommend the most relevant technique subset.

## Mapping Table

| Scene | Top Techniques | Applicability | Key Coaching Focus | Navigate Emphasis |
|-------|---------------|--------------|-------------------|-------------------|
| **Organizational Design** | T01, T06, T07, T08, T10, T11 | 19/19 (100%) | Version leaps + institutional convergence | A1 Purpose, A2 Constraints, B1 Cross-domain |
| **Business Plan / BP** | T07, T08, T09, T10, T11 | 17/19 (89%) | Expand-contract + external benchmarking | A4 Value Chain, A5 End-State, B2 Extreme |
| **Product PRD** | T03, T06, T07, T11, T15 | 18/19 (95%) | Preview before execute + evaluate-improve | A3 Simplification, B3 Perspective Flip, B5 Combinatorial |
| **Strategic Planning** | T08, T09, T10, T11, T12 | 17/19 (89%) | Version leaps + blind spot discovery | A5 End-State, A1 Purpose, B4 Inversion |
| **Investment Analysis** | T09, T11, T14, T19 | 16/19 (84%) | Three-perspective + multi-dimensional scoring | A2 Constraints, B2 Extreme, B3 Perspective |
| **Market Research** | T06, T09, T11, T19 | 14/19 (74%) | Evaluate-improve on conclusions + benchmarking | A4 Value Chain, B1 Cross-domain, B3 Perspective |
| **Technical Architecture** | T01, T06, T08, T11, T16 | 16/19 (84%) | Paradigm-level instructions + critical review | A3 Simplification, A2 Constraints, B2 Extreme |
| **Brand Strategy** | T03, T07, T11, T14 | 15/19 (79%) | Preview (visual proposals) + expand-contract | B1 Cross-domain, B5 Combinatorial, A1 Purpose |
| **Content Creation (long-form)** | T04, T05, T07, T08, T16 | 14/19 (74%) | Prompt-as-content + expand-contract | A1 Purpose, B3 Perspective Flip, B4 Inversion |
| **Interview/Assessment Design** | T06, T09, T11, T14 | 16/19 (84%) | Three-perspective + framework building | A4 Value Chain, B4 Inversion, B3 Perspective |
| **Competitive Analysis** | T09, T11, T19 | 13/19 (68%) | External benchmarking + multi-dimensional scoring | B2 Extreme, B1 Cross-domain, A5 End-State |
| **Legal Document Review** | T03, T15, T16 | 11/19 (58%) | Preview + incremental correction | A3 Simplification, A2 Constraints, B4 Inversion |

The **Navigate Emphasis** column shows which direction engines are most productive for each scene type. All 10 engines always run, but the listed ones tend to generate the strongest directions for that domain.

## Applicability Threshold

- **★★★★★ (>85%)**: Full coaching — recommend the complete 5-step core loop
- **★★★★☆ (70-85%)**: Active coaching — focus on the most relevant technique subset
- **★★★☆☆ (55-70%)**: Light coaching — suggest 3-5 specific techniques
- **★★☆☆☆ (<55%)**: Not a good fit for this skill — recommend simpler approaches
- **★☆☆☆☆ (single-turn)**: Do not use this skill

## Phase Recommendations by Scene Type

### High-complexity scenes (org design, strategy, BP)
```
Phase 1: Foundation    → T01 (paradigm instruction) + T09 (benchmark)
Phase 2: Expansion     → T07 (expand) + T11 (three perspectives)
Phase 3: Critique      → T06 (evaluate-improve) + T12 (blind spots) + T21 (role review)
Phase 3.5: Reduction   → Mode 6 (reduction check before selection — quantify what to cut)
Phase 4: Selection     → T14 (choose don't accept) + T08 (version leap if needed)
Phase 5: Convergence   → T10 (institutionalize) + T16 (verify) + T17 (sync)
Phase 6: Handoff       → T22 (session handoff) + T24 (modal sync if multi-modal)
```

### Medium-complexity scenes (product PRD, tech arch, brand)
```
Phase 1: Draft         → T03 (preview) + T01 (paradigm if complex)
Phase 2: Iterate       → T15 (incremental) + T07 (expand-contract)
Phase 2.5: Reduction   → Mode 6 (if 3+ expand rounds without contraction)
Phase 3: Validate      → T06 (evaluate) + T09 (benchmark) + T21 (stakeholder review)
Phase 4: Deliver       → T16 (verify) + T24 (modal sync) + T05 (format separately)
```

### Analysis-heavy scenes (investment, market research, competitive)
```
Phase 1: Frame         → T11 (three perspectives) + T09 (benchmark)
Phase 2: Deep-dive     → T06 (evaluate-improve on findings)
Phase 3: Quantify      → T19 (multi-dimensional scoring)
Phase 4: Conclude      → T14 (explicit choices) + T16 (verify)
```
Note: Analysis-heavy scenes are less prone to over-design. Run Mode 6 only if the analysis framework itself grows beyond 3 scoring dimensions.

### Cross-session projects (any type spanning multiple sessions)
```
Every session start  → T23 (compress previous context) + T22 (read last handoff)
Every 3-5 versions   → T25 (sunk cost checkpoint) + Mode 6 (reduction check)
Every handoff        → T20 (delegation prompt if involving others)
Every session end    → T22 (generate session handoff)
```
