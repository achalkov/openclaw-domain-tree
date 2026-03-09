# agent-ops/skills — Installed skills catalog and usage protocol

## Purpose
Catalog of all installed skills, their purposes, locations, and the protocol for selecting and using them.

---

## Usage protocol
1. Before using any skill: read its `SKILL.md` file first (located at the path shown below).
2. Match task to the most specific skill; when multiple apply, choose the most specific one.
3. Never call a skill's internals directly without reading SKILL.md — APIs and CLIs may vary.
4. After using a skill and discovering important operational details: add a note to this file or the skill's SKILL.md.

## Skill discovery
```bash
npx skills find <query>
```
Run this when the user asks about a capability that might exist as an installable skill ("есть скилл для X?"). Summarize top matches (what they do + limits), then recommend the best path.

## Installed skills

### Workspace skills (`~/.openclaw/workspace/skills/`)

| Skill | Description | SKILL.md |
|---|---|---|
| `github-api` | GitHub API integration with managed OAuth. Repos, issues, PRs, commits, branches, users. | `workspace/skills/github-api/SKILL.md` |
| `gog` | Google Workspace CLI — Gmail, Calendar, Drive, Contacts, Sheets, Docs. | `workspace/skills/gog/SKILL.md` |
| `summarize` | Summarize URLs or files (web, PDFs, images, audio, YouTube) via the summarize CLI. | `workspace/skills/summarize/SKILL.md` |
| `nano-pdf` | Edit PDFs with natural-language instructions via the nano-pdf CLI. | `workspace/skills/nano-pdf/SKILL.md` |
| `weather` | Current weather and forecasts (no API key required). | `workspace/skills/weather/SKILL.md` |
| `cloudtext-publisher` | Publish and update assignments in CloudText (lk.cloudtext.ru) — API-first workflow. Handles mixed task types (short/long answer, single/multiple choice, voice, scale). Returns edit/share links. | `workspace/skills/cloudtext-publisher/SKILL.md` |
| `find-skills` | Discover and install agent skills when users ask about extending capabilities. | `workspace/skills/find-skills/SKILL.md` |
| `self-improving-agent` | Capture learnings, errors, and corrections for continuous improvement. Use on unexpected failures, user corrections, outdated knowledge, or better approaches discovered. | `workspace/skills/self-improving-agent/SKILL.md` |
| `session-logs` | (Session log access utility.) | `workspace/skills/session-logs/SKILL.md` |

### Built-in skills (`~/.npm-global/lib/node_modules/openclaw/skills/`)

| Skill | Description | SKILL.md |
|---|---|---|
| `healthcheck` | Host security hardening and risk-tolerance config. Security audits, firewall/SSH/update hardening, risk posture review, OpenClaw cron scheduling for periodic checks. | built-in: `skills/healthcheck/SKILL.md` |
| `skill-creator` | Create, edit, improve, or audit AgentSkills. Use for new skills or improving/reviewing existing SKILL.md files. | built-in: `skills/skill-creator/SKILL.md` |
| `tmux` | Remote-control tmux sessions — send keystrokes, scrape pane output. | built-in: `skills/tmux/SKILL.md` |
| `video-frames` | Extract frames or short clips from videos using ffmpeg. | built-in: `skills/video-frames/SKILL.md` |

### Agent skills (`~/.agents/skills/`)

| Skill | Description | SKILL.md |
|---|---|---|
| `context7` | Retrieve up-to-date documentation for software libraries/frameworks via Context7 API. Use when looking up library docs, code examples, verifying correct API usage, or getting current info on APIs that may have changed. | `~/.agents/skills/context7/SKILL.md` |
| `instagram` | Instagram Graph API integration via curl. Fetch and publish Instagram media. | `~/.agents/skills/instagram/SKILL.md` |

### YouTube skill
| Skill | Description | SKILL.md |
|---|---|---|
| `youtube` (openclaw-youtube) | Extract transcripts (free, zero API quota), download 4K video & FLAC audio via yt-dlp, read comments, search with filters, batch video details. No API key needed for transcripts. | `workspace/.agents/skills/openclaw-youtube/SKILL.md` |

## Skill selection hints
- GitHub operations → `github-api`
- Google services (Gmail, Calendar, Drive, Sheets, Docs) → `gog`
- Summarize URL/file/YouTube → `summarize` or `youtube` (youtube has free transcript extraction)
- PDF editing → `nano-pdf`
- Weather → `weather`
- CloudText publishing (Dasha's primary tool) → `cloudtext-publisher`
- Library/framework documentation → `context7` (always prefer over training-time knowledge)
- Security audit / SSH hardening → `healthcheck`
- tmux / terminal UI interaction → `tmux`
- Video processing → `video-frames`
- New skill needed? → `find-skills` or `skill-creator`
- Log a lesson/correction → `self-improving-agent`

## Variables
- `agent.agent-ops.skills_workspace_path` — `~/.openclaw/workspace/skills/`
- `agent.agent-ops.skills_builtin_path` — `~/.npm-global/lib/node_modules/openclaw/skills/`
- `agent.agent-ops.skills_agents_path` — `~/.agents/skills/`

## Accumulated rules
- Always read SKILL.md before invoking a skill — do not rely on memory of previous usage.
- context7 must be used for any library/framework documentation lookup; do not trust training-time knowledge for APIs.
- cloudtext-publisher is Dasha's primary publishing tool; always use API-first workflow (not browser UI clicking).
