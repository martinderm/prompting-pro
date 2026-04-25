# General Prompting Tips

Tips in this file are **model-agnostic** — they improve prompts regardless of which LLM you are targeting.

---

## Clarity & Structure

Sources: [1], [7]

### Use XML-style tags for long prompts

Wrapping sections in `<context>`, `<task>`, and `<format>` tags makes the prompt easier to scan for both humans and models.

```
<context>
You are a customer support agent for Acme Corp.
</context>

<task>
Summarise the following complaint in one sentence.
</task>

<format>
Plain sentence, no bullet points.
</format>
```

### Lead with the task, not the background

Models pay more attention to content at the beginning and end of a prompt. Put the core instruction early.

> ❌ "Here is some background… (500 words) … now please summarise."
> ✅ "Summarise the following text in 3 bullet points.\n\n<text>…</text>"

### Use positive instructions, not just prohibitions

Tell the model what you *want* it to do, not only what to avoid.

> ❌ "Don't use technical jargon."
> ✅ "Use plain language suitable for a non-technical audience. Avoid acronyms."

---

## Few-Shot Examples

Sources: [2]

### Match example format to desired output format

If you want JSON output, your few-shot examples should also be JSON.

### Use boundary examples

Include at least one easy case and one edge case in your few-shot set to teach the model the full range of expected behaviour.

### Keep examples consistent

All examples should follow the same template; inconsistent examples confuse the model more than no examples at all.

---

## Context Management

Sources: [1], [3], [7]

### Summarise long conversations periodically

When a multi-turn conversation grows long, inject a "conversation summary so far" message to refresh the model's working context.

### Put the most important instructions last in long prompts

Recency bias means models weight recent content more heavily. Restate key constraints just before the final instruction.

### Remove irrelevant context

Every token of irrelevant context competes with the relevant parts. Trim aggressively.

### Define stop rules for multi-step tasks

State when the model should stop iterating, ask a clarifying question, or provide a fallback answer.

---

## Output Control

Sources: [1], [5]

### Use a "format header" at the top of the system message

```
Always respond with valid JSON matching this schema: { ... }
```

### Ask for confidence or uncertainty

```
After your answer, rate your confidence from 1–5 and explain any uncertainty.
```

### Request self-review

```
Review your answer for errors or omissions, then provide a final corrected version.
```

### Set explicit verbosity and length

For production answers, define target length and formatting density up front (for example: concise paragraphs, no extra sections).

---

## Cost & Latency

Sources: [5], [7]

### Shorten prompts for high-volume applications

Every saved token compounds at scale. Use abbreviations in internal pipelines where readability for humans is not required.

### Cache stable system prompts

Many providers support prompt caching for system messages that do not change between calls. Use it for long system prompts.

### Use a smaller model for triage

Route simple requests to a smaller/cheaper model; escalate to a larger model only when complexity warrants it.

---

## Safety & Reliability

Sources: [4], [5], [7]

### Anchor the model's persona with explicit constraints

```
You are a financial assistant. You do not provide specific investment advice. If asked, redirect to a licensed advisor.
```

### Test adversarial inputs

Always test your prompt against inputs designed to make the model break its instructions (prompt injection, edge cases, off-topic requests).

### Use structured output validation

When expecting JSON or a specific schema, validate the response programmatically and retry with an error message on failure.

### Add retrieval budgets for grounded responses

Define when additional retrieval is justified and when current evidence is sufficient to answer.

---

Community source index: [knowledge/sources/openai.md](../knowledge/sources/openai.md#community-sources)
