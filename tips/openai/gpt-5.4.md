# GPT-5.4 Family - Unofficial Tips

Community tips for `gpt-5.4` with practical notes for `gpt-5.4-mini` and `gpt-5.4-nano`.

---

## Model Selection Within Family

Sources: [1], [7]

Grounding:

- [1]: Supports matching prompt complexity and instruction strictness to task demands.
- [7]: Practitioner comparisons motivate tiered routing across larger and smaller variants.
- Change applied: Position routing matrix as practical guidance, validated by local evals.

| Variant | Good fit | Escalate when |
|---------|----------|---------------|
| `gpt-5.4` | feature work, robust reasoning, medium/high complexity coding | task becomes mission-critical or very deep reasoning -> try `gpt-5.5` |
| `gpt-5.4-mini` | triage, routing, extraction, test generation, subagent steps | repeated logical errors or weak synthesis |
| `gpt-5.4-nano` | very high-volume lightweight classification/transforms | nuanced reasoning is required |

---

## Prompting Patterns

Sources: [2], [3]

Grounding:

- [2]: Few-shot technique supports strict output contracts and format-consistent examples.
- [3]: ReAct decomposition supports two-pass workflows for analysis then synthesis.

### Keep one explicit output contract

Short variants benefit from strict contracts: exact schema, required fields, and allowed values.

### Split heavy tasks into two passes

Use `gpt-5.4-mini` for first-pass analysis (inventory, ranking, candidate options), then `gpt-5.4` for final synthesis.

### Add deterministic acceptance checks

Include checks such as "must compile", "must preserve API", or "must keep output valid JSON".

---

## Cost and Latency

Sources: [5], [7]

Grounding:

- [5]: Highlights cost-performance tradeoffs, preprocessing stages, and selective escalation.
- [7]: Reinforces aggressive context trimming and throughput-aware model routing.

- Keep stable instructions reusable and concise.
- Remove irrelevant context aggressively before calls.
- Use mini for high-frequency preprocessing and escalate selectively.

---

## Shared Coding Overlay

For coding tasks with the GPT-5.4 family, also apply: [codex.md](codex.md).

---

Community source index: [knowledge/sources/openai.md](../../knowledge/sources/openai.md#community-sources)
