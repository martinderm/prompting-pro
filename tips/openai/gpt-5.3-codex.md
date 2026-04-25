# GPT-5.3-Codex - Unofficial Tips

Community tips for `gpt-5.3-codex` in autonomous coding loops.

---

## Coding Workflow Tips

Sources: [4], [5], [7]

Grounding:

- [4]: Production function-calling guidance supports constrained execution, explicit retries, and fallback handling.
- [5]: Engineering patterns support minimal-change patches, staged diagnosis, and verification gates.
- [7]: Practitioner reports reinforce stop conditions and blocker escalation in autonomous loops.

### Require minimal diffs

Ask for the smallest patch that satisfies acceptance criteria. This lowers regression risk and improves review speed.

### Separate diagnosis from implementation

First request root-cause hypotheses with evidence. Then request implementation.

### Keep verification explicit

Always ask for concrete verification steps (tests, lint, build) and final pass/fail status.

### Add stop and fallback conditions

Ask the model to stop after the first correct, validated fix and report blockers if it cannot complete.

---

## Prompt Skeleton for Agentic Tasks

Sources: [4], [5]

Grounding:

- [4]: Motivates explicit tool constraints, bounded actions, and clear failure reporting.
- [5]: Motivates acceptance checks and observable verification before completion.

```text
Goal:
<what must be fixed>

Constraints:
- minimal changes
- preserve public API
- no unrelated refactors

Verification:
- run <tests>
- run <lint/type checks>
- run <build if relevant>
- report failures with file paths
- if checks cannot run, explain why and propose next-best check
```

---

## Routing Note

Sources: [7]

Grounding:

- [7]: Practitioner operations commonly use a smaller helper stage before final synthesis.

If you need a lower-cost helper stage, run inventory/classification with `gpt-5.4-mini` and keep final code synthesis in `gpt-5.3-codex`.

---

## Shared Coding Overlay

For coding tasks, also apply the shared overlay: [codex.md](codex.md).

---

Community source index: [knowledge/sources/openai.md](../../knowledge/sources/openai.md#community-sources)
