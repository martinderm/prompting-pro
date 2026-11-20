# GLM-5.3 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `glm-5.3` |
| **Provider** | Z.ai |
| **Source** | [GLM-5.3 model guide](https://docs.z.ai/guides/llm/glm-5.3), [Chat Completion API reference](https://docs.z.ai/api-reference/llm/chat-completion), [Deep Thinking](https://docs.z.ai/guides/capabilities/thinking), [Context Caching](https://docs.z.ai/guides/capabilities/cache), [Hugging Face model card](https://huggingface.co/zai-org/GLM-5.3), [Release notes](https://docs.z.ai/release-notes/new-released) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- Z.ai flagship for complex software engineering and long-horizon agent tasks. Same base model as GLM-5.2 (744B total / ~40B active MoE plus an MTP layer); all gains come from post-training.
- Text-only input; 1M-token context window (1,048,576); max output 128K tokens.
- Reasoning is always on: `thinking.type` accepts only `enabled` (sending `disabled` fails the request). `reasoning_effort` accepts only `low`, `high`, `max` and defaults to `max`; Z.ai recommends `max` for complex tasks such as coding.
- Capabilities: thinking mode, streaming, function calling, context caching, structured output (JSON).
- Open weights on Hugging Face (`zai-org/GLM-5.3`, BF16/FP8) under the custom GLM-5.3 License; code repo `zai-org/GLM-5` under Apache-2.0. Also served third-party on Mistral La Plateforme as `zai-glm-5-3`.
- API protocols: OpenAI-compatible Chat Completions (`https://api.z.ai/api/paas/v4`; GLM Coding Plan: `https://api.z.ai/api/coding/paas/v4`), OpenAI Responses (`https://api.z.ai/api/v1`), Anthropic Messages (`https://api.z.ai/api/anthropic`).

---

## Variant Note

- `glm-5.3-flash` is the natively multimodal, cost-efficient sibling (320B total / 18B active) - see [glm-5-3-flash.md](glm-5-3-flash.md).
- `glm-5.3` is text-only; for image, video, or file input use GLM-5.3-Flash.

---

## Official Prompting Guidance

### 1. Control reasoning via parameters, never via prompt text

- Set `thinking: {"type": "enabled"}` and an explicit `reasoning_effort`. Omitting `reasoning_effort` lands on `max` - slower and more expensive than needed for simple turns.
- `low` = lightweight reasoning, `high` = enhanced, `max` = deep (recommended for coding and other complex tasks). Higher effort increases response time and output tokens.
- Do not ask the model to "think step by step" in the prompt; the effort parameter does this better.

### 2. Migrate off `thinking.type: "disabled"` before switching model IDs

- GLM-5.3 rejects `disabled`. Change it to `enabled` and set `reasoning_effort: "low"` before updating the model ID to `glm-5.3`, otherwise the request fails.

### 3. Use the standard system/user split

- Put the stable role, behavior, and output rules in the `system` message (Z.ai's quick-start pattern is a role definition, e.g. "You are a senior full-stack software engineer..."); put the concrete task in the `user` message.
- The API is stateless: resend the system prompt and history with every request.

### 4. Keep sampling at documented defaults unless you measure

- `temperature` defaults to 1.0 for the GLM-5.x series (allowed range 0.0-1.0); Z.ai's own evaluations use temperature 1.0 with top_p 0.95-1.0.
- Tune `temperature` or `top_p`, not both.

### 5. Budget output tokens for reasoning

- Reasoning is returned separately (`reasoning_content` / `reasoning_details`; `delta.reasoning_content` when streaming) and billed as output tokens (`usage.completion_tokens_details.reasoning_tokens`). Leave room in `max_tokens` for reasoning plus the final answer.

### 6. Manage multi-turn reasoning explicitly

- `clear_thinking` (default `true` on the standard API) clears `reasoning_content` from previous turns. In the open chat template it defaults to `false` - pass `clear_thinking=true` explicitly for plain chat scenarios.

### 7. Function calling: precise schemas, replay full messages

- Pass `tools` as JSON Schema function definitions; validate generated arguments before executing. When replaying history in tool loops, retain the assistant tool-call message and any reasoning fields.
- Interleaved thinking between tool calls is supported; for streaming tool arguments enable `tool_stream: true`.

### 8. Use structured outputs for machine-consumed responses

- Use `response_format` with a strict JSON schema for extraction and pipelines; validate the payload in code regardless.

### 9. Design prompts for automatic context caching

- Caching is automatic - there is no cache key to set. Keep the stable part (system prompt, tool schemas, long reference material) at the beginning of the prompt and append new content at the end. Cached input tokens are billed at a discount (GLM-5.3: $0.26/M vs $1.40/M standard input).

### 10. Write task prompts like work tickets

- GLM-5.3 is trained for agentic engineering work: state the goal, constraints, definition of done, and verification steps. On consequential outputs, ask for trade-offs and an explicit separation of confirmed vs. unverified results.

---

## Prompt Template

```text
[SYSTEM]
You are <role> with <expertise>.
Rules:
- <stable rule 1>
- <output format rule>

[USER]
# Goal
<one-sentence outcome>

# Context
<only relevant files/facts; keep the stable prefix first>

# Constraints
- <hard constraint>

# Definition of done
- <observable completion criteria>
- Verify <checks> before reporting; separate confirmed from unverified results.
```

Request shape: `model: "glm-5.3"`, `thinking: {"type": "enabled"}`, `reasoning_effort: "max"` for coding tasks, `max_tokens` with headroom for reasoning, `temperature: 1.0` (default).

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Sending `thinking: {"type": "disabled"}` | Rejected by GLM-5.3; use `enabled` + `reasoning_effort: "low"` |
| Omitting `reasoning_effort` | Defaults to `max` - slower and costlier than needed |
| `max_tokens` too small for reasoning + answer | Reasoning counts toward output tokens; budget headroom |
| Dropping reasoning fields when replaying tool-loop history | Replay full assistant messages incl. reasoning and tool_calls |
| Treating GLM-5.3 as multimodal | Text-only; use `glm-5.3-flash` for images/video/files |
| Rewriting the stable prefix between turns | Breaks automatic context caching; append new content instead |
| Assuming reasoning is free | Reasoning tokens are billed at the output rate |
