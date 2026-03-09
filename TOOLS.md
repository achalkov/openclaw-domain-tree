# TOOLS — Agent tooling and integrations

## Purpose
Documents concrete tools available to the agent: hardware pipelines, SSH access, external services.
If AGENTS/ describes operational rules, TOOLS/ describes the specific instruments to execute them.
This is L1. Tool detail lives in TOOLS/ sub-tree (L2, max L4).

## Tool registry

| Tool | Path | Description |
|------|------|-------------|
| stt | TOOLS/stt/stt.md | Speech-to-text pipeline for voice messages |
| ssh | TOOLS/ssh/ssh.md | SSH access config and host inventory |
| printing | TOOLS/printing/printing.md | Network printer (EPSON L3260) |

## Navigation
- Need to transcribe a voice message → TOOLS/stt/stt.md
- Need SSH to a remote host → TOOLS/ssh/ssh.md (for how-to); AGENTS/inventory/ (for what runs there)
- Need to print → TOOLS/printing/printing.md

## Decision boundaries
- TOOLS/ = HOW to use a specific instrument (pipeline steps, credentials, commands).
- AGENTS/inventory/ = WHAT runs on each host and its configuration.
- These complement each other: ssh.md tells you how to connect; homelab.md tells you what you'll find there.

## Accumulated rules
(empty)
