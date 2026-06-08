# SDLC Agents Codex Plugin

This plugin packages Jira workflows for Codex.

## Included Surfaces

- `mcpServers`: starts Atlassian's official remote MCP server through `mcp-remote`.
- `skills/jira`: guides Codex when reading, creating, updating, and triaging Jira issues.
- `references`: keeps auth, REST fallback, and workflow details close to the skill.

## MCP Server

```json
{
  "command": "npx",
  "args": [
    "-y",
    "mcp-remote@latest",
    "https://mcp.atlassian.com/v1/mcp/authv2"
  ]
}
```

## REST Fallback

Set these before launching Codex if you need API-token fallback:

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

The fallback uses Jira Cloud's current JQL search endpoint:

```text
GET /rest/api/3/search/jql
```
