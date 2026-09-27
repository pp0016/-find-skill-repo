# How to Deep Research Any Topic as a Long-Form YouTube Creator

This is a distilled research methodology for producing high-quality, long-form faceless YouTube content using AI tools. Every section below maps to a practical step in the production pipeline.

---

## Phase 1: Topic Selection & Packaging

### Frame an Operational Question
Do not research a broad topic. Convert your idea into a specific, compelling question that gives the video a narrative spine.

- **Wrong:** "Solar energy"
- **Right:** "Why did solar farms in the Sahara desert fail?"

The question does two things: it tells you what to research, and it tells the viewer why they should care.

### Reverse-Engineered Packaging (Title & Thumbnail First)
Conceptualize the video's title and thumbnail **before** beginning deep research. The package represents your promise to the viewer. If you cannot create a title/thumbnail that promises a specific, high-stakes angle or resolution, the topic is not worth researching.

This filters out topics that are interesting to research but produce videos nobody clicks.

### The 60-Second Hook
The first 40-60 seconds of any long-form video must contain "visual anchors" — specific visual proof like rare images, primary documents, data visualizations, or map animations. This establishes credibility immediately and prevents early viewer drop-off.

Plan the hook during the research phase, not during editing. When you find a striking piece of evidence, flag it as a potential hook element.

---

## Phase 2: Source Verification (SIFT Method)

Before trusting any source — article, video transcript, statistic, or claim — run it through the SIFT framework:

1. **Stop:** Pause before engaging. Check your own confirmation bias — are you accepting this because it supports what you already believe?
2. **Investigate the Source (Lateral Reading):** Do NOT evaluate a source by reading the page itself (vertical reading). Open new tabs and search what independent, trusted external sources say about the author, publisher, and their potential conflicts of interest.
3. **Find Better Coverage:** Seek consensus-backed organizations and expert analyses. One source is never enough for a factual claim in a video.
4. **Trace Claims Back:** Track every claim, quote, and media asset back to its original context. Quotes get selectively clipped. Statistics get taken out of context. Images get misattributed.

### The Two Core Verification Questions
For every claim you plan to include in a video, ask:
- **"How do you know that?"** — traces the evidence chain
- **"How else do you know that?"** — forces triangulation from independent sources

### Digital Asset Verification
When using specific images, screenshots, or video clips as evidence:
- **Provenance:** Use reverse image search (Google Search by Image or TinEye) to find the original source and highest-resolution version
- **Date & Location:** Cross-reference claimed dates with verifiable data (weather records via Wolfram Alpha, physical landmarks via Google Earth)

---

## Phase 3: Competitor Niche Analysis (Batch Researching)

This is the highest-value research phase for niche selection. The goal is to reverse-engineer what works in your target niche by analyzing outlier videos at scale.

### Step-by-Step Process:

1. **Identify 10-15 Overperformers:** Filter for competitor videos that achieved exceptional view counts relative to their channel's subscriber base (outlier ratio = video views ÷ channel median views).

2. **Ingest the Outliers:** Add these video URLs or transcripts into a multi-source synthesis tool (NotebookLM or equivalent) to analyze them simultaneously as a single dataset.

3. **Query for Niche Patterns:** Interrogate the dataset for structural patterns across the outliers:
   - What hook formats and opening styles do the top-performing videos use?
   - What recurring topic frameworks and visual thumbnail cues appear?
   - Where do they place calls-to-action and how do they handle viewer objections?
   - What angles or topics are conspicuously absent across all of them?

4. **Develop a Counter-Script Brief:** Do not copy what works. Instead, identify the **content gaps** — what was left unsaid across all 10-15 outliers is your highest-value opportunity. Build your first video briefs around these gaps.

---

## Phase 4: Scripting for the Screen

### The ABT (And, But, Therefore) Model
Structure every script using Randy Olson's ABT framework:

- **AND** — establishes the known, accepted facts (setup)
- **BUT** — introduces a specific tension, contradiction, or knowledge gap (conflict)
- **THEREFORE** — provides your analysis and resolution (payoff)

Avoid episodic "and then" writing (*X happened, and then Y happened, and then Z happened*). Every story beat must react to the one before it. Connect scenes with **"But" (obstacle/reversal)** or **"Therefore" (logical consequence)** to drive the narrative forward.

### Dual-Channel Script Format
Use a two-column layout:
- **Left column:** Spoken narration (the audio track)
- **Right column:** Specific visual and sound cues (e.g., `[Insert map showing 1945 borders]`, `[Audio: low-frequency synth drone]`)

This is grounded in Dual-Coding Theory: the brain processes visual and auditory information through separate channels simultaneously. Synchronized tracks produce faster and deeper comprehension than narration alone.

### Pacing Rules
- Write in active voice with short, direct sentences and natural contractions
- Target narration tempo: **130-150 words per minute**
- Read the script aloud with a timer — cut anything that creates tongue-twisters, pacing drags, or tangents that don't support the core argument

---

## Phase 5: Fact-Checking Before Production

### The Green Fact-Check Standard
(Used by Johnny Harris and other investigative video essayists)

1. Highlight every factual assertion in your script in **red**
2. Do not turn a highlight **green** until you have verified the claim against a primary source
3. Attach a citation reference to every green-marked claim
4. Any claim still highlighted red when you begin recording must be either verified, rewritten as qualified opinion, or cut

### The Shame Draft
Before committing to full production (AI visuals, voiceover generation, editing):
- Compile a rough audio draft of the narration with crude placeholder visuals
- Use this to test pacing, narrative flow, and identify weak sections
- Cutting 2 minutes from a shame draft saves hours of production on content that would have dragged anyway

---

## Research Template Prompts

Use these modular prompts in separate AI conversations to structure your research.

### Prompt 1: The Research Architect (Planning & Search Strategy)

```markdown
You are an expert research assistant specializing in systematic investigation and source mapping. I want to perform a deep research investigation into the following topic:

[INSERT TOPIC HERE]

Guide me through framing and search strategy:

1. **5W1H Framework**: Break this topic into Who (involved/affected), What (core phenomenon), When (timeline), Where (geographic/demographic context), Why (causes), and How (mechanisms).

2. **Vertical Logic Drill-Down**:
   - State the core research question.
   - Identify the 3-4 parallel components of this issue.
   - For the 2 most critical components, drill down by asking successive "Why?" questions to reach the systemic root causes.

3. **Targeted Search Strategy**: Identify which source types (academic databases, government repositories, industry reports, creator case studies) are most relevant to this topic and why.

4. **Search Strings**: Generate 3 precise Boolean search strings I can use in Google Scholar, YouTube search, and general web search to find high-quality sources.
```

### Prompt 2: The Source Evaluator (Verification)

```markdown
You are a fact-checker and source evaluator. I have found a source for my research and want to verify its credibility.

Here is the text, abstract, or key claims from the source:
[PASTE TEXT OR KEY CLAIMS HERE]

Evaluate this source:

1. **Evidence Chain**: How does this author/source know this? What original evidence supports their claims?
2. **Lateral Reading Check**: What should I search to investigate the author's background, affiliations, funding, and potential biases?
3. **Evidence Quality**: Are the claims supported by verifiable data, or are they preliminary findings, opinions, or anecdotal? What primary sources should I trace back to verify?
4. **Verification Steps**: If this source references specific events, dates, statistics, or images, what specific tools or methods should I use to confirm accuracy?
```

---

*This methodology is designed to work with an AI-powered production stack (Antigravity IDE, NotebookLM, ElevenLabs, AI visuals). Every phase produces an artifact that feeds the next stage of production.*