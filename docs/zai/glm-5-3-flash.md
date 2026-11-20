# GLM-5.3-Flash - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `glm-5.3-flash` (faster variant `glm-5.3-flashx`, ~200 tok/s) |
| **Provider** | Z.ai |
| **Source** | [GLM-5.3-Flash/FlashX guide](https://docs.z.ai/guides/vlm/glm-5.3-flash), [Chat Completion API reference](https://docs.z.ai/api-reference/llm/chat-completion), [GLM-5.3 guide](https://docs.z.ai/guides/llm/glm-5.3), [Hugging Face model card](https://huggingface.co/zai-org/GLM-5.3-Flash) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- First natively multimodal model in the GLM-5 series (released 2026-08-26), built on a new base trained on a ~30T-token multimodal corpus - unlike GLM-5.3, which reuses the GLM-5.2 base.
- 320B total / 18B active MoE with 45 layers; hybrid sparse + linear attention cuts attention compute and KV cache ~3.0x / ~4.4x versus GLM-5.3, enabling the low price at 1M context.
- Input: text, images, video, files; output: text. 1M-token context window; max output 128K tokens.
- Same reasoning controls as GLM-5.3: `thinking.type` only `enabled`; `reasoning_effort` low/high/max, default `max`.
- Recommended settings (Z.ai): `temperature: 1`, `top_p: 0.95`, `reasoning_effort: "max"`, `thinking.clear_thinking: false`; for streaming enable `stream: true` together with `tool_stream: true`.
- Open weights under MIT (`zai-org/GLM-5.3-Flash`, native FP8). API pricing $0.15 input / $0.03 cached / $0.50 output per 1M tokens - roughly a tenth of GLM-5.3; 3x quota on the GLM Coding Plan. Also served on Mistral La Plateforme as `zai-glm-5-3-flash` (optimized for agentic workflows and visual coding).

---

## Family Positioning

- Use `glm-5.3-flash` as the default for general chat, high-volume, cost-sensitive, and any visual or agentic work; escalate to `glm-5.3` (see [glm-5-3.md](glm-5-3.md)) for the hardest text-only engineering tasks.
- `glm-5.3-flashx` (~200 tok/s) for latency-sensitive serving; `glm-5.3-flashx-legal` for legal-domain workflows.

---

## Official Prompting Guidance

Shared API-level guidance (reasoning effort, sampling, caching, function calling, structured outputs, multi-turn `clear_thinking`) is identical to GLM-5.3 - see [glm-5-3.md](glm-5-3.md#official-prompting-guidance). Flash specifics:

### 1. Send images as `image_url` content blocks

- Add `{"type": "image_url", "image_url": {"url": "<public URL>"}}` blocks to `messages[].content[]`. A public URL is recommended; use a base64 data URL for local or private images. Multiple images = multiple `image_url` blocks in the same message.

### 2. Vision-driven workflows: reference assets in, verified output out

- Z.ai's recommended pattern for visual tasks: provide screenshots or other reference assets, ask the model to analyze the structure first, build, then verify by rendering/testing against the references, iterate, and finally report what is verified vs. what remains unverified.
- Documented applications: UI reproduction from screenshots/URLs (frontend), office deliverables (PPTX/PDF/DOCX/XLSX) with render-and-inspect validation, financial research with source citations, video understanding/editing, 3D scenes (Blender), games (Godot), computer-use closed loops, CAD reproduction (e.g. build123d).

### 3. Keep prompts structured and ticket-like

- Goal, context with references, constraints, definition of done, verification steps. Ask for explicit assumptions when inputs are ambiguous (e.g. dimensions that cannot be determined from a blueprint).

### 4. Set `reasoning_effort` deliberately for interactive use

- Reasoning cannot be disabled, so choose the level: `low` for quick chat or extraction, `high`/`max` for complex visual-coding loops. Reasoning tokens are billed as output.

---

## Prompt Template

```text
[SYSTEM]
You are <role>.
Rules:
- <stable rule 1>
- <output format rule>

[USER]
# Goal
<outcome, e.g. "Recreate the provided UI as a Next.js + TypeScript app">

# References
<image_url blocks with screenshots or URLs; or files>

# Constraints
- <hard constraints, licensing, "do not fabricate data - cite sources">

# Definition of done
- Build, then render/test against the references, refine, deliver <artifacts>
- Report verified vs. unverified results and remaining discrepancies
```

Request shape: `model: "glm-5.3-flash"`, `thinking: {"type": "enabled", "clear_thinking": false}`, `temperature: 1`, `top_p: 0.95`, `reasoning_effort` per task class.

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Sending images to `glm-5.3` | Text-only; use `glm-5.3-flash` for image/video/file input |
| One-shot visual prompts without a verification loop | Ask for render/test - compare against references - refine iterations |
| Treating 18B active parameters as a small local model | 320B total parameters; plan serving/hardware accordingly |
| Leaving the default `max` effort on simple turns | Set `reasoning_effort` explicitly (`low` for chat/extraction) |
| Fabricated figures in document workflows | Require source citations and a verified/unverified separation |
