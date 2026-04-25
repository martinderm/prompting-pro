# GPT-5.3-Codex - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-5.3-codex` |
| **Provider** | OpenAI |
| **Source** | [OpenAI model page](https://developers.openai.com/api/docs/models/gpt-5.3-codex), [Prompt guidance](https://developers.openai.com/api/docs/guides/prompt-guidance), [Codex prompting guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide), [Reasoning guide](https://developers.openai.com/api/docs/guides/reasoning) |
| **Last reviewed** | 2026-04 |

---

## Key Characteristics

- Optimized for agentic coding environments.
- Supports `reasoning.effort`: `low`, `medium`, `high`, `xhigh`.
- Strong for repository-grounded tasks, patch generation, and iterative fix loops.

---

## Variant Note

- No dedicated `gpt-5.3-codex-mini` variant is currently tracked in this repository.
- If lower-cost coding agents are needed, route simpler steps to `gpt-5.4-mini` and keep complex synthesis on `gpt-5.3-codex`.

---

## Official Prompting Guidance

### 1. Define repository-aware constraints

- Declare language/runtime boundaries.
- State style and safety constraints explicitly.
- Specify whether tests/linting are required before final output.

### 2. Ask for action-oriented outputs

- Prefer concrete diffs, commands, and migration steps.
- Avoid generic explanations when execution artifacts are required.

### 3. Drive iterative coding loops

- Provide compile/test failures as structured feedback.
- Request minimal corrective patches per iteration.
- Re-check against the same acceptance criteria each round.

### 4. Add explicit stopping conditions

- Stop when the core request is satisfied with evidence from code/tests.
- If blocked, ask for the smallest missing input or permission.
- Do not continue looping only for stylistic improvements unless requested.

### 5. Prompt the model to check its work

- Require concrete validation commands (targeted tests, lint/type checks, build).
- Require explicit handling when validation cannot run.
- Include failure behavior and open questions in implementation plans.

### 6. Balance effort with scope

- `medium` for most coding tasks.
- `high/xhigh` for deep debugging, security review, or architecture-heavy refactors.

---

## Prompt Template

```text
[DEVELOPER]
You are an autonomous coding assistant.
Constraints:
- <tech stack and style>
- <safety and non-goals>
Done when:
- <acceptance criteria>

[USER]
Repository context:
<files, errors, task>

Deliverables:
1. <patch plan>
2. <implementation>
3. <verification>
4. <what remains / blockers>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Vague coding objective | Add measurable acceptance criteria |
| Large, mixed-scope edits in one pass | Enforce minimal, testable patch increments |
| Missing verification loop | Require lint/test/build checks before completion |
