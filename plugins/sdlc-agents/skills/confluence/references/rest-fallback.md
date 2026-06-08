# Confluence REST Fallback

Use REST only when MCP tools are unavailable or insufficient.

## Environment

```bash
ATLASSIAN_EMAIL="${ATLASSIAN_EMAIL}"
ATLASSIAN_API_TOKEN="${ATLASSIAN_API_TOKEN}"
ATLASSIAN_INSTANCE="${ATLASSIAN_INSTANCE}"
```

If values are missing, check shell profile exports in `~/.zshrc`, `~/.bashrc`, and
`~/.bash_profile`.

## Base URL

```text
https://${ATLASSIAN_INSTANCE}/wiki/api/v2
```

Use basic auth:

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" ...
```

## List Or Search Pages

Use page listing filters when possible:

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  --get \
  --data-urlencode "title=<PAGE_TITLE>" \
  --data-urlencode "space-id=<SPACE_ID>" \
  --data-urlencode "body-format=storage" \
  "https://$ATLASSIAN_INSTANCE/wiki/api/v2/pages"
```

For richer text search, use the available Confluence search endpoint exposed by MCP
when present, or fall back to Atlassian's CQL search APIs if the site supports them.

## Get Page

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  --get \
  --data-urlencode "body-format=storage" \
  "https://$ATLASSIAN_INSTANCE/wiki/api/v2/pages/$PAGE_ID"
```

## Create Page

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  -X POST \
  -H "Content-Type: application/json" \
  -d @page-create.json \
  "https://$ATLASSIAN_INSTANCE/wiki/api/v2/pages"
```

Payload shape:

```json
{
  "spaceId": "<SPACE_ID>",
  "status": "current",
  "title": "<Page title>",
  "parentId": "<PARENT_PAGE_ID>",
  "body": {
    "representation": "storage",
    "value": "<p>Page content</p>"
  }
}
```

Omit `parentId` when creating at the space root.

## Update Page

Fetch the current page first and increment `version.number`.

```bash
curl -sS -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  -X PUT \
  -H "Content-Type: application/json" \
  -d @page-update.json \
  "https://$ATLASSIAN_INSTANCE/wiki/api/v2/pages/$PAGE_ID"
```

Payload shape:

```json
{
  "id": "<PAGE_ID>",
  "status": "current",
  "title": "<Page title>",
  "body": {
    "representation": "storage",
    "value": "<p>Updated page content</p>"
  },
  "version": {
    "number": 2,
    "message": "Update from SDLC Agents"
  }
}
```

## Payload Rules

- Build JSON with a structured encoder.
- Treat Confluence storage HTML as structured content; do not concatenate unescaped
  user text into JSON or HTML.
- Do not log `ATLASSIAN_API_TOKEN`.
- Confirm before publishing create or update requests.
