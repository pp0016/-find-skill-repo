# Failure Patterns Reference

37 patterns that waste tokens and cause re-prompts, optimized for Antigravity IDE with Gemini 3.1 Pro (High) and Claude Opus 4.6 (Thinking). Read this file when the user pastes a bad prompt and asks you to fix it, or when diagnosing why a prompt is underperforming.

---

## Task Patterns

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 1 | **Vague task verb** | "help me with my code" | "Refactor `getUserData()` to use async/await and handle null returns" |
| 2 | **Two tasks in one prompt** | "explain AND rewrite this function" | Split into two prompts: explain first, rewrite second |
| 3 | **No success criteria** | "make it better" | "Done when the function passes existing unit tests and handles null input without throwing" |
| 4 | **Over-permissive agent** | "do whatever it takes" | Explicit allowed actions list + explicit scope lock |
| 5 | **Emotional task description** | "it's totally broken, fix everything" | "Throws uncaught TypeError on line 43 when `user` is null" |
| 6 | **Build-the-whole-thing** | "build my entire app" | Break into Prompt 1 (scaffold), Prompt 2 (core feature), Prompt 3 (polish) |
| 7 | **Implicit reference** | "now add the other thing we discussed" | Always restate the full task — never reference "the thing we discussed" |

---

## Context Patterns

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 8 | **Assumed prior knowledge** | "continue where we left off" | Include Memory Block with all prior decisions |
| 9 | **No project context** | "write a cover letter" | "PM role at B2B fintech, 2yr SWE experience transitioning to product, shipped 3 features as tech lead" |
| 10 | **Forgotten stack** | New prompt contradicts prior tech choice | Always include Memory Block with established stack |
| 11 | **Hallucination invite** | "what do experts say about X?" | "Cite only sources you are certain of. If uncertain, say so explicitly rather than guessing." |
| 12 | **Undefined audience** | "write something for users" | "Non-technical B2B buyers, no coding knowledge, decision-maker level" |
| 13 | **No mention of prior failures** | (blank) | "I already tried X and it did not work because Y. Suggest a different approach." |

---

## Format Patterns

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 14 | **Missing output format** | "explain this concept" | "3 bullet points, each under 20 words, with a one-sentence summary at top" |
| 15 | **Implicit length** | "write a summary" | "Write a summary in exactly 3 sentences" |
| 16 | **No role assignment** | (blank) | "You are a senior backend engineer specializing in Node.js and PostgreSQL" |
| 17 | **Vague aesthetic adjectives** | "make it look professional" | "Monochrome palette, 16px base font, 24px line height, clean layout" |

---

## Scope Patterns

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 18 | **No scope boundary** | "fix my app" | "Fix only the login form validation in `src/auth.js`. Touch nothing else." |
| 19 | **No stack constraints** | "build a React component" | "React 18, TypeScript strict, no external libraries, Tailwind only" |
| 20 | **No stop condition for agents** | "build the whole feature" | Explicit stop conditions + ✅ checkpoint output after each step |
| 21 | **No file path in Antigravity** | "update the login function" | "Update `handleLogin()` in `src/pages/Login.tsx` only" |
| 22 | **Wrong template for model** | Generic chatbot prompt used in Antigravity | Adapt to the appropriate Antigravity template (Template G/I/J) |
| 23 | **Pasting entire codebase** | Full repo context every prompt | Scope to only the relevant function and file |

---

## Reasoning Patterns

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 24 | **No reasoning guidance for logic task** | "which approach is better?" | "Think through both approaches carefully before recommending" |
| 25 | **Over-prescribed CoT on thinking model** | Rigid "Step 1, Step 2, Step 3" on Opus 4.6 (Thinking) | Remove rigid steps — Opus 4.6 has built-in extended thinking. Use light guidance: "Think carefully before starting" |
| 26 | **Expecting inter-session memory** | "you already know my project" | Always re-provide the Memory Block in every new session |
| 27 | **Contradicting prior work** | New prompt ignores earlier architecture | Include Memory Block with all established decisions |
| 28 | **No grounding rule for factual tasks** | "summarize what experts say about X" | "Use only information you are highly confident is accurate. Say [uncertain] if not." |

---

## Agentic Patterns (Antigravity-Specific)

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 29 | **No starting state** | "build me a REST API" | "Empty Node.js project, Express installed, `src/app.js` exists" |
| 30 | **No target state** | "add authentication" | "`/src/middleware/auth.js` with JWT verify. `POST /login` and `POST /register` in `/src/routes/auth.js`" |
| 31 | **Silent agent** | No progress output | "After each step output: ✅ [what was completed]" |
| 32 | **Unlocked filesystem** | No file restrictions | "Only edit files inside `src/`. Preserve `package.json`, `.env`, and all config files." |
| 33 | **No human review trigger** | Agent decides everything autonomously | "Stop and ask before: deleting any file, adding any dependency, or changing the database schema" |
| 34 | **Context rot on long sessions** | Keeps correcting in the same session for 60+ turns | New task = new session. Start fresh instead of stacking corrections. Switch to a new conversation at ~50% context usage. |
| 35 | **No model selection** | Uses whichever model happens to be active | Match model to task type: Opus 4.6 for reasoning-heavy work, Gemini 3.1 High for research/exploration/docs |

---

## Structural Patterns (from 2026 Context Engineering Research)

| # | Pattern | Bad Example | Fixed |
|---|---------|------------|-------|
| 36 | **Negative instructions** | "Do not be verbose. Do not hallucinate. Never use informal language." | Convert to positive: "Provide concise responses. Cite only verified sources. Use formal register." |
| 37 | **Blob prompt** | One giant paragraph with no structure or sections | Restructure with XML tags: `<context>`, `<instructions>`, `<constraints>`, `<examples>` |
| 38 | **Format Tax** | Prompt demands complex reasoning AND strict JSON output simultaneously | Separate phases: "First analyze the problem. Then format your conclusion as JSON." |
| 39 | **Critical info buried in middle** | Important constraint mentioned in paragraph 4 of a long prompt | Move to the first 30% of the prompt — both models exhibit "lost in the middle" bias |
| 40 | **Dynamic content breaks caching** | Timestamps, session IDs, or changing variables placed early in the prompt | Place all static content (system instructions, role, constraints) at the START; dynamic content at the END |
| 41 | **No XML structure for complex prompts** | Complex multi-section prompt using only prose and dashes | Wrap sections in semantic XML tags for unambiguous parsing by both Gemini and Opus |
| 42 | **Redundant CoT on thinking models** | "Think step by step" sent to Opus 4.6 (Thinking) or Gemini 3.1 (High) | Both models have native reasoning. Light guidance only: "Think carefully" for hard tasks, nothing for simple ones |
