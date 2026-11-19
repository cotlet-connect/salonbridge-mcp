# SalonBridge MCP server for ChatGPT and Claude

**Yes, ChatGPT, Claude and other AI agents can work in your SalonBridge account.** Cotlet.dev connects your signed-in Cloud Browser to a hosted SalonBridge MCP server for appointments, clients, payments, stock and reports. Write actions ask for your confirmation by default.

## What you can ask

> Book a client into the calendar for a service and staff member, after I confirm.

> Find the messages sent to a client last week.

> Show the form responses linked to a client.

> Review last month's income, expenses and net profit.

> Show the staff working roster for next week.

## Connect your agent

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1/connect` under Settings > Connectors and sign in to Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its SalonBridge tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

Or with Docker:

```bash
docker build -t salonbridge-mcp .
docker run -i --rm -e COTLET_API_KEY salonbridge-mcp
```

Tools: `salonbridge_guide`, `salonbridge_status`, `salonbridge_open`, `salonbridge_read`, `salonbridge_click`, `salonbridge_type`, `salonbridge_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 salonbridge_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 salonbridge_agent.py status    # is SalonBridge ready in your Cotlet.dev account
python3 salonbridge_agent.py guide     # SalonBridge screens and sign-in link
python3 salonbridge_agent.py read      # open SalonBridge, read the page, close the browser
python3 salonbridge_agent.py tools     # list Cotlet.dev tools
python3 salonbridge_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from SalonBridge users

**Does SalonBridge have an API?**

The Cotlet.dev integration page links to SalonBridge API documentation at developers.mysalonbridge.com, checked 16 November 2026. Cotlet.dev works in your signed-in SalonBridge console.

**How do I connect SalonBridge to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=salonbridge, enable SalonBridge and sign in at online.mysalonbridge.com in your Cotlet.dev Cloud Browser. Add https://cotlet.dev/mcp/v1/connect to ChatGPT with OAuth.

**Can I use SalonBridge with Claude?**

Yes. Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev.

**Is this an official SalonBridge MCP server?**

No. Cotlet.dev is independent and not affiliated with SalonBridge. Your SalonBridge package and staff permissions determine which work you can do.

## Source and setup

[SalonBridge integration page](https://cotlet.dev/integrations/salonbridge-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=salonbridge)

---

More: https://cotlet.dev/integrations/salonbridge-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=salonbridge

Start free: https://cotlet.dev/signup?app=salonbridge&utm_source=github&utm_medium=readme&utm_campaign=salonbridge
