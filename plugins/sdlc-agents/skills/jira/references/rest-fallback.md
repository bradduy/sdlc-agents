# Jira REST Fallback

Use REST only when MCP tools are unavailable or insufficient.

## Environment

```bash
ATLASSIAN_EMAIL="${ATLASSIAN_EMAIL}"
ATLASSIAN_API_TOKEN="${ATLASSIAN_API_TOKEN}"
ATLASSIAN_INSTANCE="${ATLASSIAN_INSTANCE}"
```

If values are missing, check shell profile exports in `~/.zshrc`, `~/.bashrc`, and
`~/.bash_profile`.

## Endpoints

```text
https://${ATLASSIAN_INSTANCE}/rest/api/3
https://${ATLASSIAN_INSTANCE}/rest/agile/1.0
```

Jira Cloud search must use the current endpoint:

```text
GET /rest/api/3/search/jql
```

The older `/rest/api/3/search` endpoint may return a removed API error.

## Latest Assigned Task

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  --get \
  --data-urlencode 'jql=assignee = currentUser() AND statusCategory != Done ORDER BY updated DESC' \
  --data-urlencode 'maxResults=1' \
  --data-urlencode 'fields=summary,status,issuetype,priority,updated,created,assignee,project,parent' \
  "https://$ATLASSIAN_INSTANCE/rest/api/3/search/jql"
```

## Payload Rules

- Build JSON with a structured encoder.
- Use Atlassian Document Format for description and comment bodies.
- Do not interpolate unescaped user content into JSON strings.
- Do not log `ATLASSIAN_API_TOKEN`.
