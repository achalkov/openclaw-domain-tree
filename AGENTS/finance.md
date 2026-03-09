# finance — Cost analysis, budget tracking, and financial queries

## Purpose
Rules for all finance-related tasks: API cost tracking, budget analysis, spend routing decisions,
and general financial queries.

Covers: OpenRouter/API cost monitoring, model cost comparisons, budget projections,
cost-saving routing rules, bank statement analysis.
Does NOT cover: science/tech product research without cost angle (→ knowledge/science/),
content publishing costs (→ content/).

## Rules & Directives

### Confidence and completeness (CRITICAL)
- Finance is 🔴 high-importance — confidence threshold 0.1
- NEVER extrapolate costs from a partial data sample without verifying coverage
  (Anti-pattern: taking 6 files out of 200+ and projecting — led to $14/mo estimate vs real $208/mo)
- Before any cost analysis: confirm you have the COMPLETE dataset
  (`find` all relevant files/logs, verify no gaps in date ranges)
- Always state the data range and sample completeness when reporting cost figures

### OpenRouter spend tracking (as of 2026-03-09)
- Current balance: ~$42 remaining from $50 limit
- 2-week stats (2026-02-23 → 2026-03-09):
  - Total spend: ~$102
  - gpt-5.3-codex: $99 (97%) — ACP/coding sessions, 1845 turns, 37M input tokens
  - Claude Sonnet 4.6: $1.34 (1%)
  - DeepSeek v3.2: $1.15 (1%)
- Monthly projection: ~$208 (range: $146–$271)
- Primary cost driver: ACP/Codex sessions (~97% of total)

### Cost-saving routing rules (applies to BOTH users: Artem 1285239 and Dasha 163037943)
- Routine/light tasks → route to agent `beta` (gpt-5-mini) via agent-to-agent
  Examples: text formatting, summarization, simple transformations, drafts without complex logic
- Long text processing → `beta` first; escalate to main model only if quality is insufficient
- Main model reserved for: advanced reasoning, high accuracy in ambiguous tasks, complex planning
- Preferred mechanism: `sessions_spawn`/`sessions_send` for agent-to-agent offload

### Model cost awareness
- ACP/Codex sessions dominate costs — scope them tightly
- For new ACP sessions: set clear exit conditions, avoid open-ended prompts
- When user asks about model cost/speed comparisons: pull current pricing from official sources
  (do not use training knowledge — pricing changes frequently)

### Bank statement analysis
- Recategorize vague transaction descriptions; do not leave items as "miscellaneous"
- Show transfer breakdown by recipient where applicable
- For spending pattern analysis: ensure date range covers full periods (full months, not partial)

## Variables
- `$OPENROUTER_API_KEY` — API key for OpenRouter (from environment)

## Accumulated rules
(empty)
