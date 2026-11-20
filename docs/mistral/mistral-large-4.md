# Mistral Large 4 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `mistral-large-4`, `mistral-large-4-0` (alias `mistral-large-latest`) |
| **Provider** | Mistral AI |
| **Source** | [Large 4 model card](https://docs.mistral.ai/models/mistral-large-4-0), [Models overview](https://docs.mistral.ai/models), [Prompting guide](https://docs.mistral.ai/guides/prompting_capabilities), [Reasoning](https://docs.mistral.ai/inference/conversations/reasoning), [Sampling](https://docs.mistral.ai/guides/sampling), [Chat completions](https://docs.mistral.ai/inference/conversations/chat-completion), [Vision](https://docs.mistral.ai/capabilities/vision), [Structured outputs](https://docs.mistral.ai/capabilities/structured_output), [Function calling](https://docs.mistral.ai/inference/conversations/function-calling), [Prompt caching](https://docs.mistral.ai/inference/conversations/advanced/prompt-caching) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- State-of-the-art, open-weight, general-purpose multimodal model with a granular Mixture-of-Experts architecture (1.05T total / 52B active parameters, 1.6B vision encoder).
- 1M token context window; input: text and images; output: reasoning + text.
- Always reasons: `reasoning_effort` supports only `low`, `medium`, `high`. `high` is the default and the recommended starting point. `none`, `minimal`, `xhigh`, and `max` are not accepted by this model.
- Features: chat completions, function calling, structured outputs, predicted outputs, prefix, document QnA, batching, agents & conversations, built-in tools/connectors.
- Open weights under the Mistral Ecosystem Open Weight License; served via the Mistral API (La Plateforme / Studio) and self-hostable.

---

## Family Positioning

- `mistral-large-4` is the flagship for the hardest problems, very long context, agentic work, coding, and multimodal input.
- `mistral-small-4` covers everyday chat, high-volume, and cost-sensitive work - see [mistral-small-4.md](mistral-small-4.md).
- `codestral` remains the specialist for low-latency code completion / FIM - see [codestral.md](codestral.md).
- Deprecated predecessors (`mistral-large-2512`, `mistral-medium-3-5`) point to Large 4 as their alternative; the Magistral, Devstral, and Pixtral lines are retired and their capabilities moved into Large 4, Small 4, and Ministral 3 (see the [models overview deprecation table](https://docs.mistral.ai/models)).

---

## Official Prompting Guidance

The provider-wide [prompting guide](https://docs.mistral.ai/guides/prompting_capabilities) applies to Large 4; the key rules are:

### 1. Separate system prompt and user prompt

- Put stable behavior, role, and constraints in the `system` message (developer-managed, at the start of the conversation).
- Put the task and current context in the `user` message.
- If you cannot control the system prompt, concatenate instructions with the query in a single `user` message.

### 2. Define a clear purpose

- Start with a concise role and task definition: "You are a `<role>`, your task is to `<task>`."

### 3. Structure the prompt hierarchically and completely

- Organize instructions into clear sections using Markdown headings and/or XML-style tags (readable, parsable, familiar to the model).
- Write as if for someone with no prior context: the prompt should be clear and complete on its own.

### 4. Use few-shot examples when output format matters

- Provide examples directly in the prompt or as `user`/`assistant` message pairs; match the example format to the desired output format.

### 5. Avoid blurry and subjective words

- Replace vague qualifiers ("too long", "many", "interesting", "make it better") with objective measures and exact criteria.

### 6. Avoid contradictions in long prompts

- Resolve overlapping conditional rules with an explicit decision tree instead of contradictory instructions.

### 7. Do not make the model count

- Provide character/word/item counts as input data instead of asking the model to count words or characters.

### 8. Keep generated output lean

- Models ingest tokens faster than they generate them; with structured outputs, ask only for what is strictly necessary.

### 9. Prefer worded scales for ratings

- Use labeled scales (e.g. Very Low / Low / Neutral / Good / Very Good with definitions) instead of bare numeric 1-5 scales.

### 10. Control reasoning via `reasoning_effort`, not prompt scripting

- `low`: simple tasks, minimal reasoning compute. `medium`: balance of quality, tokens, latency. `high` (default, recommended): complex tasks, best quality.
- Do not ask the model to "think step by step" in the prompt; set the parameter in the API request.
- When reasoning is active, `message.content` is a chunk list: a `ThinkChunk` (`type: "thinking"`) with the reasoning trace, followed by a `TextChunk` (`type: "text"`) with the final answer.

### 11. Replay full assistant messages in multi-turn conversations

- Always append the full assistant message, including the `ThinkChunk`, back into the message history. Stripping the reasoning trace increases token efficiency but significantly degrades output quality.

### 12. Tune sampling conservatively

- Recommended `temperature` range is 0.0-0.7 (0.2 = focused/deterministic, 0.7 = more random). Change `temperature` or `top_p`, not both. The default varies by model - check the `/models` endpoint.

### 13. Use structured outputs and function calling deliberately

- Custom structured outputs (`response_format` with a JSON schema) are more reliable and recommended; JSON mode only guarantees valid JSON and requires you to explicitly instruct the model in the prompt to output JSON and to specify the format.
- Describe tools with a precise JSON schema: type, function name, description, parameters, and required parameters.

### 14. Send images as `image_url` content parts

- Use a publicly accessible URL or a base64-encoded image inside the `content` list alongside a `text` part.
- For document parsing, OCR, and data extraction, prefer Document AI (OCR service) over pure vision prompting.

### 15. Exploit prompt caching for repeated prefixes

- Keep stable prefixes (system prompt, tool definitions, long shared context) at the start of the prompt and set a stable `prompt_cache_key` (e.g. conversation or session ID, never secrets). Cached input tokens are billed at 10% of the standard input price.

### 16. Iterate on prompts like code

- Model updates can change behavior; revisit prompts after model changes and evaluate the impact of each change.

---

## Prompt Template

```text
[SYSTEM]
You are <role>. Your task is to <task>.

# Rules
- <stable behavior rule>
- <hard constraint>

# Response Format
<exact format, or reference to the JSON schema>

[USER]
# Context
<only the relevant context>

# Task
<specific request>

# Examples (optional)
Input: <example input>
Output: <example output in the required format>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Sending `reasoning_effort: "none"` to Large 4 | Not accepted; use `low` for the least reasoning |
| Scripting chain-of-thought steps in the prompt | Set `reasoning_effort` in the API instead |
| Stripping `ThinkChunk` from history in multi-turn chats | Replay the full assistant message including thinking chunks |
| Vague qualifiers ("make it better", "too long") | State objective, measurable criteria |
| Contradictory conditional rules in long prompts | Replace with an explicit decision tree |
| JSON mode without a JSON instruction in the prompt | Add the instruction, or use custom structured outputs (`json_schema`) |
| Changing `temperature` and `top_p` together | Tune one parameter at a time |
| Re-sending long unchanged prefixes without a cache key | Set a stable `prompt_cache_key` |
