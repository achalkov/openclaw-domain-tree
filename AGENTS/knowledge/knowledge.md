# knowledge — Research, reference, and factual queries

## Purpose
Covers tasks where the primary goal is finding, verifying, or explaining factual information.
Includes: academic research, history queries, science/tech lookups, teaching material research,
general reference questions, "similar recommendations" requests.

Does NOT cover: content creation for publishing (→ content/), code-related lookups (→ coding/),
financial analysis (→ finance/).

## Routing
- `./history.md` — historical facts, academic history, ЕГЭ/ОГЭ prep materials
- `./science.md` — science, technology, space, engineering concepts

## Decision boundaries
- Query is about historical events, dates, figures, or teaching history → history.md
  because history has specific academic requirements (ЕГЭ/ОГЭ prep context, source verification)
- Query is about science, technology, space, or engineering concepts → science.md
  because science queries often require up-to-date sources and have different verification needs
- General knowledge that doesn't fit history or science (geography, culture, recommendations) → handled at this level

## Rules & Directives

### Verification first
- All knowledge queries are subject to confidence thresholds from AGENTS.md
- 🔴 Important questions (affect real decisions): threshold 0.1 — verify before answering
- 🟡 Medium importance: threshold 0.25
- 🟢 Light/casual: threshold 0.4 — self-verify via web/docs, then answer
- Never answer from training knowledge alone on factual claims — use web_search or primary sources

### Research methodology
- Find ALL relevant sources before drawing conclusions (not just the first result)
- Cross-check with ≥2 independent sources for important claims
- For "similar recommendations" (games, books, films): always verify the genre and core-loop
  of the reference item first — do not assume based on franchise name or vague category

### Source priority
1. Official documentation / primary sources
2. Academic / peer-reviewed
3. Reputable secondary sources
4. General web (use with caution; cross-check)

## Variables
(none)

## Accumulated rules
(empty)
