# Tips — How They Are Organised

The `tips/` directory collects **unofficial** prompting tips: community best-practices, experimental techniques, and model-specific tricks that are not part of any provider's official documentation.

## Structure

```
tips/
├── README.md            ← this file
├── general.md           ← tips that work well across all models
└── openai/
    ├── gpt-5.5.md       ← GPT-5.5-specific tips
    ├── gpt-5.4.md       ← GPT-5.4-specific tips (incl. mini/nano notes)
    └── gpt-5.3-codex.md ← GPT-5.3-Codex-specific tips
```

Add a new `<provider>/` sub-directory when tips for a different provider are contributed.

## Tip Categories

| Category | Where to put it |
|----------|----------------|
| Applies to all models | `tips/general.md` |
| Specific to one model / version | `tips/<provider>/<model>.md` |
| Specific to one provider but all their models | `tips/<provider>/general.md` |

## Contributing a Tip

1. Pick the right file (or create one using the naming convention above).
2. Add the tip under the most relevant section heading.
3. Include:
   - **What**: a short, actionable description.
   - **Why**: the intuition or evidence behind it.
   - **Example** (optional but encouraged): a before/after prompt snippet.
4. If the tip has a public source (blog post, paper, tweet), add it as a footnote link.
5. Open a pull request; tips are lightly reviewed for accuracy and clarity.

## Principles

- Tips are **community knowledge** — they may or may not work for every use-case.
- If a tip is later validated by official documentation, move it to `docs/` and remove it from `tips/`.
- Label tips that are known to be model-version-specific (e.g. "Tested on gpt-5.4-2026-03-05 only").
- Keep mini/nano notes under their parent family tip file unless a variant has materially different behavior.
