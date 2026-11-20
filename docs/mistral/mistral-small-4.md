# Mistral Small 4 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `mistral-small-2603` (alias `mistral-small-latest`) |
| **Provider** | Mistral AI |
| **Source** | [Small 4 model card](https://docs.mistral.ai/models/model-cards/mistral-small-4-0-26-03), [Models overview](https://docs.mistral.ai/models), [Prompting guide](https://docs.mistral.ai/guides/prompting_capabilities), [Reasoning](https://docs.mistral.ai/inference/conversations/reasoning), [Sampling](https://docs.mistral.ai/guides/sampling), [Vision](https://docs.mistral.ai/capabilities/vision), [Changelog](https://docs.mistral.ai/resources/changelogs) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- Hybrid model unifying instruct, reasoning, and coding capabilities in a single multimodal model (119B total / 6.5B active parameters, 256k context window).
- Adjustable reasoning via `reasoning_effort`: `none` (minimal thinking, thinking chunk omitted, `message.content` is a plain string) or `high` (full thinking chunk before the final answer). No extra configuration required.
- Features: chat completions, function calling, agents & conversations, built-in tools, structured outputs, predicted outputs, document QnA, prefix, batching.
- Open weights under Apache 2.0 (Hugging Face: `mistralai/Mistral-Small-4-119B-2603`); same prompt shape via the API or self-hosted OpenAI-compatible servers (vLLM, etc.).

---

## Family Positioning and Migration Notes

- Small 4 absorbed three retired lines: **Magistral** (reasoning), **Pixtral** (vision), and **Devstral** (agentic coding). Their capabilities now live in Small 4 (and Large 4 / Ministral 3 for larger or edge deployments).
- Route within the family: Small 4 for general chat, high-volume, and cost-sensitive tasks; escalate to `mistral-large-4` (see [mistral-large-4.md](mistral-large-4.md)) for the hardest problems or 1M-context workloads; use `codestral` (see [codestral.md](codestral.md)) for IDE autocomplete / FIM.
- `mistral-medium-3-5` is deprecated (retires 2027-04) with Large 4 as the documented alternative; `mistral-large-2512` likewise. See the [models overview deprecation table](https://docs.mistral.ai/models).

---

## Ministral 3 Variant Note

- The **Ministral 3** family (`ministral-3b-2512`, `ministral-8b-2512`, `ministral-14b-2512`) provides the same text + vision capability at edge sizes (3B/8B/14B).
- Prompting shape is compatible with Small 4; use Ministral 3 for on-device / edge deployment and high-volume lightweight routing.

---

## Official Prompting Guidance

The provider-wide [prompting guide](https://docs.mistral.ai/guides/prompting_capabilities) applies - the shared rules (system vs. user prompt, clear role + task, hierarchical Markdown/XML structure, few-shot examples, no blurry words, no contradictions, no counting tasks, lean outputs, worded scales) are summarized in [mistral-large-4.md](mistral-large-4.md#official-prompting-guidance). Small 4 specifics:

### 1. Choose `reasoning_effort` by task class

- `none`: fast conversational chat, summarization, extraction, high-volume workloads - response is a plain string, no thinking chunk.
- `high`: complex coding, multi-step debugging, math, agentic tasks - response includes a full `ThinkChunk` before the final `TextChunk`, at the cost of extra tokens.

### 2. Handle thinking chunks correctly

- With `reasoning_effort="high"`, `message.content` is a list of chunks (`ThinkChunk` type `"thinking"`, then `TextChunk` type `"text"`); parse accordingly, including in streaming where `delta.content` changes shape between thinking and answer phases.
- In multi-turn conversations, always replay the full assistant message including the `ThinkChunk`; stripping it degrades quality.

### 3. Keep prompts compact for high-volume use

- Small 4 is the cost/latency-efficient tier: keep stable instructions in the system prompt, reuse them across requests, and set `prompt_cache_key` for shared prefixes (cached input billed at 10%).

### 4. Use vision inputs via `image_url` parts

- Small 4 accepts text + image input; send images as `image_url` content parts (URL or base64) next to a `text` part.

### 5. Sampling defaults

- Recommended `temperature` 0.0-0.7; tune `temperature` or `top_p`, not both; check the model-specific default via the `/models` endpoint.

---

## Prompt Template

```text
[SYSTEM]
You are <role>. Your task is to <task>.

# Rules
- <rule 1>
- <rule 2>

# Response Format
<exact format>

[USER]
# Context
<relevant context only>

# Task
<specific request>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Using `high` reasoning for simple high-volume tasks | Use `reasoning_effort="none"` and keep `content` parsing string-based |
| Assuming a plain string response in reasoning mode | Parse the chunk list (`ThinkChunk` + `TextChunk`) |
| Dropping thinking chunks between turns | Replay full assistant messages in history |
| Treating Small 4 as a drop-in for the hardest tasks | Escalate to `mistral-large-4` |
| Using deprecated Magistral/Devstral/Pixtral slugs | Migrate to Small 4 / Large 4 / Ministral 3 per the deprecation table |
