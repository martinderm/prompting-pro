# GPT-5.5 - Unofficial Tips

Community tips for `gpt-5.5` in coding and professional workflows.

---

## Prompt Design

### Define done conditions first

`gpt-5.5` performs best when the prompt starts with an explicit definition of done (tests passing, schema valid, policy constraints met).

### Use compact constraint blocks

Prefer a short `Constraints` block over long narrative instructions. This improves consistency in agentic multi-step tasks.

### Ask for progress checkpoints on long tasks

For long-running jobs, ask for milestone updates (diagnosis, implementation, verification) before final output.

---

## Reasoning Effort Heuristics

| Effort | Typical use |
|--------|-------------|
| `low` | quick transformations, straightforward edits |
| `medium` | default for coding and review tasks |
| `high` | complex debugging and risky migrations |
| `xhigh` | deep audits, multi-component design tradeoffs |

Tip: Start at `medium`; increase only when your eval set shows clear gains.

---

## Tooling Patterns

### Prefer strict tool schemas

When using function/tool calls, strict schemas reduce invalid calls and improve repair loops.

### Include error payloads verbatim in retries

If a tool call fails validation, pass the exact error in the next turn and request a corrected output only.

---

## Known Quirks

- Can become verbose without explicit output-length constraints.
- Overly detailed meta-instructions can reduce practical execution quality; keep directives concrete and minimal.
