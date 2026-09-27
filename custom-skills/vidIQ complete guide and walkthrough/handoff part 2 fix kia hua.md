# 🔄 Handoff v2: vidIQ MCP — FIXED (Python Bridge)

> **From conversation**: `58fac529-713a-4214-93cb-f4e1e2eb6964`
> **Date**: 2026-08-01
> **Status**: FIXED — switched from slow `mcp-remote` to fast Python bridge

---

## What Was Wrong & How It Was Fixed

### The Problem
`mcp-remote` (the Node.js SSE↔stdio bridge) took **8-10 seconds** to start up because it had to:
1. Download itself via npx
2. Discover OAuth configuration
3. Do the OAuth/token handshake
4. Establish the proxy

Antigravity's MCP loader has a **startup timeout** shorter than this, so it **silently dropped the vidIQ server**.

### The Fix
Replaced `mcp-remote` with a **fast Python bridge** at:
`C:\Users\renu5\.gemini\antigravity\scratch\vidiq_bridge\vidiq_mcp_bridge.py`

This bridge:
- Starts in **<1 second** (Python, no npm download)
- Reads cached OAuth tokens directly from `~/.mcp-auth/`
- Falls back to API key from environment variable
- Forwards all tool calls to vidIQ's MCP server via HTTP
- Uses the **exact same pattern** as the working `cloud_llm_bridge.py`

### Verified Working
```
✅ MCP handshake: SUCCESS
✅ Tool discovery: 17 tools registered (6 free, 9 standard, 2 heavy)
✅ Startup time: <1 second
✅ Both configs updated (mcp.json + mcp_config.json)
```

---

## What To Test NOW

### Test 1: Check if vidIQ MCP loaded
Just ask: "What MCP servers are available?" — you should see `vidiq` in the list.

### Test 2: Check Credit Balance (0 credits)
```
Use the vidIQ MCP tool credits_balance to check my credit balance
```

### Test 3: List Connected Channels (0 credits)
```
Use the vidIQ MCP tool your_connected_channels
```

### Test 4: Browse Trending Categories (0 credits)
```
Use the vidIQ MCP tool trend_categories
```

---

## If OAuth Token Expired (401 Error)

The cached OAuth token at `C:\Users\renu5\.mcp-auth\` expires hourly but has a refresh token. If you get a 401:

1. Open terminal and run:
```
npx -y mcp-remote https://mcp.vidiq.com/mcp --header "Authorization: Bearer vidiq_rFQ_LgHczDP05RYs7rtwGKdRyceUFUupg3joo_Uq"
```
2. Authorize in the browser window that opens
3. Press Ctrl+C once connected
4. The token is now refreshed — restart Antigravity and try again

---

## User Context (for new agent)

- **Name**: Priyanshu
- **YouTube status**: Starting new channel, no uploads yet
- **Languages**: Multiple (Hindi, English, Hinglish)
- **Niche**: Not decided — wants niche-agnostic workflows
- **Credits**: ~170/month free tier
- **API Key**: `vidiq_rFQ_LgHczDP05RYs7rtwGKdRyceUFUupg3joo_Uq`
- **Strategy**: Single key, swap when exhausted (has ~10 Gmail accounts)
- **Skill installed**: `C:\Users\renu5\.gemini\config\skills\vidiq-youtube-creator\`
