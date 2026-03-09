# MEMORY.md — Long-Term Memory

> Level 1 core file. Load in MAIN SESSION only (not in shared/group contexts).

## Policy
- Long-term memory is in SQLite: `memory/memory.sqlite3`.
- Daily notes: `memory/YYYY-MM-DD.md`.
- This file stores only: invariant behavioral rules + pointers.
- Details/history/journal → daily `.md` files and SQLite.

## Memory storage rules
- On "remember this" → write to `memory/YYYY-MM-DD.md` or relevant domain file.
- On lesson learned → update relevant domain `.md` and/or this file.
- Periodic hygiene: consolidate daily files into MEMORY.md every few days.

## Behavioral constants
_(Agent: add durable rules here as they are confirmed across sessions.)_
