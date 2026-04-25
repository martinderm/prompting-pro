# GPT-5.5 - Unofficial Tips

Community tips for `gpt-5.5` in coding and professional workflows.

---

## Prompt Design

Sources: [1], [2], [7]

Grounding:

- [1]: Strongly supports explicit task framing, constraints, and clear completion criteria.
- [2]: Few-shot consistency informs the recommendation to keep instruction blocks compact and regular.
- [7]: Practitioner observations support milestone check-ins for long-running workflows.

### Define done conditions first

`gpt-5.5` performs best when the prompt starts with an explicit definition of done (tests passing, schema valid, policy constraints met).

### Use compact constraint blocks

Prefer a short `Constraints` block over long narrative instructions. This improves consistency in agentic multi-step tasks.

### Ask for progress checkpoints on long tasks

For long-running jobs, ask for milestone updates (diagnosis, implementation, verification) before final output.

### Separate personality from task rules

Keep a short personality block for tone and a separate collaboration block for behavior (questions vs assumptions, proactivity, uncertainty handling).

---

## Reasoning Effort Heuristics

Sources: [7]

Grounding:

- [7]: Practitioner discussions describe effort-tier routing as an operational heuristic, not a formal standard.
- Change applied: Keep this table as a starting heuristic for eval-driven tuning, not as normative guidance.

| Effort | Typical use |
|--------|-------------|
| `low` | quick transformations, straightforward edits |
| `medium` | default for coding and review tasks |
| `high` | complex debugging and risky migrations |
| `xhigh` | deep audits, multi-component design tradeoffs |

Tip: Start at `medium`; adjust only when evaluations show clear gains.

---

## Tooling Patterns

Sources: [3], [4], [5], [7]

Grounding:

- [3]: ReAct-style loops motivate explicit step control and bounded retrieval decisions.
- [4]: Function-calling production patterns support strict schemas and explicit retry context.
- [5]: Product patterns reinforce controlled tool orchestration and observable execution states.
- [7]: Practitioner usage supports short preambles in tool-heavy user experiences.

### Prefer strict tool schemas

When using function/tool calls, strict schemas reduce invalid calls and improve repair loops.

### Include error payloads verbatim in retries

If a tool call fails validation, pass the exact error in the next turn and request a corrected output only.

### Add a retrieval budget for grounded tasks

Define when another search is allowed and when to stop and answer. This reduces endless retrieval loops.

### Use short preambles in tool-heavy workflows

In streaming UX, ask for a one- to two-sentence status preamble before tool calls.

---

## Shared Coding Overlay

For coding tasks with GPT-5.5, also apply: [codex.md](codex.md).

---

## Known Quirks

Sources: [7]

Grounding:

- [7]: Captures recurring field reports on verbosity drift and over-specified meta-instructions.

- Can become verbose without explicit output-length constraints.
- Overly detailed meta-instructions can reduce practical execution quality; keep directives concrete and minimal.

---

Community source index: [knowledge/sources/openai.md](../../knowledge/sources/openai.md#community-sources)
