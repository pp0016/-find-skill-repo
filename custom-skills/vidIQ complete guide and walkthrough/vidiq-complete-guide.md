# vidIQ MCP — Complete Guide for YouTube Creators

> **Portable Reference**: Copy-paste this into any conversation to get full vidIQ MCP context.

---

## Quick Setup

### Antigravity 2.1.4 (newer)
Config file: `C:\Users\renu5\.gemini\config\mcp.json`

### Antigravity IDE 2.1.1 (older)
Config file: `C:\Users\renu5\.gemini\config\mcp_config.json`

Both use the same entry:
```json
"vidiq": {
  "command": "npx",
  "args": [
    "-y",
    "mcp-remote",
    "https://mcp.vidiq.com/mcp",
    "--header",
    "Authorization: Bearer YOUR_API_KEY"
  ]
}
```

### Get/Replace API Key
1. Go to https://app.vidiq.com/account/settings/mcp
2. Generate API key
3. Replace `YOUR_API_KEY` in the config above
4. Restart the application

---

## All Available Tools

| Tool | Credits | Category | Purpose |
|------|---------|----------|---------|
| `credits_balance` | 0 | Utility | Check remaining credits |
| `your_connected_channels` | 0 | Utility | List linked YouTube/Instagram channels |
| `async_job_tracking` | 0 | Utility | Check async job status |
| `voice_library` | 0 | Utility | List AI voice options |
| `trend_categories` | 0 | Utility | Browse trending categories/niches |
| `feedback` | 0 | Utility | Submit feedback to vidIQ |
| `keyword_research` | 5 | Standard | Search volume, competition, keyword opportunities |
| `outliers` | 5 | Standard | Find videos that went viral beyond channel baseline |
| `trending_videos` | 5 | Standard | Real-time trending content by category |
| `video_transcript` | 5 | Standard | Extract full transcript of any YouTube video |
| `channel_analytics` | 5 | Standard | Channel health report (subs, views, growth) |
| `subscriber_insights` | 5 | Standard | Audience demographics and best post times |
| `generate_titles` | 5 | Standard | AI-generated high-CTR title ideas |
| `generate_thumbnail` | 5 | Standard | Thumbnail concepts and visual briefs |
| `generate_clips` | 5 | Standard | Find clip-worthy timestamps for Shorts |
| `video_watch` | 10 | Heavy | Deep multimodal video analysis |
| `reel_watch` | 10 | Heavy | Deep Instagram Reel analysis |

---

## Workflow Quick Reference

| Workflow | Cost | Best For |
|----------|------|----------|
| **New Channel Launch** | ~35 credits | Starting a channel, entering a niche |
| **Weekly Planning** | ~25 credits | Weekly content calendar |
| **Video SEO** | ~10 credits | Optimizing a single video |
| **Competitor Dive** | ~20 credits | Deep competitor analysis |
| **Shorts Strategy** | ~15 credits | Short-form content planning |
| **Daily Check-in** | 0 credits | Daily trend scanning |
| **Viral Breakdown** | ~10-20 credits | Understanding why a video went viral |

---

## Credit Rules

- **170 credits/month** on free tier (no rollover)
- Always check `credits_balance` first (free)
- Never chain >3 paid calls without user confirmation
- When <20 credits remaining → free tools only
- When 0 credits → swap to new API key from different Gmail account

---

## Key Swap Process

1. Log into vidiq.com with different Gmail
2. Account Settings → MCP → Generate API Key
3. Replace old key in mcp.json / mcp_config.json
4. Restart Antigravity
5. Verify with `credits_balance`

---

*Skill installed at: `C:\Users\renu5\.gemini\config\skills\vidiq-youtube-creator\`*
*This guide generated: 2026-07-31*
