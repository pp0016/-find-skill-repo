# Skill Guide — How to Use Your 3 Custom Skills

This is your reference for what each skill does, when to use it, and how they work together.

---

## Installed Skills

| Skill | Path | Lines | Sources Combined |
|---|---|---|---|
| **deep-researcher** | `~\.gemini\config\skills\deep-researcher\` | ~180 | efficient-web-research + deep-research + OSINT methodology |
| **anti-sycophancy** | `~\.gemini\config\skills\anti-sycophancy\` | ~210 | 0xcjl three-layer defense + FutureSpeakAI circuit breaker + mskadu extract-assess |
| **prompt-forge** | `~\.gemini\config\skills\prompt-forge\` | ~250 + refs | prompt-master v1.7.0 + severity1 prompt-improver + dair-ai engineering guide |
| **agent-skill-creator** | `~\.gemini\config\skills\agent-skill-creator\` | ~756 | FrancyJGLisboa/agent-skill-creator (cloned as-is) |

- Custom skills (combined): `C:\Users\renu5\Downloads\find-skill-repo\custom-skills\`
- Original source repos (cloned as-is): `C:\Users\renu5\Downloads\find-skill-repo\sources\`

---

## Skill 1: Deep Researcher

### What it does
Autonomous multi-source research on ANY topic. Breaks complex questions into sub-queries, searches systematically with query sharpening, reads sources using a token-efficient layered protocol, and synthesizes findings into structured reports with confidence scores and citations.

### When it triggers
- "Research X"
- "Deep dive on Y"
- "Find everything about Z"
- "What's the current state of..."
- "Compare A vs B"
- "Analyze the market for..."
- Any question needing synthesis from multiple web sources

### When NOT to use it
- Simple factual questions answerable from the model's knowledge
- Questions about your local files or codebase (use normal conversation)
- Tasks that need action, not information (use prompt-forge or normal conversation)

### What makes it different from a normal web search
1. **Plans before searching** — breaks your question into 3-10 sub-queries instead of one vague search
2. **Sharpens queries** — transforms "how to grow on YouTube" into "YouTube growth strategies algorithm 2026 case study"
3. **Reads efficiently** — skims headings first, only deep-reads if needed (saves tokens)
4. **Scores confidence** — every finding labeled High/Medium/Low so you know what to trust
5. **Structures output** — Executive Summary → Key Findings → Contradictions → Sources

### Sources it was built from
- **efficient-web-research** (antigravity-awesome-skills): Layered fetch protocol, GitHub API protocol, query sharpening rules, anti-patterns table, token budget guide
- **deep-research** (sanjay3290): Autonomous planning, sub-query breakdown, research workflow stages
- **OSINT methodology** (0xcjl): 5-stage pipeline structure, time-budget framework, confidence upgrade patterns

---

## Skill 2: Anti-Sycophancy

### What it does
Kills yes-man behavior. Forces the AI to challenge your assumptions, provide counter-arguments before agreeing, detect when you're seeking confirmation instead of truth, and maintain critical thinking even when you push back. This is structural — it changes how the AI PROCESSES your input, not just how it phrases output.

### When it triggers
- **ALWAYS** — this skill is designed to run on every conversation
- Also explicitly on: "be ruthless", "challenge my assumptions", "don't agree with me", "play devil's advocate", "anti-sycophancy"

### The 3 layers
1. **Input Debiasing**: "This is right, right?" gets internally transformed to "What could go wrong with this?" BEFORE the model reasons about it
2. **Critical Response Strategy**: 7 rules — assumption challenge first, never directly confirm, mandatory counter-argument, confirmatory detection, agreement streak detection, pushback classification, proactivity safety floor
3. **Sentence Pattern Enforcement**: Bans "Great question!", "You're absolutely right", "I completely agree" and all sycophantic openers. Forces ANSWER→WHY→COUNTER→CONDITIONS→SOURCES structure

### Response structure it enforces
1. **ANSWER** — Direct answer, no preamble
2. **WHY** — Reasoning and evidence
3. **COUNTER** — Strongest argument AGAINST the answer
4. **CONDITIONS** — When the answer would change
5. **SOURCES** — Where it comes from

### Sources it was built from
- **anti-sycophancy (0xcjl)**: Three-layer architecture, input debiasing from ArXiv 2602.23971, critical response strategy (6 rules), sentence pattern conversion, pushback classification
- **anti-sycophancy (FutureSpeakAI)**: Circuit breaker concept, 6 adaptive dimensions, agreement streak detection, bounded drift, proactivity safety floor
- **anti-sycophancy (mskadu)**: Extract-assess-conclude-respond framework

---

## Skill 3: Prompt Forge

### What it does
Two modes:
1. **CREATE** — Build production-ready prompts from rough ideas, optimized for the specific target AI tool (30+ tools supported)
2. **ENHANCE** — Take an existing prompt, diagnose its weaknesses against 37 known failure patterns, and rewrite it

### When it triggers
- "Write me a prompt for [tool]"
- "Fix/improve/enhance this prompt"
- "Adapt this prompt for [different tool]"
- "What's wrong with this prompt?"
- "Prompt for Midjourney/GPT/Claude/Cursor/etc."

### When NOT to use it
- General conversation or coding tasks
- You want the AI to DO something (not write a prompt for something)
- Document writing that isn't a prompt

### Tools it knows (30+)
Claude 4.x, GPT-5.x, o3/o4-mini, Gemini, Qwen, Ollama, Llama, Mistral, DeepSeek-R1, Claude Code, Antigravity, Cursor, Windsurf, Cline, GitHub Copilot, Bolt/v0/Lovable/Stitch, Devin, Perplexity, Midjourney, DALL-E 3, Stable Diffusion, SeeDream, ComfyUI, Meshy/Tripo/Rodin (3D), Unity AI, Sora/Runway/Kling (Video), ElevenLabs (Voice), Zapier/Make/n8n (Workflow)

### Template auto-selection
It automatically picks the right framework based on your task:
- Simple task → RTF
- Business writing → CO-STAR
- Complex project → RISEN
- Creative work → CRISPE
- Logic/debugging → Chain of Thought
- Format-critical → Few-Shot
- Code editing → File-Scope
- Autonomous agents → ReAct + Stop Conditions
- Image generation → Visual Descriptor
- Existing prompt → Prompt Decompiler

### Progressive disclosure
Heavy reference material loads on-demand from `references/`:
- `templates.md` — Full template structures for all 13 categories
- `patterns.md` — Complete 37-pattern diagnostic checklist

### Sources it was built from
- **prompt-master v1.7.0 (nidhinjs)**: Foundation — 30+ tool profiles, 12 templates, 9-dimension intent extraction, diagnostic checklist, credential safety, token efficiency audit
- **claude-code-prompt-improver (severity1)**: Research-before-asking methodology for ENHANCE mode
- **Prompt-Engineering-Guide (dair-ai)**: Academic validation of technique selection hierarchy

---

## How They Work Together

```
You have a question/idea
        │
        ├── Need information? ──────────→ [deep-researcher]
        │   "Research YouTube thumbnail       Searches, reads, synthesizes
        │    strategies for 2026"              Delivers cited report
        │                                          │
        │                                          ▼
        ├── Need an AI prompt? ─────────→ [prompt-forge]
        │   "Write me a Midjourney prompt     Extracts intent, picks template,
        │    for a tech thumbnail"             optimizes for the specific tool
        │                                          │
        │                                          ▼
        └── Need honest feedback? ──────→ [anti-sycophancy]
            (Always active)                   Challenges assumptions,
                                              provides counter-arguments,
                                              kills yes-man behavior
```

### Example workflow: Creating a YouTube video

1. **Research phase**: "Research what makes YouTube thumbnails get the most clicks in 2026"
   → `deep-researcher` activates, searches 5-8 sources, delivers structured report with confidence scores

2. **Prompt creation phase**: "Write me a Midjourney prompt for a thumbnail about AI coding tools"
   → `prompt-forge` activates, uses Visual Descriptor template, outputs comma-separated Midjourney syntax with --ar and --v parameters

3. **Quality check**: Throughout everything, `anti-sycophancy` is running — if you ask "this thumbnail idea is good, right?" it will challenge the assumption before confirming

---

## Skill 4: Agent Skill Creator

### What it does
Builds new SKILL.md files from scratch using a structured 5-phase factory process: Intent Derivation → Skill Architecture → Content Generation → Validation → Delivery. Supports 17+ platforms including Antigravity, Claude Code, Cursor, and Gemini CLI.

### When it triggers
- "Create a skill for..."
- "Build a new skill"
- "Turn this workflow into a skill"
- "Make a SKILL.md from..."

### Source
Cloned as-is from [FrancyJGLisboa/agent-skill-creator](https://github.com/FrancyJGLisboa/agent-skill-creator). Not modified. The full 756-line SKILL.md contains the complete factory methodology.

### Why this one and not Anthropic's skill-creator (298K installs)
Anthropics' version requires Claude Code subagent infrastructure for testing/eval. Won't work in Antigravity. FrancyJGLisboa's works on 17 platforms including Gemini CLI.

---

## Existing Skills (Untouched)

These were already installed before this work and remain unchanged:

| Skill | Purpose |
|---|---|
| priyanshu-controller-skill | Response quality controller |
| skill-repair | Fix failed skill installations |
| accidental-data-loss-prevention | Safety gate for destructive commands |
| + 15 GCP/data skills | BigQuery, Dataform, Spark, etc. |

> **Note**: `prompt-master` has been **removed**. `prompt-forge` fully supersedes it — it has everything prompt-master had PLUS the ENHANCE mode and research-before-asking methodology.

---

## Modifying These Skills Later

All 4 skills are standard SKILL.md files. To modify:

1. Edit the SKILL.md in `~\.gemini\config\skills\[skill-name]\SKILL.md`
2. Changes take effect in the next conversation (no restart needed)
3. Keep the YAML frontmatter (`name:` and `description:`) intact — this is how skills trigger
4. Keep SKILL.md under 500 lines — use `references/` for heavy content
5. The `description` field is the MOST important part — it controls when the skill activates

### File Structure
```
find-skill-repo\
├── custom-skills\          ← Your 3 combined skills (deep-researcher, anti-sycophancy, prompt-forge)
├── sources\                ← Original cloned repos (efficient-web-research, 0xcjl, FutureSpeakAI, prompt-master, agent-skill-creator)
├── SKILL_GUIDE.md          ← This file
├── Prompt Improver\        ← Original prompt-master download
├── Prompt engineer\        ← Original antigravity-awesome-skills download
└── findskill\              ← findskill CLI tool
```
Something that I found out and I am pasting here because I can use it in the workflow 

Viewed controller.md:1-405

I have read all 405 lines of your `controller.md`. You have built something genuinely impressive — a full 11-stage video production pipeline for your **Stickman** channel with 27 auto-trigger skills, 7 Python scripts, 5 mandatory quality gates, and a learning loop.

Now here is exactly how `/learn`, `/schedule`, `/grill-me`, and `/goal` map to YOUR specific production system:

---

### `/schedule` — Your Stage 9 Performance Reviews (Automated)
Your controller says after every upload you MUST run performance analysis at **24hr, 72hr, 7-day, and 30-day** windows. Right now you have to remember to come back and do this manually. With `/schedule`, you set it once and forget:

> After uploading Video 01, type:
> `/schedule Remind me in 24 hours: Run 24hr quick verdict for Video 01 using performance_analysis.md`

I will wake up automatically at those intervals and remind you (or even run the analysis if you have the YouTube Analytics MCP connected). This directly powers your **Gate 5** and prevents your learning loop from breaking.

---

### `/grill-me` — Your Stage 1 Validation (Interactive)
Your controller says Stage 1 requires validating the topic + title concept + thumbnail concept before proceeding. Instead of you guessing whether your idea is strong enough, `/grill-me` turns me into a ruthless interviewer:

> Type: `/grill-me I want to make a video about why ancient humans feared the dark`

I will walk you through every decision one-by-one:
- *"Who is the target viewer — someone curious about evolution or someone who wants survival tips?"*
- *"Your title 'Why Humans Fear The Dark' scores 6/10 on WTPI. Would you consider 'You Were Never Meant To Sleep Alone' instead?"*
- *"Your thumbnail concept has no visual contrast. Should we add a glowing eye in the darkness?"*

This replaces your 4-step validation gate with a structured, interactive interrogation that catches weak ideas before you waste 5 hours producing them.

---

### `/goal` — Your Full Pipeline Execution (Stages 2-8, Overnight)
Your pipeline takes 4-7 hours per video. With `/goal`, you can hand me an approved topic and let me grind through multiple stages autonomously while you sleep:

> Type: `/goal The topic "Why Sleep Deprivation Kills You" passed Gate 1. Execute Stages 2 through 5: research, write the script, generate music prompts, and create all image prompts. Save everything to C:\Users\renu5\Downloads\Stick man videos project\Video_01_Sleep_Deprivation\`

I will run deep research, write the full script using your Voice DNA, run `score_script.py` against the alive_checklist, generate Lyria 3 music prompts, create Nano Banana 2 image prompts for every scene — and I won't stop until every gate passes. You wake up to a production-ready package.

---

### `/learn` — Your Channel Memory Updates (Permanent Rules)
Your controller has a "Learning Loop" where Stage 9 analysis feeds rules back into `channel_memory.md`. But right now, if I discover something important mid-conversation (like "hooks with questions always outperform hooks with statements on your channel"), that insight dies when the conversation ends.

With `/learn`, I permanently save that discovery:

> After analyzing Video 03's performance, I notice retention spikes 15% whenever you use a "dead body" opening. Type: `/learn`

I will propose adding a new Hard Rule to your system: *"R11: Always test a 'death scene' hook variant — historically +15% retention on this channel."* After you approve, every future conversation will know this rule automatically.

---

### Summary: How They Map to Your Pipeline

| Command | Your Pipeline Stage | What It Replaces |
|---------|-------------------|-----------------|
| `/grill-me` | Stage 1 (Validate) | Manual 4-step validation → interactive interrogation |
| `/goal` | Stages 2-8 (Produce) | You babysitting every stage → overnight autonomous execution |
| `/schedule` | Stage 9 (Analyze) | Forgetting to review → automated 24hr/72hr/7d/30d reminders |
| `/learn` | The Learning Loop | Insights dying between conversations → permanent channel rules |

Want to test one of these right now on your next video idea?

I've completed everything you asked for. Let me verify against your original request:

### Deliverable Checklist

| Requirement | Status | Evidence |
|---|---|---|
| Read `controller.md` only | ✅ Done | Read all 405 lines, no other files opened |
| Explain `/learn` for your content workflow | ✅ Done | Mapped to your Learning Loop → `channel_memory.md` permanent rule saving |
| Explain `/schedule` for your content workflow | ✅ Done | Mapped to your Stage 9 → automated 24hr/72hr/7d/30d performance review reminders |
| Explain `/grill-me` for your content workflow | ✅ Done | Mapped to your Stage 1 → interactive topic/title/thumbnail validation replacing your 4-step gate |
| Explain `/goal` for your content workflow | ✅ Done | Mapped to your Stages 2-8 → overnight autonomous pipeline execution |
| Keep it short, from starting to ending | ✅ Done | Covered Stage 1 (start) through Stage 9 (end) with summary table |

Everything is answered. No pending work remains — this was an informational request and all four commands have been explained with direct references to your Stickman Studio pipeline stages and gate system.

<!-- GOAL_COMPLETE -->
2nd edit 
1. Memory Bank
What it is doing: Saving text files (like projectbrief.md) in your local folder.
What it will do for you: It acts as my long-term memory. You define your brand voice, target audience, and active projects once. I will auto-read it every session so you never have to repeat yourself.
2. Humanizer
What it is doing: Scanning AI-generated text for robotic patterns (like overusing the word "delve" or predictable sentence structures).
What it will do for you: It strips the "AI slop" from your scripts and captions. It makes your content sound authentic, keeping your audience engaged and bypassing AI detectors.
3. Sequential Thinking
What it is doing: Forcing me to create a visible, step-by-step reasoning chain before I give you a final answer.
What it will do for you: It cures "lazy AI." When you ask for complex content (like adapting a podcast into a TikTok), it ensures I analyze the pacing, hook, and climax first, resulting in a much higher quality script instead of generic garbage.
4. Hyperframes
What it is doing: Using code (HTML/CSS) and a headless browser to render video files.
What it will do for you: It lets you type a text prompt (e.g., "Create a 15-second product explainer") and I will write the code, animate it, and generate a finalized, pixel-perfect MP4 video file for you without needing a video editor.

Third edit 
agency-agents: Helpful as a reference guide. Specifically, the design folder teaches you the architectural blueprint of how to structure prompts and manage context for your own specialized content agents.
youtube-automation-agent: Helpful as a practical, ready-to-use system. It gives you a complete, working architecture (database, dashboards, scheduling) that you can immediately adapt into your own end-to-end YouTube content factory. 
Fourth edit 
Your Daily Workflow — Like a Decade-Experienced YouTuber
A veteran YouTuber doesn't open 15 tools. They run a tight loop: Research → Validate → Create → Optimize → Repeat. Here's yours:

PHASE 1: Pick Your Niche (Do Once, Then Move On)
Time: 2-3 hours, one-time.


Step 1: Google Trends → YouTube Search filter
        → Type 5 niche ideas you're considering
        → Compare them side-by-side (up to 5 at once)
        → KILL any niche that's declining or flat-lining
        → KEEP anything with a rising curve
Step 2: vidIQ Free → Keyword Explorer
        → Search the surviving niches as keywords
        → Check: Search Volume vs Competition Score
        → You want: HIGH volume + LOW/MEDIUM competition
        → Write down the top 3 niches
Step 3: YouTube itself → Manual "10K-100K" scan
        → Search each niche → Filter: Channel
        → Find channels with 10K-100K subs
        → Are their recent videos getting 50K+ views?
        → YES = viable niche. NO = skip it.
Output: 1-2 validated niches with proven demand and room for new creators.

PHASE 2: Study The Winners (Weekly, 30 min)

Step 1: ViewStats Chrome Extension
        → Go to your top 5 competitor channels
        → Check their last 10 uploads
        → ViewStats shows "hit or miss" scoring
        → Identify which videos MASSIVELY outperformed
        → Note: title format, thumbnail style, video length, topic
Step 2: ViewStats → Thumbnail/Title Change History
        → See if the creator changed their title or thumbnail after upload
        → If they did, the SECOND version performed better
        → Copy that pattern, not the original
Step 3: Social Blade → Growth comparison
        → Compare 3 competitor channels side-by-side
        → Who's growing fastest in the last 30/90 days?
        → Study that channel harder — they found something
Step 4: vidIQ → Competitor tracking
        → Add your top 5 competitors to vidIQ tracking
        → It will notify you when they upload
        → Check their SEO score overlay on each new video
Output: A list of 5-10 proven video ideas with validated titles and thumbnail styles.

PHASE 3: Create Content (Per Video, 15 min research)

Step 1: vidIQ → AI Title Generator (free, 150 credits/mo)
        → Input your topic → Get 10 title options
        → Pick the one with highest estimated CTR
Step 2: vidIQ → AI Script Outline
        → Generate a script structure from your topic
        → Edit it — don't publish AI slop raw
Step 3: Competitor transcript extraction
        → Use YouTube's built-in transcript (click "..." → "Show transcript")
        → Or use TubeOnAI extension (free) for cleaner extraction
        → Study the HOOK (first 30 seconds) of top-performing competitor videos
        → Model your hook after theirs
PHASE 4: Post-Upload Optimize (Per Video, 10 min)

Step 1: YouTube Studio → "Test & Compare" (Thumbnail A/B testing)
        → Upload 2-3 thumbnail versions
        → YouTube tests them against REAL viewers
        → Better than any paid tool — this uses actual click data
Step 2: vidIQ → SEO Score
        → Check your video's SEO score immediately after upload
        → Fix any red flags (missing tags, weak description, poor keyword density)
Step 3: Social Blade → Track your growth
        → Check weekly, not daily (daily checking is a productivity killer)
        → Are you growing? Keep doing what you're doing.
        → Flat? Go back to Phase 2 and study new competitors.

 5th edit 
MY DAILY WORKFLOW
STEP 1: PICK NICHE (One-time, 2-3 hours)
Google Trends → YouTube filter → Compare 5 niche ideas → Kill declining ones
vidIQ → Keyword Explorer → Check volume vs competition → Want HIGH volume + LOW competition
YouTube → Search niche → Filter: Channel → Find channels 10K-100K subs getting 50K+ views = viable niche
STEP 2: STUDY WINNERS (Weekly, 30 min)
ViewStats extension → Open top 5 competitor channels → Check hit/miss on last 10 uploads
ViewStats → See if they changed thumbnail/title after upload → The CHANGED version = what works
Social Blade → Compare 3 competitors → Who's growing fastest last 30 days? Study them.
vidIQ → Add 5 competitors to tracking → Get notified when they upload
STEP 3: CREATE CONTENT (Per video, 15 min research)
vidIQ → AI Title Generator → Pick highest-CTR option
vidIQ → AI Script Outline → Edit it, don't publish raw AI
Watch top competitor video → Copy their HOOK structure (first 30 seconds)
YouTube transcript → use notbookllm → Study their format
STEP 4: POST-UPLOAD (Per video, 10 min)
YouTube Studio → "Test & Compare" → Upload 2-3 thumbnails → YouTube tests with real viewers
vidIQ → Check SEO score → Fix red flags (tags, description, keywords)
Social Blade → Check growth WEEKLY not daily

6th edit 
The Complete Free Stack — Your Daily Workflow
Phase 1: Niche Research (Before starting a channel)
Google Trends (YouTube filter) → Validate demand exists and isn't declining
TubeLab Free Niche Analyzer → Check saturation and estimated RPM
FlowShorts → Get faceless-specific niche ideas with CPM data
vidIQ Free → Keyword research with competition scores
Phase 2: Competitor Analysis (Finding channels to study)
vidIQ Free → Discover competing channels, track their uploads
Social Blade → Historical growth, side-by-side comparisons
ViewStats → View velocity, thumbnail/title change history, hit/miss scoring
1of10 extension → Outlier scores on videos you browse
Phase 3: Content Creation (Making videos)
vidIQ Free → AI script generator, title generator (150 credits/mo)
KeywordTool.io → Long-tail keyword brainstorming from YouTube Autocomplete
YouTube Studio "Test & Compare" → Real A/B thumbnail testing with actual viewer data
TubeOnAI → Extract competitor transcripts for format research
Phase 4: Post-Upload Optimization
vidIQ Free → SEO scoring, tag recommendations
Social Blade → Monitor your growth trajectory 

