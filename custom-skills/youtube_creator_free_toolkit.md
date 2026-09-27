# YouTube Creator Free Toolkit — ₹0/month Stack

**For:** Stickman Educational/Explainer YouTube Channel
**Date:** 2026-08-04 | **Budget:** ₹0

---

# PART 1 — Complete Free Tool Stack

## 🔍 Keyword Research (Replace vidIQ Keyword Tool)

| Tool | URL | What's Free | Limits |
|---|---|---|---|
| **Google Trends (YouTube filter)** | [trends.google.com](https://trends.google.com) | Relative interest data filtered to YouTube Search, trending topics, regional data, related queries | No absolute volume — only 0-100 relative scale |
| **YouTube Autocomplete** | YouTube search bar + [suggestqueries endpoint](#part-2) | Real-time long-tail keyword suggestions straight from YouTube | Manual unless scripted |
| **KeywordTool.io** | [keywordtool.io/youtube](https://keywordtool.io/youtube) | 750+ keyword suggestions per search from YouTube autocomplete | No volume/competition data on free plan — ideas only |
| **Analyze AI** | [analyze.ai](https://analyze.ai) | YouTube-specific search volume, keyword difficulty, CPC estimates | Free tier has daily limits |
| **Botster.io** | [botster.io](https://botster.io) | Bulk YouTube autocomplete extraction, exports to CSV | Free tier has run limits |
| **pytrends (Python)** | [github.com/GeneralMills/pytrends](https://github.com/GeneralMills/pytrends) | Programmatic Google Trends data with YouTube filter (`gprop='youtube'`) | Unofficial API, rate-limited |

**Best combo:** Google Trends (validate topic demand) + YouTube Autocomplete script (find exact titles) + Analyze AI (get volume estimates)

---

## 📊 Competitor & Channel Analysis (Replace vidIQ Analytics)

| Tool | URL | What's Free | Limits |
|---|---|---|---|
| **YouTube Studio** | [studio.youtube.com](https://studio.youtube.com) | Your own channel's full analytics — CTR, retention, demographics, traffic sources, "Research" tab, subscriber sources | Only YOUR channel |
| **Social Blade** | [socialblade.com](https://socialblade.com) | Historical sub/view growth, daily gains/losses, earnings estimates, channel grades | Public data only, shows ads |
| **NoxInfluencer** | [noxinfluencer.com](https://noxinfluencer.com) | Channel analytics, live sub counts, channel comparisons, earnings estimates | No API key needed |
| **YouTube Data API v3** | [console.cloud.google.com](https://console.cloud.google.com) | Programmatic access to video stats, channel stats, search results | 10,000 units/day free |

---

## 🔥 Outlier/Viral Video Discovery (Replace vidIQ Outlier Research)

| Tool | URL | What's Free | Limits |
|---|---|---|---|
| **OutlierKit** | [outlierkit.com](https://outlierkit.com) | Finds videos performing 5-10x above a channel's baseline | Free tier has limits |
| **ViewStats** | [viewstats.com](https://viewstats.com) | Chrome extension with views-over-time graphs, trending channels | Pro ($49.99/mo) needed for full features — free for basic browsing |
| **vidIQ MCP (your 5 accounts)** | Via Antigravity | 3 outlier searches per account × 5 accounts = **15 outlier searches/day** | Rotate API keys |

---

## 🖼️ Thumbnails (Replace vidIQ Thumbnail AI)

### For Stickman/Animation/Educational Content:

| Tool | URL | What's Free | Best For |
|---|---|---|---|
| **Canva** | [canva.com](https://canva.com) | 1280×720 templates, basic AI, text overlays, design editor | Final thumbnail assembly, text, backgrounds |
| **Pivot Animator** | [pivotanimator.net](https://pivotanimator.net) | Desktop app for 2D stickman animation, export frames | Creating stickman character poses for thumbnails |
| **Stick Nodes** | [stickfigure.app](https://www.stickfigure.app) | Browser/mobile stickman creator, high-res export | Quick stickman graphics |
| **Pixlr** | [pixlr.com](https://pixlr.com) | Free photo editor, layers, effects | Adding glow/contrast to stickman exports |
| **CleverTools / TestMyThumbnails** | [testmythumbnails.com](https://testmythumbnails.com) | Preview thumbnails in simulated YouTube layouts (home feed, mobile, dark mode) | Visual A/B comparison before publishing |

**Workflow:** Create stickman pose in Pivot/Stick Nodes → Export PNG → Import to Canva → Add background, text, effects → Preview in TestMyThumbnails → Publish

---

## ✍️ AI Writing — Titles, Descriptions, Scripts, Tags

| Tool | URL | What's Free | Limits |
|---|---|---|---|
| **Gemini API (Google AI Studio)** | [aistudio.google.com](https://aistudio.google.com) | Gemini 2.5 Flash — generous free tier, 1M token context | RPM/RPD limits, data may be used for training |
| **Groq** | [groq.com](https://groq.com) | Ultra-fast inference for Llama 3, Mixtral | Free tier with rate limits |
| **OpenRouter** | [openrouter.ai](https://openrouter.ai) | Routes to dozens of free open-source models | Some models have free endpoints |
| **ChatGPT** | [chatgpt.com](https://chatgpt.com) | GPT-4o mini free tier | Rate limited |

---

## 📈 SEO Scoring & Optimization (Replace vidIQ Video Optimizations)

| Tool | URL | What's Free | Limits |
|---|---|---|---|
| **TubeBuddy (Free)** | [tubebuddy.com](https://www.tubebuddy.com) | Browser extension: SEO scorecard, basic tag suggestions, basic title optimization | Limited depth, no bulk processing, no A/B testing |
| **YouTube Studio "Research" tab** | Built into Studio | Search gap analysis from YouTube's own backend | Only for your channel |

---

## 👥 Subscriber/Audience Insights (Replace vidIQ Subscriber Insights)

| Tool | What's Free |
|---|---|
| **YouTube Studio → Analytics → Audience tab** | "What your audience watches" + "Channels your audience watches" — first-party data, more accurate than vidIQ |
| **Social Blade** | Public growth data for any channel |
| **NoxInfluencer** | Audience demographics estimates for public channels |

---

## Your vidIQ Multi-Account Strategy — How It Maps

With 5 vidIQ free accounts rotated through the MCP:

| Feature | Per Account | × 5 Accounts | Daily Total |
|---|---|---|---|
| Monthly credits | 150 | 750 | — |
| Daily login bonus | +20 | +100 | 100 credits/day |
| Keyword research | 3/day | 15/day | 15 searches |
| Outlier research | 3/day | 15/day | 15 searches |
| Video ideas | 3/day | 15/day | 15 ideas |

This is decent for vidIQ-specific features (keyword scores, outlier detection). But for everything else, the free tools above are better and unlimited.

---

# PART 2 — API Setup & Configuration

## 1. YouTube Data API v3 (Free — 10,000 units/day)

### Setup:
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project (e.g., "YouTube-Research")
3. Enable **YouTube Data API v3** from the API Library
4. Go to Credentials → Create API Key
5. Save the key

### Quota Costs:

| Endpoint | Cost | What It Does | Daily Max (free) |
|---|---|---|---|
| `search.list` | **100 units** | Search YouTube, find videos by keyword | 100 calls |
| `videos.list` | **1 unit** | Get video stats (views, likes, comments) | 10,000 calls |
| `channels.list` | **1 unit** | Get channel stats (subs, views, video count) | 10,000 calls |
| `commentThreads.list` | **1 unit** | Get video comments | 10,000 calls |

### Pro Tip:
Don't waste `search.list` (100 units) to find videos. Instead:
- Use YouTube autocomplete to find keywords
- Use YouTube RSS feeds (`https://www.youtube.com/feeds/videos.xml?channel_id=CHANNEL_ID`) to get recent video IDs for free
- Then use `videos.list` (1 unit) to pull stats on those IDs in bulk

---

## 2. YouTube Autocomplete Endpoint (Free — No API Key Needed)

```
GET http://suggestqueries.google.com/complete/search?client=firefox&ds=yt&q=YOUR_KEYWORD
```

- `client=firefox` → returns clean JSON
- `ds=yt` → filters for YouTube only
- No API key required
- Returns real-time search suggestions

### Python Script:
```python
import requests
import json

def get_youtube_suggestions(keyword):
    url = f"http://suggestqueries.google.com/complete/search?client=firefox&ds=yt&q={keyword}"
    response = requests.get(url)
    suggestions = json.loads(response.text)[1]
    return suggestions

# Example: Get suggestions for "stickman"
results = get_youtube_suggestions("stickman animation")
for s in results:
    print(s)
```

### A-Z Expansion (bulk keyword extraction):
```python
def bulk_suggestions(seed_keyword):
    all_suggestions = []
    for letter in 'abcdefghijklmnopqrstuvwxyz':
        query = f"{seed_keyword} {letter}"
        suggestions = get_youtube_suggestions(query)
        all_suggestions.extend(suggestions)
    return list(set(all_suggestions))  # deduplicate

keywords = bulk_suggestions("stickman tutorial")
print(f"Found {len(keywords)} keyword ideas")
for kw in sorted(keywords):
    print(f"  - {kw}")
```

---

## 3. pytrends — Google Trends for YouTube (Free)

### Install:
```bash
pip install pytrends
```

### Usage:
```python
from pytrends.request import TrendReq

pytrends = TrendReq(hl='en-US', tz=330)  # IST timezone

# Compare keywords on YouTube specifically
kw_list = ["stickman animation", "stick figure fight", "stickman tutorial"]
pytrends.build_payload(kw_list, timeframe='today 12-m', geo='IN', gprop='youtube')

# Get interest over time (0-100 scale)
data = pytrends.interest_over_time()
print(data)

# Get related queries (gold mine for video ideas)
related = pytrends.related_queries()
for kw in kw_list:
    print(f"\n--- Related to '{kw}' ---")
    if related[kw]['rising'] is not None:
        print(related[kw]['rising'].head(10))
```

### Rate Limiting:
- Add `time.sleep(2)` between requests
- Don't run more than ~30 requests per hour
- Use `requests_args={'timeout': 10}` for stability

---

## 4. Free AI APIs

### Gemini API (Google AI Studio):
1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Get API key (free)
3. Use Gemini 2.5 Flash — generous free tier

```python
import google.generativeai as genai

genai.configure(api_key="YOUR_API_KEY")
model = genai.GenerativeModel("gemini-2.5-flash")

response = model.generate_content(
    "Generate 10 YouTube title ideas for a stickman animation video "
    "about teaching physics concepts. Make them high-CTR, under 60 characters, "
    "with emotional hooks."
)
print(response.text)
```

### Groq (Ultra-fast, Free):
1. Go to [console.groq.com](https://console.groq.com)
2. Get API key (free)
3. Supports Llama 3, Mixtral

---

## 5. Rotating vidIQ MCP API Keys

To switch between your 5 vidIQ accounts in Antigravity, you just need to update the API key in the MCP config. When you want to use a different account's credits, provide me the new API key and I'll use that account's allocation.

---

# PART 3 — Full Creator Workflow

## Video Idea → Published Video (₹0 Stack)

```
┌─────────────────────────────────────────────────────┐
│  STEP 1: FIND TOPIC                                 │
│  ├─ Google Trends (YouTube filter) → trending       │
│  ├─ YouTube Autocomplete script → long-tail ideas   │
│  ├─ vidIQ MCP outlier search → viral in your niche  │
│  └─ YouTube Studio Research tab → search gaps        │
├─────────────────────────────────────────────────────┤
│  STEP 2: VALIDATE DEMAND                            │
│  ├─ pytrends → compare keyword interest             │
│  ├─ Analyze AI → check search volume (if available) │
│  └─ YouTube search → check existing competition     │
├─────────────────────────────────────────────────────┤
│  STEP 3: RESEARCH COMPETITORS                       │
│  ├─ YouTube Data API → pull stats on top videos     │
│  ├─ NoxInfluencer → channel-level comparison        │
│  ├─ Social Blade → growth trends                    │
│  └─ Watch top 3-5 videos → note hooks, structure    │
├─────────────────────────────────────────────────────┤
│  STEP 4: WRITE SCRIPT                               │
│  ├─ Gemini API or ChatGPT → generate script draft   │
│  ├─ Structure: Hook (0-30s) → Problem → Solution    │
│  └─ Review and personalize (AI is the starting      │
│     point, not the final product)                   │
├─────────────────────────────────────────────────────┤
│  STEP 5: CREATE THUMBNAIL                           │
│  ├─ Pivot Animator / Stick Nodes → stickman pose    │
│  ├─ Canva → assemble with background + text         │
│  ├─ TestMyThumbnails → preview in YouTube layouts   │
│  └─ Rules: high contrast, ≤5 words, faces/emotion   │
├─────────────────────────────────────────────────────┤
│  STEP 6: OPTIMIZE SEO (Before Upload)               │
│  ├─ Title: Use Gemini to generate 5-10 options      │
│  ├─ Tags: YouTube Autocomplete + TubeBuddy free     │
│  ├─ Description: Gemini API → keyword-rich desc     │
│  └─ TubeBuddy SEO Scorecard → check score           │
├─────────────────────────────────────────────────────┤
│  STEP 7: UPLOAD & PUBLISH                           │
│  ├─ Upload to YouTube Studio                        │
│  ├─ Set end screens + cards                         │
│  ├─ Schedule for optimal time (check Studio →       │
│  │   Analytics → "When your viewers are online")    │
│  └─ Share first 48 hours → key for algorithm push   │
├─────────────────────────────────────────────────────┤
│  STEP 8: POST-PUBLISH ANALYSIS                      │
│  ├─ YouTube Studio → watch CTR + retention at 24h   │
│  ├─ If CTR < 4%: change thumbnail                   │
│  ├─ If retention drops at 30s: fix future hooks     │
│  └─ Track in spreadsheet for pattern recognition    │
└─────────────────────────────────────────────────────┘
```

---

## Quick Reference: What Replaces What

| vidIQ Paid Feature | Your Free Replacement | Better/Worse/Same? |
|---|---|---|
| Keyword volume/competition | Google Trends + Analyze AI + Autocomplete script | ⚠️ 70% as good (no exact numbers) |
| Outlier video discovery | OutlierKit + vidIQ MCP (5 accounts × 3/day) | ✅ Same |
| Subscriber insights | YouTube Studio Audience tab | ✅ Better (first-party data) |
| Video optimizations | TubeBuddy free + Gemini API | ✅ Same |
| Thumbnail AI | Pivot Animator + Canva + TestMyThumbnails | ✅ Better (more control) |
| Competitor tracking | Social Blade + NoxInfluencer + YouTube API | ✅ Same |
| AI titles/descriptions | Gemini API / ChatGPT | ✅ Same or better |
| Trend alerts | Google Trends + pytrends script | ⚠️ Manual (no push notifications) |

**Total cost: ₹0/month**
**Coverage vs vidIQ Boost: ~85%**
**The missing 15%:** Exact keyword volume numbers + automated trend push notifications

---

> [!TIP]
> **Your biggest edge isn't tools — it's workflow consistency.** The creators who grow fastest aren't using better tools. They're publishing consistently, studying their analytics weekly, and iterating on what works. This free stack gives you everything you need. The constraint is execution, not software.
