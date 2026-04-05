---
name: wiki-automate
description: Set up scheduled automation (distill + lint) for a wiki vault using /schedule
---

# Wiki Automate

You are setting up scheduled automation for a wiki vault. This is a one-time setup that registers cron-based triggers via `/schedule`.

## Step 1: Locate Vault

Determine the target vault:
- If a vault path is provided in the prompt, use it directly
- Otherwise, read the current project's CLAUDE.md for the `Wiki location:` marker
- If cwd itself is a vault (has `index.md` + `wiki/`), use it
- If none found, ask the user

## Step 2: Read Config

Read the vault's `config.yml`. If it doesn't exist, inform the user they should run `sb update` to create one, or create it from defaults.

Show the user the current automation config and confirm what they want to enable.

## Step 3: Register Schedules

For each enabled automation, use the `/schedule` skill to create a trigger.

### Lint trigger

If `automation.lint.enabled` is true:

```
/schedule "<cron-expression>" "Run /wiki-lint on <VAULT_PATH>. This is an autonomous scheduled run. Check if the wiki has changed since the last lint. If no changes, skip. Otherwise apply mechanical fixes automatically and commit them. Add all findings to tracker.md. Do not apply semantic fixes."
```

Use the cron expression from `config.yml` (default: `*/30 * * * *`).

### Distill trigger

If `automation.distill.enabled` is true:

```
/schedule "<cron-expression>" "Run /wiki-distill on <VAULT_PATH>. This is an autonomous scheduled run. Review Claude Code conversations since the last distill, extract wiki-worthy content into raw/sessions/, then ingest the new raw files into wiki pages."
```

Use the cron expression from `config.yml` (default: `0 7 * * *`).

## Step 4: Report

Show the user:
- Which triggers were registered
- Their cron schedules (in human-readable form)
- How to check status: `/schedule list`
- How to remove: `/schedule delete <id>`
