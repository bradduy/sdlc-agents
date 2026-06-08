---
name: confluence
description: >
  Work with Confluence Cloud from Codex. Use this skill when the user mentions
  Confluence pages, spaces, page IDs, page URLs, runbooks, PRDs, specs,
  architecture docs, release notes, sprint notes, retrospectives, Markdown sync,
  or requests to search, summarize, create, update, append, or publish docs.
---

# Confluence

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

- Treat "docs", "page", "runbook", "PRD", "spec", "architecture", "release
  notes", "sprint notes", and "retro" as possible Confluence work.
- Read and summarize pages freely when credentials permit.
- Confirm before creating, updating, appending, deleting, moving, or overwriting
  Confluence content.
- Show a concise preview or diff before any page update.
- Preserve page structure and existing headings unless the user asks for a rewrite.
- Prefer updating a specific section over replacing a whole page.

## Guardrails

- Never print API tokens or OAuth credentials.
- Do not invent space keys, page IDs, parent IDs, labels, or page URLs. Query
  Confluence first.
- Before updating a page, fetch the current page version and content.
- For REST updates, increment the page version and include a clear version message.
- Do not publish sensitive local files or secrets to Confluence.
- When syncing Markdown, confirm the target space, parent page, title, and whether
  to create or update.

## Workflows

Read `references/workflows.md` for the standard workflows:

- Search pages.
- Read and summarize a page.
- Create a page.
- Update a section.
- Append notes.
- Sync Markdown to Confluence.
- Pull a page into Markdown.
- Link Confluence pages to Jira issues.
- Review stale docs.

Read `references/auth.md` for authentication details and `references/rest-fallback.md`
for direct Confluence REST calls.
