# Walkthrough — vidIQ MCP Integration Complete

## What Was Built

### 1. ✅ MCP Server Connection (Both Versions)

Added vidIQ MCP server to **both** Antigravity configs using `mcp-remote` as a stdio↔SSE bridge:

**[mcp.json](file:///C:/Users/renu5/.gemini/config/mcp.json)** (Antigravity 2.1.4)
```json
"vidiq": {
  "command": "npx",
  "args": ["-y", "mcp-remote", "https://mcp.vidiq.com/mcp",
           "--header", "Authorization: Bearer PASTE_YOUR_VIDIQ_API_KEY_HERE"]
}
```

**[mcp_config.json](file:///C:/Users/renu5/.gemini/config/mcp_config.json)** (Antigravity IDE 2.1.1)
— Same entry added.

> [!IMPORTANT]
> You must replace `PASTE_YOUR_VIDIQ_API_KEY_HERE` with your real vidIQ API key (the one starting with `vidiq_rFQ...`), then **restart both Antigravity versions** for it to take effect.

---

### 2. ✅ YouTube Creator Skill (Shared Across Both Versions)

Created at: [vidiq-youtube-creator/](file:///C:/Users/renu5/.gemini/config/skills/vidiq-youtube-creator/)

| File | Size | Purpose |
|------|------|---------|
| [SKILL.md](file:///C:/Users/renu5/.gemini/config/skills/vidiq-youtube-creator/SKILL.md) | 7KB | Main skill — triggers on any YouTube/vidIQ mention, contains all tool definitions, credit rules |
| [tools-reference.md](file:///C:/Users/renu5/.gemini/config/skills/vidiq-youtube-creator/references/tools-reference.md) | 10KB | Complete reference for all 17 tools with parameters, costs, examples |
| [workflow-templates.md](file:///C:/Users/renu5/.gemini/config/skills/vidiq-youtube-creator/references/workflow-templates.md) | 8KB | 8 pre-built niche-agnostic workflow templates with step-by-step guides |
| [credit-strategy.md](file:///C:/Users/renu5/.gemini/config/skills/vidiq-youtube-creator/references/credit-strategy.md) | 5KB | Credit management, warning thresholds, key swap instructions |

**Skill auto-triggers on**: YouTube, vidIQ, content creation, video SEO, keyword research, thumbnails, titles, trending, competitor analysis, channel analytics, shorts, clips, "what should I make a video about", "go viral", "niche research"

---

### 3. ✅ Portable Reference Guide

Created at: [vidiq-complete-guide.md](file:///C:/Users/renu5/.gemini/antigravity/brain/58fac529-713a-4214-93cb-f4e1e2eb6964/vidiq-complete-guide.md)

A standalone markdown you can reference from any conversation — contains setup, all tools, workflow quick-ref, and credit rules.

---

## What Was Tested

| Test | Result |
|------|--------|
| mcp.json valid JSON | ✅ Passed |
| mcp_config.json valid JSON | ✅ Passed |
| Skill directory structure correct | ✅ 4 files created |
| SKILL.md under 500 lines | ✅ ~130 lines |

---

## 🔴 ONE ACTION REQUIRED FROM YOU

Open **both** config files and replace `PASTE_YOUR_VIDIQ_API_KEY_HERE` with your real API key:

```
Your key: vidiq_rFQ...  (the full key you generated earlier)
```

**Files to edit:**
1. [mcp.json](file:///C:/Users/renu5/.gemini/config/mcp.json) — line 37
2. [mcp_config.json](file:///C:/Users/renu5/.gemini/config/mcp_config.json) — line 43

Then **restart both Antigravity applications**.

After restart, test by saying in a new conversation:
> "Check my vidIQ credit balance"

If the skill triggers and returns your balance, everything is working. 🎉

---

## If Something Goes Wrong

| Problem | Solution |
|---------|----------|
| "Tool not found" after restart | `mcp-remote` might need Node.js 18+. Run `node --version` to check. |
| Connection timeout | vidIQ server might be down. Try again in a few minutes. |
| 401 Unauthorized | API key is wrong or expired. Generate a new one at https://app.vidiq.com/account/settings/mcp |
| Tools appear but return errors | Free tier might have different tool access. Start with `credits_balance` (guaranteed free). |
| `mcp-remote` not found | Run `npm install -g mcp-remote` to install globally, or ensure npx works: `npx -y mcp-remote --help` |
