# GPT-5.5 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-5.5` |
| **Provider** | OpenAI |
| **Source** | [OpenAI model page](https://developers.openai.com/api/docs/models/gpt-5.5), [Prompt guidance](https://developers.openai.com/api/docs/guides/prompt-guidance), [Reasoning guide](https://developers.openai.com/api/docs/guides/reasoning), [Prompt engineering guide](https://developers.openai.com/api/docs/guides/prompt-engineering) |
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

### 2. Add explicit stop rules and missing-evidence behavior

- Define when the model should stop searching and answer.
- Specify when to ask a clarification question versus make a safe assumption.
- Require minimal missing evidence requests (ask only for the smallest blocking field).

### 3. Use reasoning effort as a tuning knob

- `medium` is a strong default for quality and reliability.
- Move to `high` / `xhigh` for difficult debugging, audits, and deep multi-step work.
- Move to `low` or `none` when latency dominates.

### 4. Keep tool workflows explicit

- Define available tools and expected call patterns.
- For function calling loops, pass outputs back in structured form.
- Treat tool schema quality as part of prompt quality.

### 5. Use preambles for better perceived responsiveness

- In streaming or tool-heavy tasks, start with a short user-visible preamble before tool work.
- Keep preambles concise (one to two sentences) and action-oriented.
- For assistant item replay workflows, preserve `phase` values exactly (`commentary` and `final_answer`).

### 6. Reserve output budget intentionally

- For complex tasks, allow enough token budget for both reasoning and final output.
- Detect and handle incomplete responses (`max_output_tokens` constraints).

### 7. Control format and verbosity explicitly

- Set clear output shape and length bounds for the target audience.
- Use lower verbosity for short operational answers.
- For rewriting tasks, preserve artifact type, length, and structure before stylistic changes.

### 8. Prefer structured outputs for machine use

- Use strict schemas for JSON outputs.
- Validate outputs and retry with precise correction messages.

### 9. Add grounding and retrieval budgets

- Define what claims require citations.
- Limit retrieval loops with explicit budget rules.
- If evidence is insufficient, prefer generic safe output with labeled assumptions over unsupported specifics.

### 10. Prompt the model to check its work

- Require concrete validation steps when checks are available.
- If validation cannot run, require the model to explain why and provide a next-best check.

---

## Prompt Template

```text
[DEVELOPER]
Role: <1-2 sentence role definition>

# Personality
<tone and collaboration style>

# Goal
<user-visible outcome>

# Success criteria
<what must be true before final answer>

# Constraints
- <constraint 1>
- <constraint 2>

# Output
- <exact format>

# Stop rules
<when to continue, ask, fallback, or stop>

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
| No stop condition for retrieval loops | Add explicit retrieval budget and stop rules |
| Poor perceived latency in tool workflows | Add a short preamble before tool calls |
