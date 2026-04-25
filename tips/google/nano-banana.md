# Nano Banana - Unofficial Tips

Community tips for `Nano Banana`, `Nano Banana 2`, and `Nano Banana Pro` based on Google's product-blog guidance.

---

## Vision Framing

Sources: Google blog - Nano Banana Pro prompting tips

Grounding:

- The blog recommends specifying subject, composition, action, location, style, and direct editing instructions.
- This strengthens creative control beyond short keyword prompts.

### Establish story, subject, and style explicitly

Start prompts with a concrete visual brief: who or what is in the scene, what is happening, where it happens, how it is framed, and what style the result should evoke.

### For edits, state the change directly

When modifying an existing image, name the exact change in plain language instead of embedding it inside a larger descriptive paragraph.

---

## Cinematic Control

Sources: Google blog - Nano Banana Pro prompting tips

Grounding:

- The blog recommends explicit aspect ratio, camera, lighting, text-in-image styling, factual constraints, and reference-image role assignment.
- These are framed as the jump from simple prompts to professional results.

### Direct camera, lighting, and format like a photographer

Specify framing, aspect ratio, camera perspective, depth of field, lighting setup, and color grade when you need predictable art direction.

### Tell the model exactly how text should appear

If text must render inside the image, specify the exact words plus placement, font feel, and visual treatment.

### Assign a role to each reference image

When using multiple inputs, say what each image contributes, for example pose, style, background, texture, or product identity.

---

## Production Use Cases

Sources: Google blog - Nano Banana Pro prompting tips

Grounding:

- The blog highlights text rendering, real-world knowledge, localization, studio-quality edits, resizing, blending, character consistency, and brand look-and-feel.
- These are presented as practical prompting techniques rather than abstract theory.

### Use Nano Banana Pro for text-heavy and brand-heavy work

When you need posters, packaging, diagrams, or mockups with readable text and controlled styling, write the prompt as a design brief rather than a generic image request.

### Use grounded generation for data-backed visuals

For diagrams, infographics, or visuals tied to real-world facts, treat factual accuracy as a prompt requirement and verify the inputs before generation.

### Use conversational iteration for polish

After the first pass, refine specific properties such as time of day, lighting, consistency, localization, or brand treatment in follow-up turns instead of rewriting from scratch.

---

## Known Limits

Sources: Google blog - Nano Banana Pro prompting tips

Grounding:

- The blog explicitly warns about limitations in visual/text fidelity, factual accuracy, localization nuance, complex edits, image blending, and character consistency.
- These limitations should shape prompt expectations and verification steps.

### Verify small text and factual diagrams manually

Do not assume that tiny text, spellings, or data-heavy visuals are correct on the first render.

### Expect artifacts in complex blends and lighting edits

Large compositing or relighting changes can still produce unnatural results, so plan for iterative cleanup.

### Treat localization as draft-quality until reviewed

Multilingual text rendering is useful, but grammar and cultural nuance still need human review.

---

Community source index: [knowledge/sources/google.md](../../knowledge/sources/google.md)
