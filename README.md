# BonBook Travel

Book flights by chatting with your AI assistant. BonBook is a licensed travel agency, and this connector works with any MCP client — Claude, Cursor, Grok Bot, and others.

```
Connector URL:  https://mcp.bonbook.co/mcp
```

No account, no password, no card. Your first booking opens a bonbook.co checkout page; after that you book by saying "book option 2."

## Set up

**Claude (web or desktop app)**

1. Open **Settings → Connectors → Add custom connector**. Paste `https://mcp.bonbook.co/mcp` and click **Add**.
2. Click **Connect**. A BonBook page appears for a second and closes by itself.
3. Start a new chat and type where you want to go.

**Claude Code** — one line in your terminal, then `/mcp` to sign in:

```
claude mcp add --transport http --scope user bonbook https://mcp.bonbook.co/mcp
```

**Cursor and other MCP clients** — add a remote MCP server:

- Transport: **Streamable HTTP**
- URL: `https://mcp.bonbook.co/mcp`
- Auth: **OAuth** (discovered automatically; dynamic registration is supported)

```json
{
  "mcpServers": {
    "bonbook": { "url": "https://mcp.bonbook.co/mcp" }
  }
}
```

**Grok Bot** — install **BonBook Travel** from the **Connect apps** sidebar.

## Want your assistant to walk you through it?

Paste this link into your assistant and say "set up BonBook Travel for me":
https://github.com/aSzelem/bonbook-travel/blob/main/SKILL.md

## Things to say

- "Austin AUS to LAX next Friday, back Sunday, 2 adults"
- "Show me more options" · "Details on option 3"
- "Book option 2"
- "What trips do I have?" · "Cancel my Denver trip"

Every booking is confirmed by email and reversible within 24 hours via support@bonbook.co.

[Privacy](https://bonbook.co/privacy) · [Terms](https://bonbook.co/terms) · support@bonbook.co
