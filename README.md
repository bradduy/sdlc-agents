# SDLC Agents

SDLC Agents is a Codex plugin that connects Codex to Jira Cloud through Atlassian's official remote MCP server.

The first packaged workflow is Jira issue management: find assigned work, search with JQL, read issue context, create issues, add comments, transition work, and inspect boards or sprints.

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

On first use, Atlassian opens an OAuth flow. Sign in with the Atlassian account that has access to your Jira site.

For environments where MCP is unavailable, the Jira skill documents a REST fallback. Export these variables before starting Codex:

Create an Atlassian API token from [Atlassian API tokens](https://id.atlassian.com/manage-profile/security/api-tokens).

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

## Example Prompts

```text
Show my latest Jira task with status, priority, parent, and updated time.
List my open Jira issues in the current sprint, grouped by status.
Find unresolved ONAP bugs assigned to me and sort them by priority.
Summarize ONAP-1209, including acceptance criteria, comments, and blockers.
Create a Jira task in ONAP for the release readiness checklist.
Move ONAP-1209 to In Progress after confirming the available transition.
Add a QA result comment to ONAP-1209 with the test outcome and evidence.
```

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/sdlc-agents/.codex-plugin/plugin.json
plugins/sdlc-agents/.mcp.json
plugins/sdlc-agents/skills/jira/SKILL.md
plugins/sdlc-agents/skills/jira/references/
```

## 🙋🏻‍♂️ Contributing

- Duy Tran Thanh - Applied AI Leader, Senior AI Engineer at OneMount Group
