# DeepSeek V4.1 Flash (1017) - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `deepseek-flash` (API alias served by **DeepSeek-V4.1-Flash-1017**, released 2026-10-17); on Mistral La Plateforme: `vv4.1-flash-1017` |
| **Provider** | DeepSeek |
| **Source** | [Thinking Mode](https://api-docs.deepseek.com/guides/thinking_mode/), [Chat Completions API](https://api-docs.deepseek.com/api/create-chat-completion/), [Vision](https://api-docs.deepseek.com/guides/vision/), [Tool Calls](https://api-docs.deepseek.com/guides/tool_calls/), [JSON Output](https://api-docs.deepseek.com/guides/json_mode/), [Models & Pricing](https://api-docs.deepseek.com/quick_start/pricing/), [Change Log](https://api-docs.deepseek.com/updates/), [V4.1-Flash-1017 news](https://api-docs.deepseek.com/news/news261017/), [HF model card](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017), [Mistral model card](https://docs.mistral.ai/models/deepseek-v4-flash-1017) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- Smallest model in DeepSeek's V4.1 Causal Encoder-Decoder (CED) architecture family; sparse MoE with native multimodal (text + image) input. 1017 is a post-training refresh of V4.1-Flash (2026-09-10) with stronger reasoning/coding/agentic/visual results and shorter outputs.
- 1M-token (1,000,000) context window; max output up to 384K tokens via the DeepSeek API (128K via Mistral hosting).
- Thinking mode is **enabled by default** with default effort `high`; controllable via `thinking.type` (`enabled`/`disabled`) and `reasoning_effort` (`none`/`low`/`high`/`max`).
- Open weights under MIT (`deepseek-ai/DeepSeek-V4.1-Flash-1017` on Hugging Face). Also hosted third-party on Mistral La Plateforme as `vv4.1-flash-1017` (public preview, served without Mistral modifications, text+image, optimized for long-context coding and agentic workflows).
- API: OpenAI-compatible `https://api.deepseek.com` (`/chat/completions`, `/responses`), plus Anthropic-compatible `/anthropic/v1/messages`. Peak/off-peak pricing (off-peak = half); automatic context caching (cache hits billed at 1/10 of input).

---

## Model IDs and Lifecycle

- Use `deepseek-flash` for new integrations - it now serves DeepSeek-V4.1-Flash-1017 with unchanged calling method and pricing.
- Retired but still accepted aliases route to V4.1-Flash-1017 at the Flash price: `deepseek-v4-flash`, `deepseek-v4-flash-vision-exp`, and the legacy `deepseek-chat` / `deepseek-reasoner` (retired 2026-07-24).
- `deepseek-v4-pro` (1.6T / 49B active MoE, text-only, no vision) is the larger sibling; not covered by this file.

---

## Official Prompting Guidance

### 1. Set the thinking mode explicitly

- Thinking is on by default with effort `high`. Pass `reasoning_effort: "none"|"low"|"high"|"max"`, or `thinking: {"type": "enabled"/"disabled"}` (via `extra_body` with the OpenAI SDK); if `thinking` is provided, `type` takes precedence over `reasoning_effort`.
- Compatibility aliases: `minimal` -> `low`, `medium`/`xhigh` -> `high`, `ultra` -> `max`. Prefer the documented values.
- In thinking mode the chain-of-thought is returned separately in `reasoning_content` (streaming: `delta.reasoning_content`), alongside `content`. Do not mix it into the answer text.
- Do not ask the model to "think step by step" in the prompt; use the parameters.

### 2. Follow the multi-turn reasoning rules

- Without `tools`: previous turns' `reasoning_content` is ignored by the API - no need to pass it back.
- With `tools`: you MUST pass the full `reasoning_content` of all previous turns back in every request (append the whole assistant message); otherwise the API returns a 400 error.

### 3. Respect the sampling rules of thinking mode

- `temperature` (range 0-2, default 1) has **no effect in thinking mode**; `presence_penalty`/`frequency_penalty` are deprecated and never take effect. Tune `temperature` or `top_p`, not both.
- `top_p` for `deepseek-flash`: in thinking mode only the range 0.95-1.0 is effective (below 0.95 is treated as 0.95; default 1.0); in non-thinking mode it is fixed at 1.0.

### 4. Budget `max_tokens` for reasoning

- `max_tokens` accepts 1..384K. Defaults: 8K in non-thinking mode, 64K in thinking mode, 128K with `reasoning_effort: "max"`. Reasoning tokens count toward `completion_tokens` (see `usage.completion_tokens_details.reasoning_tokens`) and bill as output. Input + output together are limited by the 1M context.

### 5. Send images as content blocks

- `deepseek-flash` accepts images in `user`/`system`/`tool` messages (not `assistant` - that returns 400). Use a `content` array with `text` + `image_url` blocks: `image_url.url` = public `http(s)` URL (max 8192 chars, image <= 32 MiB, download <= 60 s) or base64 `data:` URL (counts toward the 48 MiB body limit); or a `file` block referencing a Files API `file_id` (up to 64 MiB).
- Formats: JPEG, PNG, GIF, WebP. `detail: "low"` downsamples to 512x512 (faster/cheaper); `high`/`original`/`auto` keep the original. Limits: max 600 images per request, <= 1024 tokens per image after automatic resizing.

### 6. Tool calling: JSON schemas, thinking-mode restrictions

- Declare function tools with a JSON Schema `parameters` object (optional `strict: true` beta for schema-enforced calls). Validate the generated `arguments` yourself before executing.
- In thinking mode, `tool_choice` only supports `none`/`auto` - `required` or a named tool return a 400 error (disable thinking first). With the built-in web tools declared, `required` is treated as `auto`.
- Built-in server-side web tools: `deepseek_web_search` and `deepseek_read_url` (pass `server_tool_calls` back unchanged in follow-up requests).

### 7. JSON output requires a prompt instruction too

- Set `response_format: {"type": "json_object"}` AND instruct the model in a system/user message to output JSON (e.g. include the schema). Non-JSON output may be replaced with spaces (content can look empty) - retry on empty content and watch `finish_reason: "length"`.

### 8. Exploit automatic context caching

- Caching is automatic - keep the stable prefix (system prompt, tool schemas, long reference material) at the start of the prompt and append new content at the end. Read the hit ratio from `usage.prompt_cache_hit_tokens` / `prompt_cache_miss_tokens`; cache hits are billed at 1/10 of the input price.

### 9. Use the standard system/user split

- Stable role and rules in the `system` message, concrete task in the `user` message. The API is stateless: resend system prompt and history each request.

### 10. Write coding/agent tasks as tickets with a definition of done

- With 1M context you can include whole files/repos; state goal, constraints, acceptance checks, and ask for verified vs. unverified results on consequential outputs.

---

## Prompt Template

```text
[SYSTEM]
You are <role>.
Rules:
- <stable rule 1>
- Output format: <format or "JSON matching schema ...">

[USER]
# Goal
<one-sentence outcome>

# Context
<relevant files/facts; keep the stable prefix first for cache hits>

# Constraints
- <hard constraint>

# Definition of done
- <observable completion criteria / checks>
```

Request shape: `model: "deepseek-flash"`, `thinking: {"type": "enabled"}`, `reasoning_effort: "high"` (default) or `"max"` for hard agent tasks, `max_tokens` with headroom for reasoning.

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Relying on the default thinking mode | Set `thinking`/`reasoning_effort` explicitly - the checkpoint behind `deepseek-flash` can change |
| Using `temperature` to make thinking deterministic | No effect in thinking mode; use non-thinking mode or fixed `top_p` 0.95-1.0 |
| Dropping `reasoning_content` in tool loops | With `tools`, replay it fully in every request or you get a 400 |
| `tool_choice: "required"` or named tool in thinking mode | 400 error; disable thinking first |
| JSON mode without instructing JSON in the prompt | Add the instruction + schema; handle empty (spaces-only) content |
| Sending images in `assistant` messages | 400 error; images only in user/system/tool messages |
| Small `max_tokens` in thinking mode | Defaults are 64K (128K at max effort); reasoning consumes output tokens |
| Using retired IDs (`deepseek-chat`, `deepseek-v4-flash`, `-vision-exp`) in new code | Use `deepseek-flash`; old IDs still route but are retired |
