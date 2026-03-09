# stt — Speech-to-text pipeline

## Purpose
Handles transcription of incoming voice messages (Telegram .ogg/opus audio).
Used before responding to any voice message from any user.

## Pipeline
1. Receive audio file (Telegram .ogg/opus).
2. SSH to homelab STT server (`${agent.tools.stt.host}`).
3. Activate venv: `${agent.tools.stt.venv}`.
4. Run faster-whisper with VAD filter: language=RU, vad_filter=True.
5. Return transcript to main session.
6. Respond based on transcript.

## Configuration
- Host: `${agent.tools.stt.host}` (homelab primary SSH)
- venv: `${agent.tools.stt.venv}`
- Engine: faster-whisper
- Default language: RU
- VAD filter: enabled (vad_filter=True)
- Dependency: ffmpeg must be available

## Rules & Directives
- ALWAYS run STT before responding to voice messages — applies to ALL users without exception.
- Use RU language by default unless user context suggests otherwise.
- Enable vad_filter=True to reduce background noise artifacts.

## Variables
- `agent.tools.stt.host` — STT server SSH host:port (homelab primary: 95.165.27.175:22022)
- `agent.tools.stt.venv` — Python venv path: `~/stt-venv`
- `agent.tools.stt.engine` — `faster-whisper`

## Accumulated rules
(empty)
