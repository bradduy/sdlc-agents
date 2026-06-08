# Jira Authentication

## Preferred: Atlassian MCP OAuth

The plugin configures Atlassian MCP through:

```bash
npx -y mcp-remote@latest https://mcp.atlassian.com/v1/mcp/authv2
```

On first use, `mcp-remote` opens a browser OAuth flow. Sign in with the Atlassian
account that has Jira access.

Some Atlassian organizations restrict external tools or IP ranges. If auth succeeds
but Jira data is unavailable, confirm the selected Atlassian site and organization
policy.

## REST Fallback: API Token

For API-token fallback, export:

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

Create API tokens from [Atlassian API tokens](https://id.atlassian.com/manage-profile/security/api-tokens).

Restart Codex after exporting variables so subprocesses inherit them.
