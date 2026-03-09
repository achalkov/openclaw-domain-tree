# telegram — Publishing to Telegram groups and channels

## Purpose
Rules for publishing messages and content to Telegram groups, channels, and users
via the workspace publisher script.

Covers: group/channel posts, formatted messages, media publishing via script.
Does NOT cover: direct DM replies in OpenClaw chat sessions (those use the message tool),
CloudText publishing (→ ./cloudtext.md).

## Rules & Directives

### Publisher script
- Script: `/home/clawd/.openclaw/workspace/scripts/tg_group_publisher.py`
- ALWAYS specify `--chat-id` explicitly — never rely on defaults or omit this flag
- After each publish call, verify the API response confirms success (`ok: true` or equivalent)
- Do not assume success from lack of error; explicitly check the response body

### Formatting rules
- No markdown tables — Telegram does not render them; use bullet lists instead
- For multiple links: wrap in `<>` to suppress embeds: `<https://example.com>`
- Bold/italic markdown is supported in most Telegram message modes
- No headers (`#`, `##`) in message content — use **bold** or CAPS for emphasis

### Known user IDs
- Artem: `1285239`
- Dasha: `163037943`

### Autonomy (Dasha context)
- Publishing to Telegram on Dasha's behalf is a silent background action — she sees only the result
- Never ask Dasha to run the script herself or provide CLI commands to her

## Variables
- `$TELEGRAM_BOT_TOKEN` — Telegram bot API token (from environment)

## Accumulated rules
(empty)
