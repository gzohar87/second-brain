---
name: wiki-lint
description: Fully agentic wiki health check — find contradictions, orphans, stale content, and suggest improvements
---

# Wiki Lint

You are performing a comprehensive health check on the wiki. This is a fully agentic process — read, reason, and report.

## Autonomous Mode

If the prompt indicates autonomous or scheduled operation:

### Skip check
Before doing any work, check if the wiki has changed since the last lint:
- Read `log.md` for the timestamp of the most recent lint entry (look for `| Lint pass`)
- Run `git log --since="<last-lint-time>" -- <wiki-path>/` to check for commits since then
- If no commits since last lint, append a brief "no changes, skipping" note to `log.md` and **exit early** — do not proceed to scanning

### If changes found
- Proceed with all steps below (scan, check, report)
- Apply all mechanical fixes (Step 2 findings) **without asking** — do not wait for user input
- Commit fixes: `git add -A && git commit -m "chore: wiki-lint auto-fix <DATE>"`
- Update `tracker.md` with all findings (Step 5)
- Do **not** apply semantic fixes — log them to `tracker.md` only for human review
- Append to `log.md` with the standard lint log format
- Skip Step 6 (Offer to Fix) entirely

## Step 1: Scan the Wiki

1. Read `index.md` to get the page catalog
2. List all `.md` files in `wiki/` recursively
3. Read each wiki page (if the wiki is very large — over ~50 pages — read a representative sample and flag that a full audit wasn't done)
4. Also read `log.md` for recent activity context
5. Read `tracker.md` for current work context and previous lint findings

## Step 2: Mechanical Checks

### Orphan pages
Wiki pages with **no inbound `[[wikilinks]]`** from any other page. Check every page in `wiki/` — is it linked to from at least one other page or from `index.md`?

### Broken links
`[[wikilinks]]` that point to pages that **don't exist** as files. Scan all pages for `[[...]]` patterns and verify each target exists.

### Index drift
- Pages in `wiki/` that are **not listed** in `index.md`
- Entries in `index.md` that point to pages that **no longer exist**

### Missing frontmatter
Pages without proper YAML frontmatter, or missing required fields (`title`, `type`, `created`, `updated`).

### Empty / stub pages
Pages with very little content — under ~5 lines of actual content (excluding frontmatter).

### Unresolved comments
Scan all pages for user-left review comments. These are inline notes left by the user (typically in Obsidian) requesting changes or raising questions. Look for:
- Callout blocks: `> [!comment] ...`
- HTML comment markers: `<!-- COMMENT: ... -->`

Surface each one with its location and content so it can be addressed.

### Stale file-path references
For wikis linked to code repos: code paths cited in wiki pages (e.g., `src/foo.ts:12`) where the **file no longer exists** in the repo. Scan for patterns like backtick-wrapped file paths and verify they exist.

## Step 3: Semantic Checks

These require reading and reasoning about content — the high-value part of this lint.

### Contradictions
Claims in one page that **conflict** with claims in another page, where the contradiction is not acknowledged. Look for:
- Different dates, numbers, or facts about the same entity
- Conflicting assessments or conclusions
- Superseded information that wasn't marked as such

### Stale content
Pages that reference topics covered by **newer sources** but haven't been updated. Cross-reference `log.md` timestamps with page `updated` dates.

### Missing pages
Concepts or entities **frequently mentioned** across multiple pages (via `[[wikilinks]]` or plain text) but lacking their own dedicated page.

### Missing cross-references
Pages covering **related topics** that should link to each other but don't. Look for topical overlap, shared tags, or shared source references.

### Synthesis gaps
Areas where **multiple sources** touch on a topic but no comparison or synthesis page exists to tie them together.

### Misplaced content
Each file in the vault has a defined role. Content should live in the right place — not drift into the wrong file. Check for:
- **Tasks in wiki pages** — wiki pages document knowledge, not work items. Task lists (`- [ ] ...`) belong in `tracker.md`, not in wiki pages.
- **Narrative in tracker** — `tracker.md` is a structured list of work items, not a journal. If it contains long prose, session narratives, or explanations that belong in `log.md` or a wiki page, flag it.
- **Log entries in wiki pages** — chronological "what happened" entries belong in `log.md`, not scattered across wiki pages. Wiki pages should describe the current state of knowledge, not a timeline.
- **Wiki content in log** — `log.md` records what changed and when. If it contains detailed explanations or knowledge that should be a wiki page, flag it.
- **Frontmatter `type` mismatches** — a page with `type: concept` that reads like a decision record, or `type: reference` that reads like a how-to guide. The type should match the actual content.

The principle: every piece of information has a correct home. Knowledge goes in wiki pages, tasks go in the tracker, chronological records go in the log, and the index is a catalog — not a page with content of its own.

### Wiki structure
Evaluate whether the overall directory structure and page grouping still make sense:
- Are subdirectories becoming too large or too small? Should any be split or merged?
- Are pages grouped logically — do related pages live near each other?
- Would the wiki look well-organized in Obsidian's graph view — meaningful clusters rather than isolated nodes or one tangled blob?
- Have new natural categories emerged that don't have their own subdirectory yet?

If the structure needs reorganization, include specific proposals in the report.

## Step 4: Produce Report

Structure the report by severity:

### Errors (should fix)
- Broken links
- Index drift (missing entries or stale entries)
- Missing frontmatter

### Warnings (should review)
- Unresolved comments (user review notes left inline)
- Misplaced content (tasks in wiki pages, prose in tracker, etc.)
- Contradictions
- Stale content
- Stale file-path references
- Orphan pages

### Suggestions (could improve)
- Missing pages to create
- Missing cross-references to add
- Synthesis gaps to fill
- New sources to seek
- New questions to investigate

For each finding: describe the issue, list the files involved, and suggest a specific fix.

## Step 5: Update Tracker

After producing the report, update the vault's `tracker.md` (the `## Lint Findings` section):

1. **Read `tracker.md`** to see current lint findings
2. **Check for legacy `wiki/tasks.md`** — if it exists, migrate any open items to `tracker.md` under `## Lint Findings` and suggest deleting the old file
3. **Remove resolved items** — if a previously logged finding no longer appears in this lint run, mark it `[x]`
4. **Add new findings** under `## Lint Findings`:
   - `- [ ] \`error\` <description> — <files involved>`
   - `- [ ] \`warn\` <description> — <files involved>`
   - `- [ ] \`suggest\` <description> — <files involved>`
5. **Don't duplicate** — if a finding is already tracked (same issue, same files), leave the existing item
6. **Update** the `updated` field in `tracker.md` frontmatter to today

## Step 6: Offer to Fix

After presenting the report:
- **Mechanical fixes** (broken index entries, missing frontmatter, orphan links): offer to fix these automatically
- **Semantic fixes** (contradictions, stale content, new pages): discuss with the user first — these require judgment

If fixes are applied, update `log.md`:
```
## [<TODAY>] updated | Lint pass

Findings: <N> errors, <N> warnings, <N> suggestions
Fixed: <list what was auto-fixed>
Deferred: <list what needs user input>
```
