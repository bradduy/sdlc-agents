# Jira Workflows

## Latest Assigned Task

Use this JQL:

```text
assignee = currentUser() AND statusCategory != Done ORDER BY updated DESC
```

Return the first issue with key, summary, status, priority, parent, updated time,
and URL.

## My Open Issues

Use:

```text
assignee = currentUser() AND statusCategory != Done ORDER BY updated DESC
```

For sprint focus:

```text
assignee = currentUser() AND sprint in openSprints() ORDER BY priority DESC, updated DESC
```

## Search

Translate user intent into JQL and run the query. Keep results compact:

```text
project = ONAP AND issuetype = Bug AND statusCategory != Done ORDER BY priority DESC
key in (ONAP-1209, ONAP-265)
text ~ "AMLEAD" ORDER BY updated DESC
```

## Read Issue

Fetch by issue key or URL. Include:

- Summary, issue type, status, priority.
- Assignee, reporter, parent or epic.
- Labels, fix versions, sprint if present.
- Description summary.
- Comments and remote links only when relevant.

## Create Issue

1. Ask for project, issue type, summary, and acceptance criteria if missing.
2. Query issue types and required fields.
3. Build a minimal payload.
4. Show the planned issue and ask for confirmation.
5. Create it and return key plus URL.

## Update Issue

Fetch the current issue first. Summarize meaningful field changes before updating.
Use discovered custom field IDs rather than guessing.

## Add Comment

Keep comments concise. For longer status updates, use short headings and bullets.

## Transition Issue

Fetch available transitions. If one transition clearly matches the requested target,
apply it. If multiple match, ask for the exact transition.

## Boards, Sprints, And Backlog

List boards when the board is unknown. Confirm before moving issues into or out of a
sprint.

## Bulk Operations

Before bulk changes, show a table of planned actions and ask for confirmation with
the exact count.
