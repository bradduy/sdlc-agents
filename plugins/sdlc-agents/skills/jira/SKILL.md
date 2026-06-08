---
name: jira
description: >
  Work with Jira Cloud from Codex. Use this skill when the user mentions Jira,
  issue keys such as ONAP-1209 or PROJ-123, Jira URLs, JQL, assigned work,
  comments, transitions, boards, sprints, backlog grooming, or creating and
  updating Jira issues.
---

# Jira

Use Atlassian MCP first. This plugin starts Atlassian's official remote MCP server
through `mcp-remote`:

```json
{
  "command": "npx",
  "args": ["-y", "mcp-remote@latest", "https://mcp.atlassian.com/v1/mcp/authv2"]
}
```

Prefer MCP tools when available. If MCP tools are not present in the current
session, use the REST fallback in `references/rest-fallback.md`.

## Defaults

- "latest Jira task assigned to me" means:
  `assignee = currentUser() AND statusCategory != Done ORDER BY updated DESC`
- Return the first issue unless the user asks for a list.
- Include issue key, summary, type, status, priority, parent, assignee, updated
  timestamp, and URL when available.
- Use the current Jira site from MCP auth or from `$ATLASSIAN_INSTANCE`.

## Guardrails

- Never print API tokens or OAuth credentials.
- Do not invent project keys, issue types, custom field IDs, board IDs, sprint
  IDs, account IDs, or workflow transition names. Query Jira first.
- Confirm before destructive or broad changes, including deletes, bulk updates,
  sprint moves, and ambiguous transitions.
- Before creating issues, query project issue types and required fields.
- Use Atlassian Document Format for REST descriptions and comments.
- Keep issue tables compact and actionable.

## Workflows

Read `references/workflows.md` for the standard workflows:

- Latest assigned task.
- My open issues.
- JQL search.
- Read issue context.
- Create issue.
- Update issue.
- Add comment.
- Transition issue.
- Boards, sprints, and backlog.
- Bulk operations.

Read `references/auth.md` for authentication details and `references/rest-fallback.md`
for direct Jira REST calls.
