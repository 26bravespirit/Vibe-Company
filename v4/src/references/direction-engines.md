# Direction Engines — 双引擎方向生成参考

Mode 4 (Navigate) uses two engines to generate 10 candidate directions for the user's next major version. The two engines are deliberately different in thinking style — one goes deep, the other goes wide. This tension is by design: it forces the user to consciously choose between "digging into essentials" and "breaking out of the box."

## Table of Contents
- [Engine A: First Principles (第一性原理)](#engine-a-first-principles)
- [Engine B: Creative Drive (创意驱动)](#engine-b-creative-drive)
- [Generation Guidelines](#generation-guidelines)
- [Example: Organizational Design v3→v4](#example)

---

## Engine A: First Principles

First principles thinking strips away all inherited assumptions and rebuilds from the ground truth. Each direction follows the pattern: "What is the fundamental purpose? → What assumptions are we making? → What happens if we remove them?"

### A1 · Purpose Regression (目的回溯)

**Core question:** "What problem is this project ultimately solving? Is the current version solving the real problem, or just a symptom?"

How to generate this direction:
1. Identify the stated goal of the current version
2. Ask "why does that matter?" 3 times (the 3-why chain) to reach the root purpose
3. Compare the root purpose against what the current version actually optimizes for
4. If there's a gap, the direction is: realign the project around the root purpose

**Signals this direction is relevant:** The project has grown complex and may have drifted from its original intent. Features have accumulated but the "why" is fuzzy.

### A2 · Constraint Reexamination (约束重审)

**Core question:** "Which constraints in the current design are real (physics, law, budget) and which are assumed?"

How to generate this direction:
1. List all implicit constraints in the current version (format, scope, audience, technology, process)
2. For each constraint, ask: "Is this truly immovable, or is it just how we've always done it?"
3. Identify 1-2 constraints that, if removed, would open entirely new solution spaces
4. The direction is: redesign assuming those constraints don't exist

**Signals this direction is relevant:** The user says "we can't do X because..." or the current version has obvious limits that nobody has questioned.

### A3 · Structural Simplification (结构简化)

**Core question:** "Can the same (or better) result be achieved with dramatically fewer moving parts?"

How to generate this direction:
1. Count the major components/concepts/layers in the current version
2. Identify which components carry the core value vs. which are supporting or decorative
3. Propose a version that achieves the same core value with 50-70% fewer components
4. The direction is: radical simplification without losing essential capability

**Signals this direction is relevant:** The current version feels "heavy" — too many categories, too many rules, too many exceptions. Complexity is creating confusion or maintenance burden.

### A4 · Value Chain Focus (价值链聚焦)

**Core question:** "Where in this project does 80% of the value get created, and are we spending 80% of our effort there?"

How to generate this direction:
1. Map the value chain: which parts of the project directly create the core outcome?
2. Identify effort allocation: where is time/attention actually being spent?
3. Find the mismatch: usually effort is spread evenly but value is concentrated
4. The direction is: ruthlessly cut low-value parts and double down on high-value nodes

**Signals this direction is relevant:** The project has many sections/features of roughly equal weight, but intuitively some matter much more than others.

### A5 · End-State Backcast (终局倒推)

**Core question:** "If this project were in its ideal final state 3-5 years from now, what would it look like? What's the biggest gap between now and then?"

How to generate this direction:
1. Ask the user (or infer from context) what success looks like at full maturity
2. Describe that end state concretely
3. Compare against the current version to identify the biggest structural gap
4. The direction is: build the bridge that closes that specific gap

**Signals this direction is relevant:** The current version works for now but clearly isn't the long-term answer. The user has a vision but hasn't connected it to the current iteration.

---

## Engine B: Creative Drive

Creative thinking deliberately breaks conventional patterns. Each direction follows the pattern: "What if we looked at this from a completely different angle? → What would that reveal? → How can we use that insight?"

### B1 · Cross-Domain Transplant (跨界移植)

**Core question:** "What mechanism from a completely different field could solve a problem we're stuck on?"

How to generate this direction:
1. Identify the core challenge in the current version (what's not working or could be better)
2. Search for analogous challenges in unrelated domains (biology, gaming, urban planning, music, open source, sports, cuisine...)
3. Find a domain where this type of challenge has been elegantly solved
4. Describe how to transplant that mechanism into the current project

**Source domains to consider:** evolutionary biology (adaptation, selection), game design (incentive loops, progression), open source communities (governance without hierarchy), music (composition, rhythm, harmony), urban planning (zoning, flow), restaurant kitchens (brigade system, mise en place), improv theater (yes-and, scene work).

### B2 · Extreme Hypothesis (极端假设)

**Core question:** "What happens if we push a key variable to its extreme — 100x scale, zero budget, opposite audience?"

How to generate this direction:
1. Pick 1-2 key variables in the current version (scale, resources, audience, timeline, scope)
2. Push each to an extreme (100x, 0, inverted)
3. Analyze what breaks and what surprisingly still works
4. The direction is: fix what breaks under the extreme, because it reveals hidden fragility

**Useful extremes to try:** "What if 100x users?", "What if zero budget?", "What if the timeline is 1 week instead of 6 months?", "What if the target audience is the exact opposite of who we designed for?", "What if we had to explain this to a 5-year-old?"

### B3 · Perspective Flip (用户视角翻转)

**Core question:** "How does this project look from a stakeholder we haven't considered — or one who actively opposes it?"

How to generate this direction:
1. List all stakeholders currently considered in the design
2. Identify stakeholders NOT considered: critics, competitors, end-users' families, future maintainers, regulators, the person who has to clean up if this fails
3. Adopt the most revealing outsider perspective
4. The direction is: address the blind spot that perspective reveals

**Perspectives to try:** "The harshest critic", "A 5-year-old", "The competitor who wants to copy this", "The person who inherits this project in 2 years", "The user who will use this wrong", "Someone from a completely different culture."

### B4 · Inversion Design (反向构建)

**Core question:** "Instead of asking how to make this succeed, how would we guarantee it fails? Then invert."

How to generate this direction:
1. Brainstorm: "What would make this project definitely fail?" (list 5-7 failure modes)
2. Rank by likelihood and severity
3. Take the top 2-3 failure modes and invert them into design principles
4. The direction is: build the inversion into the next version as a core safeguard

**Why this works:** Our brains are better at spotting danger than imagining success. By explicitly listing failure modes, we surface risks that positive thinking overlooks.

### B5 · Combinatorial Innovation (组合创新)

**Core question:** "What happens if we combine two things that don't usually go together?"

How to generate this direction:
1. List the major modules/components in the current version
2. List external elements not currently in the project (AI, community, gamification, subscription model, real-time data, physical artifacts, rituals...)
3. Try unexpected pairings: combine an internal module with an external element, or combine two internal modules that currently don't interact
4. The direction is: implement the combination that produces the most interesting emergent behavior

**Combination patterns:** internal × internal (merge two separate features), internal × external (add AI / community / gamification to an existing module), paradigm × paradigm (apply subscription thinking to a one-time deliverable, or apply open-source governance to a private project).

---

## Generation Guidelines

When generating the 10 directions for a specific user project:

1. **Specificity over generality.** Each direction must be specific enough that the user can immediately say "yes, I want to explore that" or "no, that's not right." "Improve user experience" is not a direction. "Reorganize the information architecture around task flows instead of feature modules" is.

2. **Grounded in the current version.** Every direction should reference specific elements of the user's actual project — section names, concepts, structures they've built. Generic directions that could apply to any project are not useful.

3. **Honest difficulty and potential.** Rate each direction's implementation difficulty (⭐ to ⭐⭐⭐⭐⭐) and breakthrough potential (🔥 to 🔥🔥🔥🔥🔥). Don't inflate — a direction that's easy to implement and has modest impact should be rated as such.

4. **No ranking, no recommendation.** Present all 10 directions as equals. The coach must not say "I recommend A2" or "A1 is the best option." The choice belongs to the user (T14).

5. **Highlight the tension.** A-group directions tend toward simplification, focus, and depth. B-group directions tend toward expansion, novelty, and breadth. Briefly note this structural tension in the output so the user understands they're choosing between two thinking modes, not just ten random ideas.

---

## Example

**Project:** AI Startup Organizational Architecture, v3 completed (three-tier flat structure with 12 role definitions)

**A1 · Purpose Regression**
> v3 designs "organizational structure," but the root purpose of an organization is "getting the right information to the right person at the right time." Is v3 optimizing information flow, or just reporting relationships? Direction: rebuild around information flow as the core variable.
> Difficulty: ⭐⭐⭐ | Breakthrough: 🔥🔥🔥🔥

**A2 · Constraint Reexamination**
> v3 assumes "each person has exactly one fixed role." In an AI-native company where AI handles most execution, are role boundaries still necessary? Direction: design a fluid-role architecture where people compose capabilities dynamically.
> Difficulty: ⭐⭐⭐⭐ | Breakthrough: 🔥🔥🔥🔥🔥

**B1 · Cross-Domain Transplant (source: Linux kernel community)**
> The kernel community coordinates 10,000+ contributors without an "org chart" — it uses code ownership + trust chains. Direction: replace departmental belonging with project ownership as the primary organizational unit.
> Difficulty: ⭐⭐⭐⭐ | Breakthrough: 🔥🔥🔥🔥🔥

**B4 · Inversion Design**
> "How to guarantee this org fails?" → "Slow down every decision." Inversion: v4's core design principle should be "maximize decision velocity." Any structural element that adds decision latency needs a strong justification to survive.
> Difficulty: ⭐⭐⭐ | Breakthrough: 🔥🔥🔥🔥

_(Other 6 directions follow same format, each grounded in the specific v3 content)_
