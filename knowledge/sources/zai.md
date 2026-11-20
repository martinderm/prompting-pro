# Z.ai (GLM) Documentation Sources

This file tracks official and community sources used by prompting-pro.

## Format

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|

## Official Sources

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|
| Z.ai | GLM-5.3 model guide (flagship, text-only, 1M ctx, always-on reasoning, endpoints, quick start) | <https://docs.z.ai/guides/llm/glm-5.3> | 2026-11 | 2026-11 | active |
| Z.ai | GLM-5.3-Flash/FlashX guide (native multimodal, recommended settings, vision best practices) | <https://docs.z.ai/guides/vlm/glm-5.3-flash> | 2026-11 | 2026-11 | active |
| Z.ai | Chat Completion API reference (`thinking`, `reasoning_effort`, `clear_thinking`, `temperature`, tools, `response_format`) | <https://docs.z.ai/api-reference/llm/chat-completion> | 2026-11 | 2026-11 | active |
| Z.ai | Deep Thinking (reasoning effort levels, response-time impact) | <https://docs.z.ai/guides/capabilities/thinking> | 2026-11 | 2026-11 | active |
| Z.ai | Context Caching (automatic caching, stable-prefix guidance) | <https://docs.z.ai/guides/capabilities/cache> | 2026-11 | 2026-11 | active |
| Z.ai | Release notes (model releases and updates) | <https://docs.z.ai/release-notes/new-released> | 2026-11 | 2026-11 | active |
| Z.ai | Documentation index (llms.txt) | <https://docs.z.ai/llms.txt> | 2026-11 | 2026-11 | active |
| Z.ai | Hugging Face model card GLM-5.3 (weights BF16/FP8, GLM-5.3 License, eval sampling params) | <https://huggingface.co/zai-org/GLM-5.3> | 2026-11 | 2026-11 | active |
| Z.ai | Hugging Face model card GLM-5.3-Flash (MIT weights, native FP8, serving frameworks) | <https://huggingface.co/zai-org/GLM-5.3-Flash> | 2026-11 | 2026-11 | active |
| Z.ai | GLM-5 code repository (Apache-2.0, architecture and inference cookbooks) | <https://github.com/zai-org/GLM-5> | 2026-11 | 2026-11 | active |
| Mistral AI | Third-party hosting on La Plateforme: `zai-glm-5-3` / `zai-glm-5-3-flash` (models overview, reasoning_effort behavior) | <https://docs.mistral.ai/models> | 2026-11 | 2026-11 | active |
| Mistral AI | Reasoning page (zai-glm-5-3 supports low/high/max, not none; content always a chunk list) | <https://docs.mistral.ai/inference/conversations/reasoning> | 2026-11 | 2026-11 | active |

## Community Sources

Use these compact references when citing community input in docs and tips.

| Ref | Source | URL | First added | Last checked | Status |
|-----|--------|-----|-------------|--------------|--------|
| [1] | Prompt Engineering Guide (community curation; shared with the OpenAI and Mistral registries) | <https://www.promptingguide.ai/> | 2026-11 | 2026-11 | active |

## Notes

- **Status** values: `active` (content current), `outdated` (needs review), `archived` (model deprecated).
- A source is considered **outdated** if it has not been checked within 90 days or if Z.ai has published a newer version.
- Z.ai publishes no dedicated GLM prompting guide; prompt-relevant guidance lives in the model guides and the Chat Completion API reference listed above.
- License note for self-hosting: GLM-5.3 weights use the custom GLM-5.3 License; GLM-5.3-Flash weights are MIT. Check the license file before redistributing weights.
- `zai-glm-5-3` / `zai-glm-5-3-flash` on Mistral La Plateforme are the same models hosted third-party; cross-reference [mistral.md](mistral.md). On La Plateforme, `zai-glm-5-3` supports `reasoning_effort` low/high/max (not `none`) and always returns `message.content` as a chunk list (thinking + text).
- Deprecated predecessor: `zai-glm-5-2` on La Plateforme (deprecated, retires 2026-10-31; alternative `zai-glm-5-3`).
