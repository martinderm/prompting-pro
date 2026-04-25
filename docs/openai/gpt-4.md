# GPT-4 — Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-4`, `gpt-4-turbo` |
| **Provider** | OpenAI |
| **Source** | [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) |
| **Last reviewed** | 2025-04 |

---

## Key Characteristics

- **Text-only** (gpt-4); **vision** support in `gpt-4-turbo` and `gpt-4-vision-preview`.
- **Context window**: 8 192 tokens (gpt-4), 128 000 tokens (gpt-4-turbo).
- **Instruction following**: very strong; benefits from explicit, well-structured system prompts.
- **Default behaviour**: no built-in reasoning pause — use explicit chain-of-thought (CoT) instructions.

---

## Official Strategies

Guidance below is consistent with OpenAI's Prompt Engineering guide (same six strategies apply; this file highlights GPT-4-specific considerations).

### 1. Write clear instructions

- Use the **system message** to establish role, tone, and hard constraints before any user turn.
- For gpt-4 (8 k window) be concise in the system prompt; every token counts.
- Use numbered or bulleted lists for multi-part instructions — GPT-4 follows structure well.

### 2. Provide reference text

- Inject relevant context into the **user** message (not the system message) so the model treats it as evidence, not as a standing rule.
- For the 8 k window, carefully budget tokens: aim for ≤ 2 000 tokens of reference to leave room for the response.
- For gpt-4-turbo (128 k), larger documents can be included, but still summarise when possible to keep costs down.

### 3. Split complex tasks into simpler subtasks

- Multi-step workflows benefit from chaining: pass the structured output of one call as the input to the next.
- GPT-4 handles structured JSON output reliably — use `response_format: { type: "json_object" }` (API) when downstream parsing is required.

### 4. Give the model time to think

- Prompt: "Before answering, list the key considerations, then provide your answer."
- GPT-4 is good at self-critique: "Review your answer for errors, then provide a corrected version."

### 5. Use external tools

- Use **function calling** for any task that needs current data, precise arithmetic, or side effects.
- Prefer structured function schemas over free-text tool descriptions.

### 6. Test changes systematically

- Compare prompt variants on at least 10–20 representative examples before adopting a change.
- Log cost (tokens) alongside quality; GPT-4 is more expensive than GPT-3.5 — ensure quality gain justifies cost.

---

## Prompt Template

```
[SYSTEM]
You are <persona>. <Constraints>. Respond in <format>.

[USER]
Reference material:
---
<reference text>
---

<Task instruction>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Hitting the 8 k context limit | Switch to gpt-4-turbo or truncate/summarise reference material |
| Expecting up-to-date facts | Use function calling + retrieval |
| Ignoring system prompt mid-conversation | Re-inject critical rules periodically or use gpt-4-turbo's larger window |
