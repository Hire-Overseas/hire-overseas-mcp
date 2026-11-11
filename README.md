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
| `get_candidate_resume` | A candidate's resume as text, with surname, contact details, links and employer names removed. |
| `request_intro` | Asks Hire Overseas to introduce you to a candidate. Needs your company and work email. |
| `get_request_status` | Whether an introduction request is still pending. |

## Tool reference

Transport: MCP Streamable HTTP at `https://api.hireoverseas.com/mcp`. No authentication. Every tool returns JSON as text.

| Tool | Class | Side effects |
| --- | --- | --- |
| `search_candidates` | Read | None. |
| `get_candidate_resume` | Read | None. |
| `get_request_status` | Read | None. |
| `request_intro` | Write | Creates one introduction request and notifies the Hire Overseas team. Nothing is sent to the candidate or any third party, and no payment is involved. Not idempotent: each call creates a new request. |

No tool is destructive, and none moves money.

### `search_candidates`

Inputs: `roleTitle` (string, required), `description` (string), `skills` (string array), `minYearsExperience` (integer), `regions` (array of `ph`, `latam`, `africa`; all three when omitted).

Output: `count` and up to 5 `candidates`. Each has `candidateRef`, `firstName`, `headline`, `skills`, `experience` (a band such as "5-8 years"), `country`, `timezone`, `englishLevel`, `workHistory`, `whyMatched`, `resumeAvailable`, `introVideoAvailable` and, when a video exists, `introVideoUrl` (expires after 24 hours).

### `get_candidate_resume`

Input: `candidateRef` from a search. Output: `resume`, the resume as text with the surname, contact details, links, employer names, city and referees removed. Returns an error when the candidate has no resume or the reference is not valid.

### `request_intro`

Inputs: `candidateRef`, `roleTitle`, `clientName` (the requester's company), `clientContact` (the requester's work email), `message` (optional, up to 2000 characters).

Output: `requestId`, `status` (`pending_review`), `bookACall` (a link to book a call) and, when the candidate has an intro video, `introVideoUrl` (expires after 7 days). The Hire Overseas team verifies the candidate and replies to the contact email, usually within one business day.

### `get_request_status`

Input: `requestId`. Output: `status`, one of `pending_review`, `approved`, `rejected`.

### Errors and limits

Errors come back as a tool result with `isError: true` and an `error` message. Anonymous callers are limited to 10 requests a minute and 100 a day per IP address; over the limit, tools return an error with `retryAfterSeconds`. Identical searches within 10 minutes return the cached result. Candidate references are only valid on this server.

## Privacy

Profiles show a first name, country, timezone, skills, experience and work history by job title and industry. They never include a surname, contact details, links or employer names. Resumes are available with the same details removed. Where a candidate has recorded an intro video, the profile links to it; the video shows the candidate. Hire Overseas screens and verifies each candidate, and confirms availability and pricing, before making an introduction.

Full notice: [api.hireoverseas.com/mcp/privacy](https://api.hireoverseas.com/mcp/privacy)

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

### Grok

At [grok.com/connectors](https://grok.com/connectors), choose New Connector → Custom and enter `https://api.hireoverseas.com/mcp`.

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
