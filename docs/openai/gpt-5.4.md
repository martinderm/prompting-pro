# GPT-5.4 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-5.4` |
| **Provider** | OpenAI |
| **Source** | [OpenAI model page](https://developers.openai.com/api/docs/models/gpt-5.4), [Reasoning guide](https://developers.openai.com/api/docs/guides/reasoning), [Prompt engineering guide](https://developers.openai.com/api/docs/guides/prompt-engineering) |
| **Last reviewed** | 2026-04 |

---

## Key Characteristics

- Cost-efficient frontier model for coding and professional workflows.
- Supports `reasoning.effort`: `none` (default), `low`, `medium`, `high`, `xhigh`.
- Strong default for production workloads that need quality with better cost profile than GPT-5.5.

---

## Mini/Nano Variant Note

- Officially related variants include `gpt-5.4-mini` and `gpt-5.4-nano`.
- Prompting shape is largely compatible with GPT-5.4.
- Use these variants for classification, routing, extraction, and high-volume agent sub-steps.

---

## Official Prompting Guidance

### 1. Use explicit instruction hierarchy

- Put stable behavior and constraints in `developer` instructions.
- Put task-specific context in `user` input.
- Restate non-negotiable output requirements close to the task.

### 2. Tune effort by task class

- `none/low`: fast operations (triage, extraction, short transforms).
- `medium`: balanced coding and analysis.
- `high/xhigh`: complex refactoring, multi-file diagnosis, higher-stakes reviews.

### 3. Keep context relevant and bounded

- Remove unrelated data from prompts.
- For long histories, summarize and carry forward only required facts.

### 4. Prefer strict structures for downstream pipelines

- Use strict schema mode for machine-consumed outputs.
- Include deterministic formatting rules in the prompt contract.

---

## Prompt Template

```text
[DEVELOPER]
Role: <role>
Rules:
- <rule 1>
- <rule 2>
Output:
- <exact format>

[USER]
Task: <task>
Required checks:
- <check 1>
- <check 2>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Missing explicit output contract | Add schema or concrete format section |
| Using high effort for simple jobs | Start low and raise only if evals justify it |
| Treating mini as drop-in for hardest tasks | Escalate hard cases to GPT-5.4 or GPT-5.5 |
