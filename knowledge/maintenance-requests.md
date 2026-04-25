# Self-Learning Maintenance Requests

Use these request patterns when you want the skill to update its knowledge base on demand:

- `Check <provider> for new models or prompt-guidance updates.`
- `Refresh all outdated sources for <provider>.`
- `Compare the registered sources with the current provider docs.`
- `Add a newly discovered official model to knowledge and docs.`
- `Evaluate a new blog post as a community tip and wire it into tips/ and knowledge/.`

## Expected workflow

1. Revisit the relevant URLs in `knowledge/sources/<provider>.md`.
2. Identify new models, changed guidance, or newly relevant community sources.
3. Classify findings as official or community.
4. Update the matching files in `knowledge/`, `docs/`, and `tips/`.
5. Keep source registries, model tables, and file references consistent.

## Adding a New Model

When a new model is discovered during maintenance:

1. Add a reference doc in `docs/<provider>/<model>.md` (official guidance only).
2. Optionally add tips in `tips/<provider>/<model>.md` (unofficial / community tips).
3. Register the official documentation source in `knowledge/sources/<provider>.md`.
4. Update `knowledge/sources.md` only if this introduces a new provider.
5. Add the model row to the Supported Models table in `skill.md`.
