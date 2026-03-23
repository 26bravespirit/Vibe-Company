# 19 Vibe Iteration Techniques — Full Reference

## Prompt Design Techniques (T01-T05)

### T01 · Paradigm-Level Instructions
**One prompt to redefine the entire framework's foundation — not tweaking a detail, but resetting the underlying logic.**

Use when: The current direction needs a fundamental reset, not incremental adjustment.
Example: "Simplify all job titles into two categories: Member (value creators) and Role (service providers). Members are flat and equal, Roles serve Members."

Anti-pattern: Making 20 small edits when what you really need is to throw out the framework and start fresh.

### T02 · Precise Batch Operations
**Multiple specific edits in a single instruction, each precise to location.**

Use when: You know exactly what needs changing across multiple locations.
Example: "Add a column to tables 4.1 and 4.2. Delete the evaluation method from sections 6.2 and 6.3. Remove chapters 7, 8, and 9."

Anti-pattern: Sending one edit per message when you could batch them.

### T03 · Preview Before Execute
**Always let AI show the plan/draft before executing changes.**

Use when: The change is significant enough that you want to verify direction before committing.
Example: "Give me two naming schemes for these roles — don't modify the file yet, just show me the options."

Anti-pattern: Saying "just do it" on a major structural change without seeing AI's interpretation first.

### T04 · Prompt-As-Content
**When you've figured it out, write the actual content as your prompt and have AI format it.**

Use when: You know exactly what the final document should say and AI's job is just formatting/structuring.
Example: Providing the complete v4 document text and saying "Generate this as a formatted md file."

Anti-pattern: Asking AI to "write a document about X" when you already have the exact content in your head.

### T05 · Separate Content from Format
**First get the content right, then decide on presentation format.**

Use when: The project has both content development and formatting/visualization needs.
Example: First iterate on the org architecture md → then "make this into an HTML with my brand colors."

Anti-pattern: Asking for "a beautiful HTML about org design" when you haven't finalized what the org design actually is.

---

## Iteration Strategy Techniques (T06-T10)

### T06 · Evaluate-Improve Loop
**After completing a major version, stop and let AI attack your own work. Extract improvement directions from the attack.**

Use when: You've just completed a significant milestone (a full version, a major section, a complete draft).
Example: "Evaluate this v4 document. Emphasize critical tensions and reveal risk gaps."

Anti-pattern: Endlessly building without ever stopping to critique. Or only asking AI to praise your work.

### T07 · Expand-Contract Rhythm
**First add everything (expand possibilities), then ruthlessly cut to essentials (contract).**

Use when: You're building something complex that needs both breadth exploration and focused delivery.
Example: First add role-play mechanism + meta-competency framework (expand) → then delete three entire chapters that don't belong (contract).

Anti-pattern: Only expanding (feature creep) or only contracting (never exploring alternatives).

### T08 · Version Leaps
**At critical junctures, make paradigm-level jumps instead of incremental tweaks — skip from A to C.**

Use when: Incremental changes aren't working and the fundamental model needs rethinking.
Example: v2 (three-layer hierarchy) → v3 (Member & Role flat system). Not a tweak — a complete paradigm shift.

Anti-pattern: Making 50 tiny edits to fix something that needs a wholesale rethinking. Courage to throw things away is key.

**Navigate connection:** Mode 4 (Navigate) is the systematic way to execute T08. When a user needs a version leap but doesn't know where to leap TO, Navigate generates 10 concrete directions using first-principles and creative engines. Think of Navigate as "T08 with a compass."

### T09 · External Benchmarking
**Bring in real-world best practices as evaluation baselines — don't design in a vacuum.**

Use when: You need objectivity about whether your approach is good, or inspiration for how others solve the same problem.
Example: "Research Anthropic's organizational structure as a benchmark, then compare against our v2."

Anti-pattern: Designing everything from first principles without checking what already works in the real world.

### T10 · Converge to Institution
**Turn exploratory documents into formal, executable policy.**

Use when: The exploration phase is over and you need something people can actually follow.
Example: "Write an institutional policy document — no explanations, just definitions. 33 articles."

Anti-pattern: Leaving everything as informal discussion documents that nobody can implement.

---

## Thinking Method Techniques (T11-T15)

### T11 · Three-Perspective Analysis
**Require AI to analyze the same problem from three angles: creative / first-principles / long-term reliable.**

Use when: Facing a complex decision where no single lens gives the full picture.
Example: "Analyze this problem from: 1) a creative solution, 2) a first-principles solution, 3) a long-term reliable solution."

Why three: Creative pushes for novelty. First-principles pushes for logical soundness. Long-term reliable pushes for sustainability. Together they squeeze maximum quality from AI's reasoning.

Anti-pattern: Accepting AI's first answer without asking it to consider the problem from multiple angles.

**Navigate connection:** Mode 4's A-group and B-group are an evolved form of multi-perspective analysis — A-group uses first-principles depth, B-group uses creative breadth. Together they cover more ground than the original three perspectives, specifically for the "where to go next" question.

### T12 · Proactive Blind Spot Discovery
**Find gaps in your framework BEFORE AI does — then ask AI to analyze and solve them.**

Use when: You sense something is missing but can't quite articulate it. Or when you notice something the AI's critique didn't catch.
Example: "The current architecture only empowers product creation but ignores the relationship-building and talent-acquisition work. Analyze this blind spot."

Why this matters: The most valuable blind spots are the ones AI doesn't find — they require the human's domain intuition.

### T13 · Extract Concepts from AI's Answers
**Capture ideas that AI generates in passing and elevate them to core design principles.**

Use when: AI says something insightful as a side note in a larger response.
Example: AI mentioned "Role is a hat, not a chair" in a dispute resolution analysis → user extracted this and made it the core metaphor for v6.

Anti-pattern: Ignoring everything in AI's response except the direct answer to your question.

### T14 · Choose, Don't Accept
**When AI gives multiple options, make an explicit selection with stated reasoning — never default to option 1.**

Use when: AI presents alternatives (naming schemes, solution approaches, design options).
Example: "I choose Option B (verb-based naming). The reasons are..."

Anti-pattern: Saying "ok, go with your recommendation" without evaluating alternatives yourself.

### T15 · Incremental Correction
**Change one thing at a time, confirm it works, then move to the next.**

Use when: Multiple issues exist but they interact — fixing them all at once risks cascading confusion.
Example: v6's three sequential updates: add hat-priority principle → delete safety valve → delete example section.

Anti-pattern: "Fix all of these 10 things in one go" — then not knowing which change caused which effect.

---

## Quality Control Techniques (T16-T19)

### T16 · Verify Before Deliver
**Require AI to do a logic consistency check before generating the final version.**

Use when: A major version is about to be created and you want to catch inconsistencies first.
Example: "Before generating v7, check all chapters against the new MoR principles. Give me a verification report. Only generate v7 if verification passes."

Anti-pattern: Going straight from design to final output without a verification step.

### T17 · Sync Supporting Files
**After any version upgrade, ensure ALL related documents are updated — no dangling inconsistencies.**

Use when: The main document has changed and supporting files might reference outdated concepts.
Example: "Update all supporting documents to v7 and rename version numbers."

Anti-pattern: Upgrading the main document but leaving supporting policies, evaluation criteria, and visualizations on the old version.

### T18 · Track and Trace
**Proactively generate change logs, version evolution diagrams, and prompt audit trails.**

Use when: The project has gone through multiple iterations and you need to maintain traceability.
Example: "Generate a version evolution tracking diagram from v2 to v6 with all changes mapped chronologically."

Anti-pattern: Not keeping any record of what changed and why — making it impossible to understand the rationale for current design choices.

### T19 · Multi-Dimensional Scoring Validation
**Apply the same scoring framework under different premises to verify that improvements actually worked.**

Use when: You've made changes and want to objectively measure whether they improved things.
Example: Score 11 companies on 20 dimensions → make improvements → re-score under "AI disruption" premise → compare before/after.

Anti-pattern: Claiming improvement without measuring it, or measuring with a framework that can't detect the type of improvement you made.
