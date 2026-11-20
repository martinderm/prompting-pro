# Mistral AI Documentation Sources

This file tracks official and community sources used by prompting-pro.

## Format

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|

## Official Sources

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|
| Mistral AI | Models overview & deprecation table (current lineup incl. Large 4, Small 4, Ministral 3, Codestral, OCR 4.1) | <https://docs.mistral.ai/models> | 2026-11 | 2026-11 | active |
| Mistral AI | Model selection guide (compare models, pricing, features, licensing) | <https://docs.mistral.ai/models/model-selection-guide> | 2026-11 | 2026-11 | active |
| Mistral AI | Mistral Large 4 model card (`mistral-large-4`, `mistral-large-4-0`, v26.10, 1M context, multimodal MoE) | <https://docs.mistral.ai/models/mistral-large-4-0> | 2026-11 | 2026-11 | active |
| Mistral AI | Mistral Small 4 model card (`mistral-small-2603`, v26.03, hybrid instruct/reasoning/coding, 256k, Apache 2.0) | <https://docs.mistral.ai/models/model-cards/mistral-small-4-0-26-03> | 2026-11 | 2026-11 | active |
| Mistral AI | Codestral model card (`codestral-2508` / `codestral-latest`, v25.08, FIM + code generation, 128k) | <https://docs.mistral.ai/models/codestral-25-08> | 2026-11 | 2026-11 | active |
| Mistral AI | Prompting guide (system vs. user prompt, structure, few-shot, what to avoid) | <https://docs.mistral.ai/guides/prompting_capabilities> | 2026-11 | 2026-11 | active |
| Mistral AI | Sampling parameters (temperature, top_p, n, penalties) | <https://docs.mistral.ai/guides/sampling> | 2026-11 | 2026-11 | active |
| Mistral AI | Chat completions (message roles, prompt_cache_key) | <https://docs.mistral.ai/inference/conversations/chat-completion> | 2026-11 | 2026-11 | active |
| Mistral AI | Reasoning (`reasoning_effort`, ThinkChunk/TextChunk, multi-turn replay) | <https://docs.mistral.ai/inference/conversations/reasoning> | 2026-11 | 2026-11 | active |
| Mistral AI | Function calling (tools as JSON schema, tool_choice, parallel_tool_calls) | <https://docs.mistral.ai/inference/conversations/function-calling> | 2026-11 | 2026-11 | active |
| Mistral AI | Structured outputs (JSON mode vs. custom json_schema) | <https://docs.mistral.ai/capabilities/structured_output> | 2026-11 | 2026-11 | active |
| Mistral AI | Vision (image_url content parts, recommended vision models) | <https://docs.mistral.ai/capabilities/vision> | 2026-11 | 2026-11 | active |
| Mistral AI | Document AI / OCR (`/v1/ocr`: OCR Processor, Annotations, Document QnA) | <https://docs.mistral.ai/capabilities/document_ai> | 2026-11 | 2026-11 | active |
| Mistral AI | Prompt caching (`prompt_cache_key`, cached tokens at 10% of input price) | <https://docs.mistral.ai/inference/conversations/advanced/prompt-caching> | 2026-11 | 2026-11 | active |
| Mistral AI | Predicted outputs | <https://docs.mistral.ai/inference/conversations/advanced/predicted-outputs> | 2026-11 | 2026-11 | active |
| Mistral AI | Chat API endpoint reference (temperature 0.0-0.7 recommended, prompt+max_tokens <= context) | <https://docs.mistral.ai/api/endpoint/chat> | 2026-11 | 2026-11 | active |
| Mistral AI | FIM API endpoint reference (`/v1/fim/completions`, prefix/suffix) | <https://docs.mistral.ai/api/endpoint/fim> | 2026-11 | 2026-11 | active |
| Mistral AI | Vibe Code (coding agent: CLI, VS Code, web, desktop) | <https://docs.mistral.ai/vibe/code/overview> | 2026-11 | 2026-11 | active |
| Mistral AI | Changelog (releases, deprecations, retirements) | <https://docs.mistral.ai/resources/changelogs> | 2026-11 | 2026-11 | active |
| Mistral AI | Cookbook: prompting capabilities (classification, summarization, personalization, evaluation) | <https://docs.mistral.ai/resources/cookbooks/mistral-prompting-prompting_capabilities> | 2026-11 | 2026-11 | active |
| Mistral AI | Launch post: Mistral Large 4 | <https://mistral.ai/news/mistral-large-4/> | 2026-11 | 2026-11 | active |
| Mistral AI | Launch post: Codestral 25.08 and the Mistral coding stack | <https://mistral.ai/news/codestral-25-08/> | 2026-11 | 2026-11 | active |

## Community Sources

Use these compact references when citing community input in docs and tips.

| Ref | Source | URL | First added | Last checked | Status |
|-----|--------|-----|-------------|--------------|--------|
| [1] | Prompt Engineering Guide (community curation; shared with the OpenAI registry) | <https://www.promptingguide.ai/> | 2026-11 | 2026-11 | active |
| [2] | Hugging Face model card: Mistral-Small-4-119B-2603 (open weights, self-hosting details) | <https://huggingface.co/mistralai/Mistral-Small-4-119B-2603> | 2026-11 | 2026-11 | active |

## Notes

- **Status** values: `active` (content current), `outdated` (needs review), `archived` (model deprecated).
- A source is considered **outdated** if it has not been checked within 90 days or if Mistral has published a newer version.
- Other current families not yet covered by dedicated `docs/` files (OCR 4.1 `mistral-ocr-4-1`, Voxtral 3 audio family, Mistral Embed, Codestral Embed, Mistral Moderation 2 / Shieldstral 1.0, Timestral) are tracked via the [models overview](https://docs.mistral.ai/models).
- Third-party models hosted on La Plateforme (`zai-glm-5-3`, `zai-glm-5-3-flash`, DeepSeek V4.1 Flash) are developed by their own vendors; the Z.ai GLM models are tracked in [zai.md](zai.md).
- Deprecated lines to watch during maintenance: `mistral-medium-3-5` (retires 2027-04, alternative Large 4), `mistral-large-2512` (retires 2027-04, alternative Large 4), `devstral-2512` (retires 2027-07, alternative Medium 3.5), Magistral and Pixtral (retired; alternatives Small 4 / Medium 3.5 / Ministral 3 14B). See the deprecation table on the [models overview](https://docs.mistral.ai/models).
