# cloudtext — Educational task publishing on lk.cloudtext.ru

## Purpose
Rules for creating and publishing educational tasks/tests on the CloudText platform
(`lk.cloudtext.ru`).

Covers: task generation from source material, draft review workflow, publishing via API.
Does NOT cover: Telegram messaging (→ ./telegram.md), generic content drafting.

## Rules & Directives

### Workflow (mandatory order)
1. Generate task drafts from provided material
2. Show drafts in chat for user review (Dasha: 163037943)
3. Wait for explicit "ок" or approval
4. ONLY after approval: publish autonomously via CloudText API
5. Return edit/share links to user

Do NOT publish before approval. Do NOT ask Dasha to publish herself.

### Task format requirements

#### Matching tasks
- Include distractors: at minimum +2 options beyond the exact mapping set
- Example: if mapping set has 4 pairs, provide ≥6 answer options total
- This is an explicit user requirement; do not skip distractors

#### All task types
- Provide the correct answer for each task (for internal verification and answer key)
- Avoid predictable answer patterns — no repeated sequences like "1234", "AABB", etc.
- Shuffle answer keys so correct answers are not in obvious positional order
- Use plausible distractors that require actual knowledge to distinguish from correct answers
- Increase difficulty by mixing related-but-wrong facts, not just random noise

### Test composition preferences
- Mixed-format tests strongly preferred over single-question-type tests
  (combine: single choice, multiple choice, matching, short answer, etc.)
- For large theory blocks: generate up to 3 variants of the test
- Can combine multiple topics into one test; section by theme when requested
- Short confirmations in chat are good: "черновик готов", "жду ок", "опубликовано"

### Publishing tool
- Use the `cloudtext-publisher` skill for API-first publishing
- Skill location: `~/.openclaw/workspace/skills/cloudtext-publisher/SKILL.md`
- Script: `scripts/cloudtext_task_tool.py` (workspace utility)
- Platform URL: `https://lk.cloudtext.ru`

### Communication rules (Dasha context)
- Never say "вот файл — выложи сама" or similar
- Never expose API terms, endpoint names, JSON structure to Dasha
- Show only: draft content, confirmation of publishing, edit/share links
- If tech data is needed that Dasha can't provide: escalate to Artem (1285239)

## Variables
- `$CLOUDTEXT_API_TOKEN` — API token for lk.cloudtext.ru (from environment)

## Accumulated rules
(empty)
