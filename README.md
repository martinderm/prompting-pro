# prompting-pro

An agent skill that helps formulate high-quality prompts for specific AI models, drawing on official documentation and curated community tips.

## Quick Start

See [SKILL.md](SKILL.md) for usage instructions and a list of supported models.

## Repository Layout

```
SKILL.md            ← main skill definition (compact)
docs/               ← official prompt-guidance per model/version
  openai/
    gpt-5.5.md       ← GPT-5.5 official guidance
    gpt-5.4.md       ← GPT-5.4 official guidance
    gpt-5.3-codex.md ← GPT-5.3-Codex official guidance
  google/
    gemini-3.md      ← Gemini 3 family official guidance
    nano-banana.md   ← Nano Banana official guidance
knowledge/          ← central registry of documentation sources (self-learning)
  sources.md        ← all tracked official docs with status & last-checked date
  sources/          ← per-scope registries (openai, google, general)
tips/               ← unofficial / community tips
  general.md        ← model-agnostic tips
  openai/
    gpt-5.5.md       ← GPT-5.5 community tips
    gpt-5.4.md       ← GPT-5.4 family community tips (incl. mini/nano notes)
    gpt-5.3-codex.md ← GPT-5.3-Codex community tips
  google/
    gemini-3.md      ← Gemini 3 family & 3.8 Flash community tips (incl. Sensible Defaults)
    nano-banana.md   ← Nano Banana community tips
```

## Contributing

- **New model docs**: add a file to `docs/<provider>/<model>.md` and register its source in `knowledge/sources/<provider>.md` (plus `knowledge/sources.md` index for new providers).
- **Tips**: add to the appropriate file in `tips/`, following the guide in [tips/README.md](tips/README.md).
- **Knowledge updates**: when official docs change, update `knowledge/sources/<provider>.md` and the corresponding `docs/` file.

## Related Projects

- **[LLM-Sensible-Default-Instructions](https://github.com/martinderm/LLM-Sensible-Default-Instructions)**: Ready-to-use custom instructions for everyday chat applications (ChatGPT, Gemini Saved Info, Claude Projects), optimized for UI limits (< 1,500 chars), anti-sycophancy, and epistemic honesty.

## License

[MIT](LICENSE)
