# Hire Overseas MCP

Let your AI assistant find remote talent for you. This connects Claude, ChatGPT, Cursor and other MCP clients to [Hire Overseas](https://www.hireoverseas.com)'s pool of remote professionals in the Philippines, Latin America and Africa.

**Server URL:** `https://api.hireoverseas.com/mcp` (Streamable HTTP, no account or key needed)

Ask things like:

- "Find me a bookkeeper in the Philippines who knows QuickBooks and Xero."
- "I need an SDR with B2B SaaS cold-calling experience who can work US hours."
- "Show me executive assistants in Latin America with 5+ years of experience."

## Tools

| Tool | What it does |
| --- | --- |
| `search_candidates` | Up to 5 anonymized profiles for a role, in a few seconds. |
| `request_intro` | Asks Hire Overseas to introduce you to a candidate. Needs your company and work email. |
| `get_request_status` | Whether an introduction request is still pending. |

## Privacy

Profiles show a first name, country, timezone, skills, experience and work history by job title and industry. They never include a surname, contact details, links or employer names. Hire Overseas screens and verifies each candidate, and confirms availability and pricing, before making an introduction.

## Install

### Claude Code

```
/plugin marketplace add Hire-Overseas/hire-overseas-mcp
/plugin install hire-overseas@hire-overseas
```

This adds the server and a skill that scopes the role before searching. For the server alone:

```
claude mcp add --transport http hire-overseas https://api.hireoverseas.com/mcp
```

### Claude (claude.ai and desktop)

Settings → Connectors → Add custom connector → paste `https://api.hireoverseas.com/mcp`.

### ChatGPT

Settings → Apps & Connectors → Advanced → turn on Developer mode, then Create and paste `https://api.hireoverseas.com/mcp` with no authentication.

### Cursor, VS Code and other MCP clients

```json
{
  "mcpServers": {
    "hire-overseas": { "url": "https://api.hireoverseas.com/mcp" }
  }
}
```

### APIs (Anthropic, OpenAI, xAI)

Pass the URL as a remote MCP server in the request's tools. No authorization token is required.

## Limits

Anonymous use is limited to 10 requests a minute and 100 a day per address. Searches return at most 5 profiles.

## Contact

[hireoverseas.com](https://www.hireoverseas.com)
