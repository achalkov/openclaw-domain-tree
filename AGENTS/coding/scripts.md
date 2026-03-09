# scripts — Shell and Python utility scripts

## Purpose
Rules for writing, running, and maintaining shell and Python scripts.
Covers: one-off automation, cron scripts, utility tools, CLI helpers.
Does NOT cover: ACP agent sessions (→ ./acp.md), inline code snippets without a file.

## Rules & Directives

### General
- Always test scripts with a dry-run or limited-scope run before full execution
- Verify API/CLI success responses explicitly — do not assume success from lack of error output
- For scripts interacting with external APIs: check HTTP status codes and response body
- Scripts that modify data should be idempotent or have explicit rollback/backup logic

### Known scripts (workspace: `/home/clawd/.openclaw/workspace/scripts/`)

| Script | Purpose | Key flags |
|---|---|---|
| `tg_group_publisher.py` | Telegram group/channel publisher | `--chat-id` (required), verify API success response |
| `cloudtext_task_tool.py` | CloudText task publishing tool | See content/cloudtext domain |
| `yt_daily_digest.py` | YouTube daily digest generator | — |
| `yt_digest_send.py` | Send YT digest via Telegram | — |
| `yt_takeout_profile.py` | Parse YouTube Takeout for user profile | — |
| `ocr_openrouter.py` | OCR via OpenRouter API | — |
| `memory_sqlite_search.py` | Search memory SQLite index | — |
| `check_openai_codex_connectivity.sh` | Check OpenAI Codex connectivity | — |
| `probe_openai_codex_models.sh` | Probe available Codex models | — |
| `multi_host_openai_check.sh` | Check OpenAI across multiple hosts | — |
| `run_probe_openai_codex_all_hosts.sh` | Run Codex probe on all hosts | — |
| `skills_reconcile.sh` | Reconcile installed skills | — |
| `scan_skills.sh` | Scan workspace for skills | — |
| `openclaw_backup_run.sh` | Run OpenClaw workspace backup | — |

### Telegram publishing (`tg_group_publisher.py`)
- ALWAYS provide `--chat-id` explicitly — never rely on defaults
- After each publish call, verify the API response confirms success (check `ok: true` or equivalent)
- No markdown tables in Telegram output; use bullet lists instead
- Suppress link embeds with `<>` syntax for multiple links

### Adding new scripts
- Run `find /home/clawd/.openclaw/workspace/scripts -type f 2>/dev/null` to get current list before assuming the inventory above is complete
- Document new scripts in this file when they are created

## Variables
(none — API tokens are loaded from environment or `.env` files)

## Accumulated rules
(empty)
