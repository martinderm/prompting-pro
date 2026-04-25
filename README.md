# prompting-pro

An agent skill that helps formulate high-quality prompts for specific AI models, drawing on official documentation and curated community tips.

## Quick Start

See [skill.md](skill.md) for usage instructions and a list of supported models.

## Repository Layout

```
skill.md            ← main skill definition (compact)
docs/               ← official prompt-guidance per model/version
  openai/
    gpt-4o.md       ← GPT-4o official guidance
    gpt-4.md        ← GPT-4 official guidance
    o1.md           ← o1 / o1-mini official guidance
knowledge/          ← central registry of documentation sources (self-learning)
  sources.md        ← all tracked official docs with status & last-checked date
tips/               ← unofficial / community tips
  general.md        ← model-agnostic tips
  openai/
    gpt-4o.md       ← GPT-4o community tips
    o1.md           ← o1-series community tips
```

## Contributing

- **New model docs**: add a file to `docs/<provider>/<model>.md` and register its source in `knowledge/sources.md`.
- **Tips**: add to the appropriate file in `tips/`, following the guide in [tips/README.md](tips/README.md).
- **Knowledge updates**: when official docs change, update `knowledge/sources.md` and the corresponding `docs/` file.

## License

[MIT](LICENSE)
