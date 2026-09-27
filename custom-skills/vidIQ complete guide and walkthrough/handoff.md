# 🔄 Handoff: vidIQ MCP Integration — Ready to Test

> **From conversation**: `58fac529-713a-4214-93cb-f4e1e2eb6964`
> **Date**: 2026-07-31
> **Status**: Setup COMPLETE — needs new conversation to activate MCP

---

## What Was Done (Don't Repeat This)

### 1. ✅ MCP Server Configured in BOTH Antigravity Versions

**Antigravity 2.1.4** — `C:\Users\renu5\.gemini\config\mcp.json`:
```json
"vidiq": {
  "command": "npx",
  "args": ["-y", "mcp-remote", "https://mcp.vidiq.com/mcp",
           "--header", "Authorization: Bearer vidiq_rFQ_LgHczDP05RYs7rtwGKdRyceUFUupg3joo_Uq"]
}
```

**Antigravity IDE 2.1.1** — `C:\Users\renu5\.gemini\config\mcp_config.json`:
Same entry added.

**Connection was tested** via terminal — `mcp-remote` successfully connects:
```
Connected to remote server using StreamableHTTPClientTransport
Proxy established successfully between local STDIO and remote StreamableHTTPClientTransport
```

OAuth token is cached at `C:\Users\renu5\.mcp-auth\mcp-remote-0.1.37\` — includes refresh token.

### 2. ✅ Skill Installed

Location: `C:\Users\renu5\.gemini\config\skills\vidiq-youtube-creator\`

Files:
- `SKILL.md` — Main skill (auto-triggers on YouTube/vidIQ mentions)
- `references/tools-reference.md` — All 17 tools with parameters and costs
- `references/workflow-templates.md` — 8 pre-built niche-agnostic workflows
- `references/credit-strategy.md` — Credit management and key rotation guide

### 3. ✅ Portable Guide Created

At: `C:\Users\renu5\.gemini\antigravity\brain\58fac529-713a-4214-93cb-f4e1e2eb6964\vidiq-complete-guide.md`

---

## What To Test NOW (All Free — 0 Credits)

### Test 1: Check Credit Balance
```
Check my vidIQ credit balance
```
Expected: Returns current credits (should be ~170 for free tier)

### Test 2: List Connected Channels
```
Show my connected YouTube channels
```
Expected: Returns list of YouTube/Instagram channels linked to the vidIQ account

### Test 3: Browse Trending Categories
```
Show me trending content categories on YouTube
```
Expected: Returns list of content categories and niches

### Test 4: List Voice Options
```
What AI voices does vidIQ offer?
```
Expected: Returns available voice options

---

## User Context

- **Name**: Priyanshu
- **YouTube status**: Starting a new channel (no uploads yet)
- **Languages**: Multiple (Hindi, English, Hinglish)
- **Niche**: Not decided — wants niche-agnostic workflows
- **Credits**: ~170/month free tier, has ~10 Gmail accounts for key rotation
- **Strategy**: Single active key, manual swap when exhausted (safe approach)
- **Goal**: Use vidIQ MCP data as a long & short form YouTube creator

## If Something Breaks

| Symptom | Fix |
|---------|-----|
| "Tool not found" / "Server not loaded" | vidIQ MCP didn't start. Check if Node.js 18+ is installed (`node --version`) |
| OAuth authorization popup | Click "Authorize" in the browser window that opens |
| 401 Unauthorized | OAuth token expired. Delete `C:\Users\renu5\.mcp-auth\` folder and re-authorize |
| "context deadline exceeded" | Browser auth window timed out — click faster next time, or re-run |
| Credits = 0 | Generate new API key from different Gmail at https://app.vidiq.com/account/settings/mcp |

## Key Rotation Process

When credits run out:
1. Log into vidiq.com with different Gmail
2. Account Settings → MCP → Generate API Key
3. Update key in `C:\Users\renu5\.gemini\config\mcp.json` (line 37)
4. Also update `C:\Users\renu5\.gemini\config\mcp_config.json` (line 43)
5. Delete `C:\Users\renu5\.mcp-auth\` folder (clear old OAuth)
6. Restart Antigravity
7. Authorize in browser when prompted
