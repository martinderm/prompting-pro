# GPT-5.5 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-5.5` |
| **Provider** | OpenAI |
| **Source** | [OpenAI model page](https://developers.openai.com/api/docs/models/gpt-5.5), [Reasoning guide](https://developers.openai.com/api/docs/guides/reasoning), [Prompt engineering guide](https://developers.openai.com/api/docs/guides/prompt-engineering) |
| **Last reviewed** | 2026-04 |

---

## Key Characteristics

- Frontier model for complex professional work, coding, and agentic workflows.
- Supports `reasoning.effort`: `none`, `low`, `medium` (default), `high`, `xhigh`.
- Large context and output budget suited for long-horizon tasks.
- Strong tool ecosystem support in the Responses API.

---

## Official Prompting Guidance

### 1. Start from a clear outcome contract

- Define what counts as done.
- Specify constraints (format, policy, latency/cost boundaries).
- Ask for the final artifact directly, not exploratory prose.

### 2. Use reasoning effort as a tuning knob

- `medium` is a strong default for quality and reliability.
- Move to `high` / `xhigh` for difficult debugging, audits, and deep multi-step work.
- Move to `low` or `none` when latency dominates.

### 3. Keep tool workflows explicit

- Define available tools and expected call patterns.
- For function calling loops, pass outputs back in structured form.
- Treat tool schema quality as part of prompt quality.

### 4. Reserve output budget intentionally

- For complex tasks, allow enough token budget for both reasoning and final output.
- Detect and handle incomplete responses (`max_output_tokens` constraints).

### 5. Prefer structured outputs for machine use

- Use strict schemas for JSON outputs.
- Validate outputs and retry with precise correction messages.

---

## Prompt Template

```text
[DEVELOPER]
You are <role>.
Goal: <definition of done>.
Hard constraints:
- <constraint 1>
- <constraint 2>
Output contract:
- <exact format>

[USER]
Task:
<task>

Context:
<relevant context only>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Over-specifying internal thinking steps | Specify outcomes and constraints instead |
| Too low token budget for hard tasks | Increase `max_output_tokens` and reserve headroom |
| Weak tool schemas | Tighten schema, required fields, and descriptions |
