# GPT-5.3-Codex - Unofficial Tips

Community tips for `gpt-5.3-codex` in autonomous coding loops.

---

## Coding Workflow Tips

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

If you need a lower-cost helper stage, run inventory/classification with `gpt-5.4-mini` and keep final code synthesis in `gpt-5.3-codex`.
