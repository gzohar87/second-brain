---
name: wiki-distill
description: Review recent Claude Code conversations and extract wiki-worthy content into raw/ for ingestion
---

# Wiki Distill

You are distilling recent Claude Code conversations into raw source material for the wiki. This is a two-stage process: extract conversation content into `raw/sessions/`, then ingest the new files into wiki pages.

## Step 1: Locate Vault

Determine the target vault:
- If a vault path is provided in the prompt, use it directly
- Otherwise, read the current project's CLAUDE.md for the `Wiki location:` marker
- If cwd itself is a vault (has `index.md` + `wiki/`), use it
- If none found, ask the user

Read `config.yml` if present (warn but proceed if missing).

## Step 2: Determine Time Window

Check `log.md` for the most recent distill entry (look for `| Conversation distill`). Extract its date.

- If a previous distill exists: only process conversations since that date
- If no previous distill: process conversations from the last 24 hours

## Step 3: Find Recent Conversations

Read conversation transcripts from `~/.claude/projects/`. Each project directory corresponds to a working directory path (with slashes replaced by dashes). Each `.jsonl` file inside is a session transcript.

1. Identify the project directories that correspond to this vault and its linked repos
2. Find `.jsonl` files modified within the time window from Step 2
3. Read each transcript — lines are JSON objects with `type` (user/assistant/tool_use/tool_result), `message`, `timestamp`, `cwd`, `sessionId`

If no conversations are found in the time window, log "no new conversations" and exit.

## Step 4: Extract Wiki-Worthy Content

For each conversation, identify content worth preserving:

**Include:**
- Decisions made and their rationale
- New facts, data points, or claims
- Corrections to previously held beliefs
- Architecture or design discussions
- Problem diagnoses and solutions
- Insights, patterns, or synthesis that emerged

**Skip:**
- Routine tool calls (file reads, directory listings)
- Mechanical code edits without design significance
- Debugging sessions that didn't yield insights
- Small talk or meta-discussion about the tool itself

For each piece of content, note which conversation it came from and enough surrounding context to be understandable standalone.

## Step 5: Write to raw/sessions/

Create structured markdown files in `raw/sessions/`:

**Filename:** `raw/sessions/YYYY-MM-DD-<topic-slug>.md`

If multiple conversations cover different topics, create separate files. If they overlap, merge into one file organized by topic.

**Format:**
```markdown
---
source: conversation
session_ids:
  - "<session-id-1>"
  - "<session-id-2>"
date: <TODAY>
repos:
  - "<repo-path>"
---

# <Topic Title>

<Organized content — by topic, not chronologically.
Preserve specific details, reasoning, and context.
Use direct quotes from the conversation where they capture something precisely.>

## <Subtopic>

<More content...>
```

Ensure `raw/sessions/` directory exists (create if needed).

## Step 6: Ingest New Raw Files

For each new file created in `raw/sessions/`, run the ingest workflow:

1. Read the raw file
2. Create or update wiki pages following the same principles as `/wiki-ingest`:
   - Create organized source pages in `wiki/`
   - Update entity and concept pages with new information
   - Add cross-references
   - Flag contradictions explicitly
3. Update `index.md` with new pages

Since this is an autonomous process, skip the interactive discussion (Step 2 of `/wiki-ingest`) — proceed directly to page creation.

## Step 7: Update Log

Append to `log.md`:

```markdown
## [<TODAY>] created | Conversation distill

Sessions processed: <N>
Time window: <start> to <end>

Raw files created:
- `raw/sessions/<filename-1>.md`
- `raw/sessions/<filename-2>.md`

Pages created:
- [[new-page]] — <why>

Pages updated:
- [[existing-page]] — added <what>

Skipped: <N> conversations (no wiki-worthy content)
```

## Step 8: Commit

Stage and commit all changes:
```
git add raw/sessions/ wiki/ index.md log.md tracker.md
git commit -m "chore: wiki-distill <DATE>"
```

## Step 9: Report

Show a brief summary:
- Conversations processed vs skipped
- Raw files created
- Wiki pages created/updated
- Contradictions found (if any)
