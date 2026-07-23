# Rule: Context Before Change

## Why

This project has explicit agent instructions in AGENTS.md and separate backend/frontend concerns.
Changes made without loading context can break workflow assumptions.

## Required behavior

1. Read AGENTS.md before any analysis or edit.
2. Read existing rules in .agents/rules before proposing new ones.
3. Check memory-bank content for product context and current status.
4. Validate the target layer before editing:
   - backend changes: inspect backend/app and backend/tests
   - frontend changes: inspect frontend/src and frontend tests

## Good practice observed

- Repository already separates guidance (AGENTS.md), code, and tests by layer.

## Anti-pattern to avoid

- Editing endpoints or dashboard behavior from assumptions without checking the current files.

## Done checklist

- AGENTS.md reviewed.
- Relevant .agents/rules files reviewed.
- Relevant memory-bank files reviewed.
- Intended layer files inspected before edits.