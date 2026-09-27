# YouTube Niche Research — Complete Brief

## My Goal

I want to find a consistent, evergreen YouTube niche that delivers both high RPM AND high views — not high RPM with low views, and not high views with low RPM. Both must be high together.

**RPM Threshold:** I define "high RPM" as $2+ per 1,000 views in Tier 1 markets. Anything below $2 RPM is not worth pursuing. This is real RPM based on studied channel performance in Tier 1 countries — not inflated estimates from unreliable sources. Niche selection should be driven by identifying which countries have the highest RPM potential, then finding niches that perform well in those markets.

**Target Audience:** Tier 1 English-speaking countries: USA, UK, Canada, Australia. Primary language is English, but I am open to dubbed or multilingual content if the niche supports it.

**Revenue Model:** I do not want to rely on AdSense alone. The ideal niche should also support affiliate marketing and potential sponsorship deals, since these often exceed ad revenue in high-RPM niches.

## Channel Strategy

I want to run one channel that gives very high RPM and very high views. If the income from one channel is strong enough, I do not need a second one.

However, if there are two niches that are both easy to manage, I am open to running two channels simultaneously.

## Creator Profile

I am a faceless content creator. I have not started my channel yet. I do not show my face. Since I do not need to be on camera, I can work on any niche — the niche choice should be driven purely by RPM and view data, not personal interest.

The niche should not be so complex that AI tools cannot handle the production. If AI can do most of the work, I can do it.

## Timeline

I want results within 1 month — not 6 to 12 months.

## Content Format

I prefer long-form videos. I want a channel that can get an early boom if the videos are excellent.

**Video Length:**
- Preferred: 8 to 15 minutes (easier to produce)
- Acceptable: 15 to 30 minutes (for easy and medium effort niches)
- Maximum: 30+ minutes (for easy and medium effort niches only, not hard ones)

**Mid-Roll Ad Requirement:** Videos must be 8+ minutes to unlock mid-roll ad placements on YouTube. Mid-rolls can effectively double RPM compared to pre-roll only. This is why 8-25 minutes is the minimum target range.

**YouTube's 2025-2026 Content Policy:** YouTube is actively deprioritizing mass-produced, low-effort AI content. Even though my production is AI-powered, every video needs original research, unique angles, and editorial quality to avoid being flagged as repetitive content.

## 3-Tier Structure

I want niche recommendations organized into 3 difficulty tiers. All 3 tiers must have HIGH RPM. The only difference between tiers is how much effort each video requires:

- **Easy:** Low effort per video, high RPM
- **Medium:** Moderate effort per video, high RPM
- **Hard:** High effort per video, highest RPM potential

I can choose from any tier based on what I am willing to put in. I might pick one from easy and one from medium to run two channels, or pick one high-RPM niche from any tier and commit fully.

## Niche Validation Criteria

**The "10K-100K Subscriber" Test:** A niche is viable if channels with 10K-100K subscribers are consistently getting 50K+ views on their recent videos. This means the niche has real demand and is not locked behind massive channels only.

**For every niche recommended, I want:**
- The top 5 real faceless YouTube channels in that niche so I can personally verify them — check their subscriber count, views, upload frequency, and whether they are actually performing.

## AI Video Production Stack

I produce full YouTube videos — from topic discovery to published upload — using AI tools across every stage. No manual editing software. Here is my stack:

**Research & Scripting**
- NotebookLM — Upload competitor videos and reference material, extract structured insights through targeted Q&A (transcript-based knowledge extraction)
- Gemini (web app) — Paste a YouTube video for native video + audio analysis (watches the full video); can also analyze via URL
- Supadata — Pull exact transcripts and performance metrics from any public video
- Antigravity IDE (Gemini/Claude) — Script writing, research synthesis, competitor analysis, and command generation. This is my main working environment.

**Voice & Music**
- ElevenLabs — AI voiceover generation with emotional tags inside the script
- Google Lyria 3 — Background music generation matched to scene mood

**Visuals**
- Nano Banana 2 — AI image generation (primary visual tool)
- Google Veo 3.1 and Omni model — AI video clip generation (2-4s, 4-6s, 6-8s, 8-10s clips from Omni; 8s fixed from Veo 3.1)
- FFMPEG — Ken Burns effects, text overlays, image processing (free, runs locally)
- Pexels API — Automated B-roll footage download via custom Python scripts

**Assembly & Rendering**
- FFMPEG — Full local video assembly pipeline (audio mixing → visual composition → 4K export)
- Remotion — React-based programmatic video editing with animated captions
- GitHub Actions — Free cloud rendering (2,000 min/month). Push code → get 4K .mp4 back. Zero local CPU usage.
- HyperFrames — Claude-native video composition via HTML/CSS/JS from a single prompt (not yet used)

**Polish & Upload**
- CapCut — Color grading only
- YouTube Analytics MCP — Automated performance data pull (retention, CTR, traffic sources) via API

**Automation**
- Custom Python scripts for competitor analysis, script scoring, caption generation, B-roll processing, and full pipeline orchestration
- 25+ custom AI agent skills that auto-trigger based on task context (hook writing, SEO, thumbnails, compliance checks, etc.)

**Bottom line:** Every stage runs through AI tools. Human input is creative direction, editorial judgment, and quality gates. Production cost is effectively $0 beyond API subscriptions.

## Niche Research Tools

From my existing workflow, these are the tools I use for niche research and validation. For detailed usage instructions, optimal free-tier strategies, and honest assessments of each tool, see the companion document: **`niche-tool-guide.md`**

**Phase 1 — Niche Discovery & Validation:**
- Google Trends (YouTube filter) — Validate demand and trend direction
- Glimpse (Chrome extension) — Adds absolute search volume numbers to Google Trends data
- TubeLab Free Niche Analyzer — Check saturation and estimated RPM
- vidIQ Free — Keyword research with competition scores (browser extension)
- OutlierKit (free trial: 10 credits, one-time) — Outlier detection and keyword research for niche validation. Use credits strategically: 10 outlier scans OR mix of outlier + keyword searches. One-time research session, not ongoing.

**Phase 2 — Competitor Analysis:**
- vidIQ Free — Discover competing channels, view their tags and keywords
- Social Blade — Historical growth, side-by-side channel comparisons (ignore earnings estimates)
- ViewStats — View velocity, thumbnail/title change history, hit/miss scoring
- 1of10 extension — Outlier scores on videos while browsing (Video Views ÷ Channel Median = Outlier Score)

**Phase 3 — Content Research & Planning:**
- vidIQ Free — AI script generator, title generator (150 credits/month — save for production, not research)
- KeywordTool.io — Long-tail keyword brainstorming from YouTube Autocomplete (free = no volume data, brainstorming only)
- AnswerThePublic — Question-based keyword discovery (3 free searches/day)
- YouTube Studio "Test & Compare" — Real A/B thumbnail testing with actual viewer data (measures Watch Time Share, not CTR)
- TubeOnAI — Extract competitor transcripts for format research (400 free credits)

**Phase 4 — Post-Upload Optimization:**
- vidIQ Free — SEO scoring, tag recommendations
- Social Blade — Monitor growth trajectory

**Tools Assessed and Deprioritized:**
- NexLev (free plan) — Only 3 basic tools on free plan (monetization checker, thumbnail compressor, ad placer). The Niche Finder feature relevant to my use case is Pro-only (~€42/month). Free MCP feature (connecting to ChatGPT/Claude for YouTube data queries) is the only potentially useful free component. Not worth relying on for niche research unless willing to pay.
- FlowShorts — Primarily a Shorts video generation/auto-posting tool, not a research tool. Its CPM data is generic industry averages available free elsewhere.

## How I Plan to Work

1. Use NotebookLM Deep Research to collect genuine sources about high-RPM faceless niches
2. Bring those sources back to Antigravity IDE for evaluation — checking if the sources are real and the data is solid
3. Validate the niche using the research tool stack (see `niche-tool-guide.md` for optimal tool usage per task)
4. Start producing and uploading within the first month

## What I Do Not Want

- Generic advice without data backing
- Guru-style promises of easy money without proof
- Sources that support everything uncritically — if a niche does not actually perform, the research should say so
- Dependence on just training knowledge — I want actual research with real sources
