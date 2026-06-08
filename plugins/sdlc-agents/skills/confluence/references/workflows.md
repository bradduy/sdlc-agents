# Confluence Workflows

## Search Pages

Use this when the user asks for docs, runbooks, specs, notes, or pages by title.
Return title, space, page ID, URL, status, and last updated date when available.

If the space is unknown, search broadly first, then narrow by space or parent page.

## Read And Summarize Page

Fetch the page by URL, page ID, or title plus space. Summarize:

- Purpose and current state.
- Key sections.
- Open questions or stale content.
- Related Jira issue keys or decision references.

## Create Page

1. Ask for space, title, parent page if needed, and target content.
2. Confirm the planned title, parent, and content preview.
3. Create the page.
4. Return the page URL and page ID.

## Update Section

1. Fetch the current page and version.
2. Locate the target heading or section.
3. Show a concise before/after diff.
4. Ask for confirmation.
5. Update only the selected section.

## Append Notes

Use this for meeting notes, deployment notes, QA results, sprint updates, and
retrospectives. Append under an existing heading when possible; otherwise create a
dated heading.

## Sync Markdown To Confluence

1. Inspect the local Markdown file.
2. Ask for target space, title, and parent page if not known.
3. Confirm whether this should create a new page or update an existing page.
4. Convert Markdown to a supported Confluence body representation.
5. Preview the content or diff.
6. Publish after confirmation.

## Pull Page Into Markdown

Fetch the Confluence page and convert the useful content to Markdown. Preserve page
title, source URL, page ID, and last updated metadata at the top of the file.

## Link Confluence Pages To Jira

When Jira context is available, attach the Confluence page URL to the Jira issue as
a remote link or add a comment with the document URL. Confirm before writing to Jira.

## Review Stale Docs

For stale-document reviews, check last updated date, owner if available, broken or
outdated Jira references, and sections that conflict with current Jira status.
