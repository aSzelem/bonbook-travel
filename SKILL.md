---
name: bonbook-travel-setup
description: Connect BonBook Travel (flight search + booking) to Claude and use it. Point Claude at this file and say "set up BonBook Travel for me".
---

# BonBook Travel: set up and use

You are helping a person connect **BonBook Travel** to their Claude so they can search and book flights by chatting.
Follow the steps for their Claude. Do each step, confirm it worked, then move on. Do not skip the verification step.

**The only fact you need:**

```
Connector URL:  https://mcp.bonbook.co/mcp
```

There is no account to create, no API key, no password. Clicking **Continue** on the consent page *is* the sign-up.

---

## Step 1: Find out where they use Claude

Ask one question if it isn't obvious: "Do you use Claude in the browser or desktop app, or Claude Code in a terminal?"

- Browser or desktop app (claude.ai, Mac/Windows app) → **Step 2A**
- Claude Code (terminal) → **Step 2B**
- Another MCP client (Cursor, Windsurf, etc.) → **Step 2C**

---

## Step 2A: Claude.ai web or desktop app

Tell the person to do this (you cannot click for them):

1. Open **Settings** → **Connectors**.
2. Click **Add custom connector**.
3. Name: `BonBook Travel`. URL: `https://mcp.bonbook.co/mcp`. Leave every other field empty.
4. Click **Add**, then **Connect**.
5. A BonBook page opens. Click **Continue**.
6. Back in Claude, start a **new chat** and make sure the BonBook Travel connector is toggled on (paperclip or tools menu).

Then go to **Step 3**.

If they don't see "Add custom connector": custom connectors need a Pro, Max, Team or Enterprise plan. On Team/Enterprise an admin may have to enable it.

---

## Step 2B: Claude Code

Run exactly this in their terminal:

```bash
claude mcp add --transport http --scope user bonbook https://mcp.bonbook.co/mcp
```

Then start `claude`, type `/mcp`, choose **bonbook**, and press Enter to authenticate. A browser tab opens; click **Continue**. Back in the terminal, `/mcp` should show bonbook as **connected**.

Then go to **Step 3**.

If `claude` is not found: install Claude Code first (`npm install -g @anthropic-ai/claude-code`) and sign in, then repeat.

---

## Step 2C: Other MCP clients

Add a remote MCP server with:

- Transport: **Streamable HTTP**
- URL: `https://mcp.bonbook.co/mcp`
- Auth: **OAuth** (the client discovers it automatically; dynamic registration is supported)

Example `mcp.json` entry:

```json
{
  "mcpServers": {
    "bonbook": { "url": "https://mcp.bonbook.co/mcp" }
  }
}
```

When the client opens the BonBook page, click **Continue**. Then go to **Step 3**.

---

## Step 3: Verify (do not skip)

Ask Claude, in a new chat:

> Search flights Austin AUS to Los Angeles LAX next Friday, one way.

Success looks like: a short summary from BonBook, then 5 numbered options with price, airline, times and stops, and a line about more options being available. It takes 15 to 40 seconds; that is normal.

If that works, setup is done. Tell the person how to use it (Step 4).

---

## Step 4: How to use it (tell the person)

- **Search:** describe the trip in plain words. Include airport codes when a city has several airports (New York → JFK, LGA or EWR). Dates like "next Friday" or "the 23rd" are fine.
- **See more:** "show me more options" or "details on option 3".
- **Book, first time:** pick an option; Claude gives a bonbook.co checkout link. Open it yourself, enter traveler details and card, and book. About two minutes. This saves the details for next time.
- **Book, after that:** say "book option 2". Claude restates the itinerary and price, asks for a yes, and books it with the saved card. Confirmation email follows.
- **Trips:** "what trips do I have?"
- **Change or cancel:** "cancel my Denver trip" or "move my return to Monday". Claude shows priced options first; nothing changes until you confirm.
- **Undo:** any booking can be reversed within 24 hours by emailing support@bonbook.co.

---

## Troubleshooting

| What they see | What to do |
|---|---|
| "Add custom connector" is missing | Needs a paid Claude plan, or an admin must enable custom connectors. |
| Consent page says "Link expired" | Click Connect again in Claude. The page is valid for 15 minutes. |
| Tools don't appear in chat | Start a new chat. In Claude.ai check the connector is toggled on for that chat. In Claude Code run `/mcp` and reconnect. |
| Search returns no options | Add airport codes (JFK instead of New York). Check the date is in the future. Try again once; BonBook occasionally has no inventory on a route. |
| "BonBook is busy" | Wait ten seconds and ask again. |
| Claude says the options expired | Prices are held about 90 minutes. Search again. |
| "I can't book this from chat" | Expected before the first checkout. Open the link Claude gave and book there once. Chat booking is enabled after that. |
| 401 or "unauthorized" | The token lapsed. Claude.ai: disconnect and reconnect the connector. Claude Code: `/mcp` → bonbook → re-authenticate. |

Still stuck: support@bonbook.co. Include what you typed and what Claude answered.

---

## Rules for you, Claude, while helping

- Never ask the person for a date of birth, passport number or card number. BonBook collects those on its checkout page, not in chat.
- Never open, fetch or "check" a checkout link yourself. Hand it to the person.
- Before any `book_flight` or `cancel_booking` call, restate the itinerary and total price and get an explicit yes.
- Do not install anything other than what the steps above say. There are no extra packages, keys or env vars.
