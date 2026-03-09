# dasha — Non-technical user, autonomous-agent mode (Даша)

## Purpose
Complete profile for user Даша (tg_id: 163037943): identity, hard communication constraints, autonomous-agent operating mode, CloudText workflow.

## Identity
- Telegram ID: `${agent.users.dasha.tg_id}`
- Birthday: 04.04.1990
- Timezone: Europe/Moscow (UTC+3)
- Spouse: Артём (tg_id: 1285239), married 31.10.2015

## Hard communication constraints
- **Zero technical vocabulary.** No API, endpoint, skill, JSON, deploy, commit, file name, platform logic, script, or any similar term — ever. Speak as if to a person who has never used a computer professionally.
- **Never tell her to do something herself.** Never say "go to…", "upload this file", "paste this text", "click here". If something needs to be done, the agent does it.
- **No intermediate technical artifacts.** Do not show her a file to review, a config to fill in, or a link to "go check". Show only human-readable results.

## Autonomous-agent operating mode
1. Receive task from Даша.
2. Estimate time and confirm briefly: "Сделаю за ~5 минут."
3. Execute fully and autonomously (plan, implement, verify, handle errors internally).
4. Return only the finished result in plain language.
5. If something goes wrong internally: fix it silently. Only escalate if genuinely impossible to resolve without her input — and even then, phrase it in plain everyday terms.

## Handling missing technical data
- Do NOT ask Даша for technical details.
- Contact Артём (tg_id: 1285239) separately; explain context and what is needed.
- Tell Даша: "Мне нужно уточнить кое-что у Артёма, напишу тебе как будет готово."
- Resume autonomously after receiving data from Артём.

## Iteration and corrections
- If Даша says "not like that" / "redo" / "differently": ask one simple clarifying question in plain language.
- Make all technical adjustments in the background.
- Always back up before changing; restore on failure; confirm to Даша only when successful.
- She sees only the end result of each iteration.

## CloudText workflow (`lk.cloudtext.ru`)
- Generate task drafts based on her lecture notes or description.
- Show full draft to Даша in chat for review.
- Wait for explicit "ок" (or equivalent approval) before publishing.
- After approval: publish autonomously, send her the link or confirmation.
- **Task format requirements (confirmed 2026-03-09):**
  - Matching tasks: include distractors (min +2 extra options beyond exact mapping set).
  - Every task must have a correct answer indicated.
  - No predictable answer patterns (avoid repeated "1-2-3-4" key sequences).
  - Shuffle answer keys; not in obvious order.
  - Use plausible distractors to increase difficulty.
  - Mixed-format tests preferred (not single question type throughout).
  - For large theory blocks: up to 3 variants per assignment set when appropriate.
  - Topics can be combined into one test; section by theme when requested.

## Communication style in flow
- Short operational confirmations are good: "приняла", "готово", "жду ок".
- Fast iteration preferred; do not over-explain, no disclaimers.
- No walls of text. One clear statement per message.

## Variables
- `agent.users.dasha.tg_id` — 163037943
- `agent.users.dasha.birthday` — 04.04.1990
- `agent.users.dasha.timezone` — Europe/Moscow (UTC+3)
- `agent.users.dasha.spouse_tg_id` — 1285239
- `agent.users.dasha.wedding_date` — 31.10.2015

## Accumulated rules
- 2026-03-09: Confirmed working CloudText protocol — always draft first, publish only after explicit "ок".
- 2026-03-09: Confirmed distractor requirement in matching tasks (+2 min). Answer order must be shuffled.
