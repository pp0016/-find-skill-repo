# Prompt Templates Reference

Full template library for prompt-forge v2.0 (Antigravity Edition). Read the relevant template when the user's task type matches. Do not load all templates at once — only the one you need.

## Table of Contents

| Template | Best For |
|----------|----------|
| [A — RTF](#template-a--rtf) | Simple one-shot tasks |
| [B — CO-STAR](#template-b--co-star) | Professional documents, business writing |
| [C — RISEN](#template-c--risen) | Complex multi-step projects |
| [D — CRISPE](#template-d--crispe) | Creative work, brand voice |
| [E — Guided Reasoning](#template-e--guided-reasoning) | Logic, math, analysis, debugging |
| [F — Few-Shot](#template-f--few-shot) | Consistent structured output, pattern replication |
| [G — ReAct + Stop Conditions](#template-g--react--stop-conditions) | Autonomous agentic tasks in Antigravity |
| [H — Prompt Decompiler](#template-h--prompt-decompiler) | Breaking down, adapting, or splitting existing prompts |
| [I — Opus 4.6 Task Brief](#template-i--opus-46-task-brief) | Complex, multi-step task on Claude Opus 4.6 |
| [J — Planning Trigger](#template-j--planning-trigger) | Tasks requiring Antigravity's planning mode |

---

## Template A — RTF

*Role, Task, Format. Use for fast one-shot tasks where the request is clear and simple.*

```
Role: [One sentence defining who the AI is]
Task: [Precise verb + what to produce]
Format: [Exact output format and length]
```

**Example:**
```
Role: You are a senior technical writer.
Task: Write a one-paragraph description of what a REST API is.
Format: Plain prose, 3 sentences maximum, suitable for a non-technical audience.
```

**Best model:** Gemini 3.1 High (fast, token-efficient for simple tasks).

---

## Template B — CO-STAR

*Context, Objective, Style, Tone, Audience, Response. Use for professional documents, business writing, reports, and marketing content where full context control matters.*

```
Context: [Background the AI needs to understand the situation]
Objective: [Exact goal — what success looks like]
Style: [Writing style: formal / conversational / technical / narrative]
Tone: [Emotional register: authoritative / empathetic / urgent / neutral]
Audience: [Who reads this — their knowledge level and expectations]
Response: [Format, length, and structure of the output]
```

**Example:**
```
Context: I am a founder pitching a B2B SaaS tool that automates expense reporting for mid-size companies.
Objective: Write a cold email that gets a reply from a CFO.
Style: Direct and conversational.
Tone: Confident but respectful.
Audience: CFO at a 200-person company, busy, skeptical of vendor emails.
Response: 5 sentences max. Subject line included.
```

**Best model:** Either — Gemini 3.1 for drafts, Opus 4.6 for polished final versions.

---

## Template C — RISEN

*Role, Instructions, Steps, End Goal, Narrowing. Use for complex projects, multi-step tasks, and any output that requires a clear sequence of actions.*

```
Role: [Expert identity the AI should adopt]
Instructions: [Overall task in plain terms]
Steps:
  1. [First action]
  2. [Second action]
  3. [Continue as needed]
End Goal: [What the final output must achieve]
Narrowing: [Constraints, scope limits, what to exclude]
```

**Example:**
```
Role: You are a product manager with 10 years of experience in mobile apps.
Instructions: Write a product requirements document for a habit tracking feature.
Steps:
  1. Define the problem statement in one paragraph
  2. List user stories in the format "As a [user], I want [goal] so that [reason]"
  3. Define acceptance criteria for each story
  4. List out-of-scope items explicitly
End Goal: A PRD that an engineering team can begin sprint planning from immediately.
Narrowing: No technical implementation details. No wireframes. Under 600 words total.
```

**Best model:** Opus 4.6 for complex multi-step reasoning.

---

## Template D — CRISPE

*Capacity, Role, Insight, Statement, Personality, Experiment. Use for creative work, brand voice writing, and any task where personality, tone, and iteration matter.*

```
Capacity: [What capability or expertise the AI should have]
Role: [Specific persona to adopt]
Insight: [Key background insight that shapes the response]
Statement: [The core task or question]
Personality: [Tone and style — witty / authoritative / casual / sharp]
Experiment: [Request variants or alternatives to explore]
```

**Example:**
```
Capacity: Expert copywriter specializing in SaaS product launches.
Role: Brand voice for a productivity tool aimed at developers.
Insight: Developers dislike marketing speak and respond to honesty and specificity.
Statement: Write the hero headline and sub-headline for the landing page.
Personality: Sharp, dry, confident — no adjectives, no exclamation marks.
Experiment: Give 3 variants ranging from minimal to bold.
```

**Best model:** Opus 4.6 for creative nuance.

---

## Template E — Guided Reasoning

*Use for logic-heavy tasks, math, debugging, and multi-factor analysis. Adapted for thinking models — provides light guidance without over-prescribing step-by-step.*

**For Opus 4.6 (Thinking):**
Opus has built-in extended thinking. Provide light guidance, not rigid step-by-step chains:
```
[Task statement]

Think carefully about this before answering.

<context>
[Relevant constraints, data, or code to analyze]
</context>

Provide your analysis, then your final answer.
```

**For Gemini 3.1 High:**
Running at High reasoning tier. Slightly more structure helps:
```
[Task statement]

Before answering, consider:
1. What is the actual problem?
2. What constraints must the solution respect?
3. What are the possible approaches and their tradeoffs?

Provide your final recommendation with reasoning.
```

**When to use:**
- Debugging where the cause is not obvious
- Comparing two technical approaches
- Any math or calculation
- Analysis where a wrong first impression is likely

**When to keep it minimal:**
- Simple tasks where the answer is clear (unnecessary overhead)
- Creative tasks (structured reasoning can kill natural voice)

---

## Template F — Few-Shot

*Use when the output format is easier to show than describe. Examples outperform written instructions for format-sensitive tasks every time.*

```
[Task instruction]

Here are examples of the exact format needed:

<examples>
  <example>
    <input>[example input 1]</input>
    <output>[example output 1]</output>
  </example>
  <example>
    <input>[example input 2]</input>
    <output>[example output 2]</output>
  </example>
</examples>

Now apply this exact pattern to: [actual input]
```

**Rules:**
- 2 to 5 examples is the sweet spot. More rarely helps and wastes tokens.
- Examples must include edge cases, not just easy cases.
- Use XML tags to wrap examples — both Claude and Gemini parse XML reliably.
- If you have been re-prompting for the same formatting correction twice, switch to few-shot instead of rewriting instructions.

**Best model:** Either — both parse XML examples well.

---

## Template G — ReAct + Stop Conditions

*Use for any agentic task in Antigravity where the agent takes autonomous actions. Runaway loops and scope explosion are the biggest token killers — stop conditions are mandatory.*

```
## Objective
[Single, unambiguous goal in one sentence]

## Starting State
[Current file structure / codebase state / environment]

## Target State
[What should exist when the agent is done]

## Allowed Actions
- [Specific action the agent may take]
- Install only packages already in the project

## Scope Lock
- Only modify files inside [directory/scope]
- Preserve all existing [type signatures / API contracts / variable names]

## Stop Conditions
Pause and ask for human review when:
- A file would be permanently deleted
- A new external service or API needs to be integrated
- Two valid implementation paths exist and the choice affects architecture
- An error persists after 2 attempts
- The task requires changes outside the stated scope

## Checkpoints
After each major step, output: ✅ [what was completed]
At the end, output a full summary of every file changed.
```

**Best model:** Opus 4.6 for complex agentic work, Gemini 3.1 for file-heavy exploration tasks.

---

## Template H — Prompt Decompiler

*Use when the user pastes an existing prompt and wants to break it down, adapt it for a different model, simplify it, or understand its structure.*

**Detect which task is needed:**
- **Break down** — explain what each part of the prompt does
- **Adapt** — rewrite for the other model (Gemini ↔ Opus) while preserving intent
- **Simplify** — remove redundancy and tighten without losing meaning
- **Split** — divide a complex one-shot prompt into a cleaner sequence

**For Adapt tasks, always ask:**
"Is this prompt currently written for Gemini or Opus, and which model do you want it adapted for?"

**Break down output format:**
```
Original prompt: [paste]

Structure analysis:
- Role/Identity: [what role is assigned and why]
- Task: [what action is being requested]
- Constraints: [what limits are set]
- Format: [what output shape is expected]
- Weaknesses: [what is missing or could cause wrong output]

Recommended fix: [rewritten version with gaps filled]
```

**Adapt output format:**
```
Original (for [source model]): [original prompt]

Adapted for [target model]:
[rewritten prompt using target model strengths]

Key changes made:
- [change 1 and why]
- [change 2 and why]
```

---

## Template I — Opus 4.6 Task Brief

*Use for any complex, multi-step, or agentic task on Claude Opus 4.6 (Thinking) inside Antigravity. Opus 4.6 fills implicit context better than later versions, but explicit structure still produces the best results. This template front-loads everything so the first turn is the only turn.*

```
## Objective
[What needs to be built, fixed, or produced — one clear sentence. Add WHY if it affects approach.]

## Context
[What exists now — relevant files, current behavior, stack already in place, what was tried and failed]

## Target State
[What done looks like — specific files changed, behavior produced, tests passing. Binary where possible.]

## Scope
- Work only in: [specific files and directories]
- Preserve: [files, configs, and contracts to leave unchanged]

## Constraints
- [Stack version, naming conventions, dependency rules]
- Only make changes directly requested. Keep changes focused and minimal.

## Acceptance Criteria
- [ ] [Binary check 1]
- [ ] [Binary check 2]
- [ ] [Binary check 3]

## Stop Conditions
Stop and ask before:
- Deleting any file
- Adding any dependency
- Modifying database schema or migrations
- Touching anything outside Scope

## Progress
After each completed step: ✅ [what was done] — [file(s) affected]
```

**Thinking guidance** — add only when needed:
- Hard multi-step task: `"Think carefully before starting."`
- Simple targeted change: omit — Opus 4.6 calibrates automatically
- Default: say nothing

---

## Template J — Planning Trigger

*Use when the task is complex enough to warrant Antigravity's planning mode. This template instructs the agent to plan first and execute only after user approval.*

```
## Goal
[What needs to be accomplished — high-level description]

## Why Planning Mode
[Brief explanation of complexity: multi-file changes, architectural decisions, ambiguous requirements]

## Research Phase
Before proposing changes:
1. Read and understand [specific files/directories]
2. Identify dependencies and potential impacts
3. Note any open questions or ambiguities

## Deliverable
Create an implementation_plan.md artifact with:
- Proposed changes grouped by component
- Files to be modified, created, or deleted
- Open questions that need my input
- Verification plan

## Approval Gate
Wait for my explicit approval before making any code changes.

## Execution
After approval, execute the plan step by step with checkpoint output.
```

**Best model:** Opus 4.6 for plan creation, Gemini 3.1 High for the research phase.
