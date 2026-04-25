# Nano Banana - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `Nano Banana` image family |
| **Provider** | Google |
| **Source** | [Gemini image generation guide](https://ai.google.dev/gemini-api/docs/image-generation), [Nano Banana prompting guide](https://cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-nano-banana?hl=en), [Gemini 3 guide](https://ai.google.dev/gemini-api/docs/gemini-3), [Prompting strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) |
| **Last reviewed** | 2026-04 |

---

## What Nano Banana Refers To

- `Nano Banana` maps to `gemini-2.5-flash-image`.
- `Nano Banana 2` maps to `gemini-3.1-flash-image-preview`.
- `Nano Banana Pro` maps to `gemini-3-pro-image-preview`.
- The label refers to Google's native image-generation and image-editing capabilities inside the Gemini family, not to a single standalone text model.

---

## Key Characteristics

- Supports text-to-image generation and text-plus-image editing workflows.
- Optimized for iterative, conversational editing rather than one-shot prompting only.
- Supports grounded generation with Google Search, and for `gemini-3.1-flash-image-preview` also Google Image Search grounding.
- Supports higher-fidelity text rendering, multiple aspect ratios, multiple reference images, and up to 4K output on newer image models.

---

## Official Prompting Guidance

### 1. Describe the scene, not just keywords

- Narrative, descriptive prompts work better than disconnected keyword lists.
- Specify subject, action, context, composition, and style.
- Start with a strong verb that reflects the primary image operation you want.

### 2. Be highly specific about visual intent

- Define lighting, camera angle, lens style, composition, and materials when those details matter.
- For branded or commercial work, specify typography, color treatment, product surface, and visual mood.
- Positive framing works better than mostly negative instructions.

### 3. Use different prompt patterns for generation versus editing

- For new generation, direct the model like a creative brief.
- For editing, state what changes and what must remain unchanged.
- For inpainting-style edits or preservation tasks, explicitly say which elements must stay exactly the same.

### 4. Use reference images deliberately

- Combine reference images when identity, product fidelity, or compositional control matters.
- Newer models can mix multiple reference images in one workflow.
- When merging sources, describe the relationship between references and the target scene explicitly.

### 5. Iterate conversationally for better outputs

- Multi-turn editing is the recommended workflow for refinement.
- Use follow-up prompts to adjust lighting, expression, text, layout, or style without rewriting the whole brief.
- Small, controlled edits tend to work better than full prompt rewrites once a good base image exists.

### 6. Use grounding for real-world or time-sensitive visuals

- Enable Google Search grounding when the image depends on current facts such as weather, news, or market data.
- For `gemini-3.1-flash-image-preview`, image-search grounding can add external visual context.
- When displaying grounded results, honor the required source-attribution behavior from the API metadata.

### 7. Preserve thought signatures in multi-turn image workflows

- Conversational editing relies on returned thought signatures to preserve composition and editing continuity.
- Missing required thought signatures can produce strict validation failures.
- If you use the official SDK chat/history flow, signature handling is usually automatic.

### 8. Match model choice to workload

- Use `Nano Banana` for fast, efficient, high-volume image tasks.
- Use `Nano Banana 2` for better grounding, richer controls, and broader creative workflows.
- Use `Nano Banana Pro` for highest-quality asset production, advanced text rendering, and more demanding art direction.

### 9. Control output settings intentionally

- Set aspect ratio and image size explicitly when layout matters.
- Use higher resolutions only when the extra detail is worth the latency and cost.
- For text-heavy or design-heavy outputs, prefer the more capable image models and specify the typography requirements directly.

---

## Prompt Template

```text
Goal:
Create or edit an image for <use case>.

Subject:
<main subject and important attributes>

Scene:
<environment, context, and action>

Composition:
<shot type, framing, camera angle, aspect ratio>

Style:
<visual style, lighting, materials, color treatment>

Constraints:
- Preserve <elements that must stay unchanged>
- Render the text "<exact text>" in <font/style>
- Use grounding only when real-world accuracy matters

Output:
<target resolution or asset type>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Prompting with loose keyword piles | Use a descriptive scene-level prompt |
| Asking for edits without stating what must stay fixed | Explicitly name preserved elements |
| Skipping iterative refinement | Use multi-turn editing once a promising image exists |
| Forgetting grounding for current facts | Turn on Google Search grounding for real-world visuals |
| Dropping thought signatures between turns | Preserve signatures exactly in replay/edit workflows |
