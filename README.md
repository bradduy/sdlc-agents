# SDLC Agents

SDLC Agents is a Codex plugin that connects Codex to Jira Cloud and Confluence Cloud through Atlassian's official remote MCP server.

The packaged workflows cover Jira issue management and Confluence documentation: find assigned work, search with JQL, read issue context, create issues, add comments, transition work, inspect boards or sprints, search pages, create pages, update documentation, and sync Markdown content.

## Installation

Install the plugin with the Codex marketplace tooling:

```bash
npx codex-marketplace add bradduy/sdlc-agents --plugins
```

After installation, start or reload Codex so it can discover the new plugin.

When SDLC Agents starts the Atlassian MCP connection for the first time, an Atlassian website authorization page will open. Sign in, review the requested access, and accept the authorization for the Jira site you want Codex to use.

After accepting Atlassian authorization, reload Codex again so the plugin and MCP tools are loaded successfully in the active session.

The repo also includes a Codex marketplace manifest at:

```text
.agents/plugins/marketplace.json
```

## Authentication

The plugin starts Atlassian MCP through `mcp-remote`:

```bash
npx -y mcp-remote@latest https://mcp.atlassian.com/v1/mcp/authv2
```

On first use, Atlassian opens an OAuth flow. Sign in with the Atlassian account that has access to your Jira and Confluence sites.

For environments where MCP is unavailable, the Jira and Confluence skills document REST fallbacks. Export these variables before starting Codex:

Create an Atlassian API token from [Atlassian API tokens](https://id.atlassian.com/manage-profile/security/api-tokens).

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

## Example Prompts

### Jira

```text
Show my latest Jira task with status, priority, parent, and updated time.
List my open Jira issues in the current sprint, grouped by status.
```

### Confluence

```text
Search Confluence for release readiness docs in the ONAP space.
Summarize this Confluence page and identify outdated sections.
```

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/sdlc-agents/.codex-plugin/plugin.json
plugins/sdlc-agents/.mcp.json
plugins/sdlc-agents/skills/jira/SKILL.md
plugins/sdlc-agents/skills/confluence/SKILL.md
plugins/sdlc-agents/skills/jira/references/
plugins/sdlc-agents/skills/confluence/references/
```

## 🙋🏻‍♂️ Contributing

- Duy Tran Thanh - Applied AI Leader
