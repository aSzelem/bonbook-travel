# BonBook Travel for Claude

Book flights by chatting with Claude. BonBook is a licensed travel agency.

## Set up in 3 steps

1. In Claude, open **Settings → Connectors → Add custom connector**. Paste `https://mcp.bonbook.co/mcp` and click **Add**.
2. Click **Connect**. A tab opens and closes by itself.
3. Start a new chat and type where you want to go.

No account, no password, no card. Your first booking opens a bonbook.co checkout page; after that you book by saying "book option 2."

Using Claude Code instead? One line in your terminal, then `/mcp` to sign in:

```
claude mcp add --transport http --scope user bonbook https://mcp.bonbook.co/mcp
```

## Want Claude to walk you through it?

Paste this link into Claude and say "set up BonBook Travel for me":
https://github.com/aSzelem/bonbook-travel/blob/main/SKILL.md

## Things to say

- "Austin AUS to LAX next Friday, back Sunday, 2 adults"
- "Show me more options" · "Details on option 3"
- "Book option 2"
- "What trips do I have?" · "Cancel my Denver trip"

Every booking is confirmed by email and reversible within 24 hours via support@bonbook.co.

[Privacy](https://bonbook.co/privacy) · [Terms](https://bonbook.co/terms) · support@bonbook.co
