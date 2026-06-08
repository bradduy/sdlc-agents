# SDLC Agents Codex Plugin

This plugin packages Jira and Confluence workflows for Codex.

## Included Surfaces

- `mcpServers`: starts Atlassian's official remote MCP server through `mcp-remote`.
- `skills/jira`: guides Codex when reading, creating, updating, and triaging Jira issues.
- `skills/confluence`: guides Codex when searching, reading, creating, and updating Confluence pages.
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

Create an Atlassian API token from [Atlassian API tokens](https://id.atlassian.com/manage-profile/security/api-tokens).

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

The fallback uses Jira Cloud's current JQL search endpoint and Confluence Cloud REST API v2 page endpoints:

```text
GET /rest/api/3/search/jql
GET /wiki/api/v2/pages
POST /wiki/api/v2/pages
PUT /wiki/api/v2/pages/{id}
```
