---
name: wiki-ingest
description: Process a new source document into the wiki — summarize, cross-reference, and update all relevant pages
---

# Wiki Ingest

You are ingesting a new source document into the wiki. Follow these steps.

## Step 1: Identify the Source

The user specifies a file in `raw/` (or has just added one). Read the source document completely.

If no specific file is mentioned, list the contents of `raw/` and ask the user which source to ingest. You can also check `log.md` to see which sources have already been ingested to avoid duplicates.

Also read `tracker.md` for session context — it may indicate which source the user intended to ingest or what work item this relates to.

## Step 2: Discuss Key Takeaways

Before writing anything, discuss with the user:
- Summarize the **main points** of the source (5-10 key claims or ideas)
- Highlight what's **new or surprising** relative to existing wiki content
- Note any **contradictions** with what the wiki currently says
- Ask the user: what should we emphasize? Anything to skip or explore further?

Wait for user input before proceeding.

## Step 3: Create Source Summary Page

Create a new page in the appropriate wiki subdirectory:
- Filename: `wiki/<subdir>/<kebab-case-source-name>.md`
- If no existing subdirectory fits, propose creating a new one

Frontmatter:
```yaml
---
title: "<Source Title>"
type: source-summary
created: <TODAY>
updated: <TODAY>
sources:
  - "<raw/filename>"
tags: [<relevant tags>]
---
```

Content structure:
- **Overview**: 2-3 sentence summary
- **Key Claims**: bulleted list of the main points, each citing specific sections/pages of the source
- **Relevance**: how this connects to existing wiki content
- **Open Questions**: things raised by the source that aren't yet answered

## Step 4: Update Entity and Concept Pages

For each significant entity (person, organization, tool, project) or concept (idea, pattern, framework) mentioned in the source:

1. **Search** the wiki for an existing page (check `index.md`, use grep for `[[entity-name]]`)
2. **If a page exists**: update it with new information from this source. Add a citation. If the new info contradicts existing content, **flag the contradiction explicitly** — do not silently overwrite.
3. **If no page exists** and the entity/concept is significant enough (mentioned multiple times, central to the source, or likely to recur): create a new page with proper frontmatter and initial content.

## Step 5: Update Cross-References

- Add `[[wikilinks]]` from the new source summary to relevant existing pages
- Add `[[wikilinks]]` from existing pages back to the new source summary where relevant
- For wikis linked to code repos: if the source discusses code, add file-path references (e.g., `src/auth/handler.ts:45`)

## Step 6: Evaluate Wiki Structure

Before updating the index, step back and consider the wiki's overall organization:

- **Does the current directory structure still make sense?** As content grows, categories that once made sense may need splitting, merging, or renaming. If a subdirectory is becoming a dumping ground or a new natural grouping has emerged, propose reorganizing.
- **Are pages grouped logically?** Related pages should be near each other in the hierarchy. If you're creating a page that doesn't fit cleanly into any existing group, that's a signal the structure may need evolving.
- **Think about how this looks in Obsidian's graph view** — pages should form meaningful clusters. Isolated nodes or one giant blob both indicate structural problems.

If you think the structure needs changes, propose them to the user before proceeding.

## Step 7: Update index.md

Add entries for all newly created pages. Maintain the existing organizational structure. Each entry: `- [[page-name]] — Brief one-line description`

## Step 8: Append to log.md

```markdown
## [<TODAY>] created | Ingested: <Source Title>

Source: `raw/<filename>`

Pages created:
- [[new-page-1]]
- [[new-page-2]]

Pages updated:
- [[existing-page-1]] — added info about X
- [[existing-page-2]] — noted contradiction with source on Y
```

## Step 9: Report

Show the user a summary:
- Files created (with links)
- Files updated (what changed)
- Contradictions found (if any)
- Suggested follow-ups: related sources to seek, questions to investigate

## Step 10: Suggest Tracker Updates

Check `tracker.md` for work items related to the ingested source:
- If any items reference this source or topic, suggest updating their status
- If the ingestion reveals new work (follow-up research, contradictions to resolve, pages to create), suggest adding items to the tracker
- Append a log entry to `log.md` noting what was ingested
