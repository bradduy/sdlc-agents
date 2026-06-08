# SDLC Agents

SDLC Agents is a Codex plugin that connects Codex to Jira Cloud through Atlassian's official remote MCP server.

The first packaged workflow is Jira issue management: find assigned work, search with JQL, read issue context, create issues, add comments, transition work, and inspect boards or sprints.

## Install

Install the plugin from this repository with the Codex marketplace tooling:

```bash
npx codex-marketplace add bradduy/sdlc-agents --plugins
```

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

```bash
export ATLASSIAN_EMAIL="your.email@company.com"
export ATLASSIAN_API_TOKEN="your_api_token_here"
export ATLASSIAN_INSTANCE="yourcompany.atlassian.net"
```

## Example Prompts

```text
Use SDLC Agents to show my latest Jira task.
Show my open Jira issues in the current sprint.
Find open bugs in ONAP assigned to me.
Create a Jira task in ONAP for the deployment checklist.
Move ONAP-1209 to In Progress.
Add a comment to ONAP-1209 with the QA result.
```

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/sdlc-agents/.codex-plugin/plugin.json
plugins/sdlc-agents/.mcp.json
plugins/sdlc-agents/skills/jira/SKILL.md
plugins/sdlc-agents/skills/jira/references/
```
