# CLAUDE.md — scrum-ticket-lifecycle

This file configures Claude Code behavior for this repository.

## Repository Purpose

This repo contains the `scrum-ticket-lifecycle` skill — a Scrum process checker for Azure DevOps multi-Squad organizations. It is **not** a decision-making tool; it checks whether process conditions are met after TPO makes decisions.

## Skill Location

The primary skill file is at:
```
scrum-ticket-lifecycle/SKILL.md
```

Reference files (load on demand):
```
scrum-ticket-lifecycle/references/ac-guide.md         # AC writing guide
scrum-ticket-lifecycle/references/block-handling.md   # Block decision tree
scrum-ticket-lifecycle/references/card-states.md      # Card state definitions
scrum-ticket-lifecycle/references/ado-fields.md       # ADO field mapping
```

## How Claude Code Should Use This Skill

When a user asks process-related questions in this repo context, Claude Code should:

1. Read `scrum-ticket-lifecycle/SKILL.md` first
2. Load the relevant `references/` file only when the user's question matches the trigger described in SKILL.md's Reference Files table
3. Never load all reference files at once — use progressive disclosure

## Contribution Workflow

When making changes to skill files:

1. Always work on a **feature branch**, never commit directly to `main`
2. Branch naming: `feat/` for new rules, `fix/` for corrections, `docs/` for documentation
3. One logical change per PR
4. After pushing a branch, open a PR with:
   - Title: concise description of the change
   - Body: use the PR template at `.github/pull_request_template.md`
5. Wait for maintainer approval before merging — **do not auto-merge**

## File Editing Rules

- `SKILL.md` should stay under 300 lines — if approaching limit, move content to a new `references/` file
- Each `references/` file should cover one domain only
- Do not duplicate content between SKILL.md and references files
- When adding a new reference file, always add its entry to the Reference Files table in SKILL.md

## Language

All skill content is in **Traditional Chinese (zh-TW)**. Code, file names, and branch names use English.
