# content — Content creation, formatting, and publishing

## Purpose
Covers all tasks where content is generated for external consumption: writing, drafting,
formatting, and publishing to platforms.

Includes: educational content (CloudText), messaging/channel publishing (Telegram),
drafting posts, formatting documents.

Does NOT cover: raw code generation (→ coding/), research/lookups for internal use (→ knowledge/),
financial analysis (→ finance/).

## Routing
- `./cloudtext.md` — educational task publishing on lk.cloudtext.ru
- `./telegram.md` — publishing messages and content to Telegram groups/channels

## Decision boundaries
- Task involves creating or publishing to `lk.cloudtext.ru` → cloudtext.md
  because CloudText has a specific draft-approval-publish workflow and task format requirements
  distinct from general messaging
- Task involves sending messages or content to Telegram (groups, channels, DMs) → telegram.md
  because Telegram publishing uses a dedicated script with specific formatting constraints
- Task is generic content drafting without a specific publishing target → handled at this level

## Rules & Directives

### General content principles
- Match content complexity to audience; for Dasha (163037943) use plain language, no tech terms
- Mixed formats preferred over single-type content blocks
- Always verify content quality before publishing to any platform
- For large theory blocks: produce multiple variants (up to 3) and let user choose

### Platform formatting
- Telegram: no markdown tables; use bullet lists; suppress multi-link embeds with `<>`
- CloudText: structured task formats with distractors, shuffled keys, explicit correct answers

## Variables
(none)

## Accumulated rules
(empty)
