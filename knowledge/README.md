# Knowledge Base — How It Works

The `knowledge/` directory is the **central repository of documentation sources** for prompting-pro.  
Its purpose is to make the skill *self-learning*: as official documentation is updated or new models are released, contributors record the change here so that model reference docs (`docs/`) and tips (`tips/`) can be kept in sync.

In practice, "self-learning" here means **self-updating on request**: the skill can be asked to revisit registered sources, detect new models or changed guidance, classify findings as official or community, and propagate the changes into the right repository files.

## Files

| File | Purpose |
|------|---------|
| [sources.md](sources.md) | Compact index of provider source registries |
| [sources/openai.md](sources/openai.md) | Official and community OpenAI documentation sources |
| [sources/google.md](sources/google.md) | Official and community Google documentation sources |

## Workflow

### On-request discovery and refresh

When asked to check a provider for changes, use this workflow:

1. Revisit the URLs listed in `knowledge/sources/<provider>.md`.
2. Check whether new official model pages, new prompt-guidance pages, or new relevant community sources have appeared.
3. Determine whether each finding affects `docs/`, `tips/`, or only the source registry.
4. Update `Last checked`, status, and affected repository files.
5. If a newly discovered official model should be tracked, create a new `docs/<provider>/<model>.md` file and register it.
6. If a newly discovered community source adds actionable prompting advice, wire it into the relevant `tips/` file and keep the source registry in sync.

### Adding a new documentation source

1. Add or update the provider file at `knowledge/sources/<provider>.md` with:
   - Provider, model/scope, URL, date first added, status (`active` / `outdated` / `archived`).
   - Place official reference docs under an `Official Sources` section.
   - Place blog posts or other non-reference inputs used for `tips/` under a separate `Community Sources` section.
2. If this is a new provider, add one row in [sources.md](sources.md) pointing to that file.
3. Create or update the corresponding file in `docs/<provider>/<model>.md`.
4. Open a pull request — the PR description should quote the key changes in the source.

### Typical maintenance requests

- `Check OpenAI for new models.`
- `Refresh Google sources older than 90 days.`
- `Compare Nano Banana sources with current docs.`
- `Evaluate this blog post as a community tip.`
- `Create docs for a newly discovered official model.`

### Updating an existing source

1. Visit the URL in the relevant provider file under `knowledge/sources/` and note what changed.
2. Update the `Last checked` date and status in that provider file.
3. Update the corresponding `docs/` file for official-source changes, or the corresponding `tips/` file for community-source changes.
4. If the change is significant, add a `> ⚠️ Changed in <date>: <summary>` callout at the top of the affected docs file when appropriate.

### Marking a source as outdated

Set the status column in the provider file to `outdated` and add a note.  
A maintainer should then update or archive the corresponding docs file.

## Principles

- Provider source files in `knowledge/sources/<provider>.md` are the source registry of truth and may contain both `Official Sources` and `Community Sources` sections.
- Only **official** provider documentation should drive `docs/`.
- Community tips, blog posts, and experimental techniques should drive `tips/`, even when their URLs are tracked in `knowledge/sources/<provider>.md`.
- Discovery should be explicit and user-triggered; this repository does not assume background automation.
- Keep [sources.md](sources.md) as a compact index and provider files as the detailed source of truth.
