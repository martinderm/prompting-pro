# Knowledge Base — How It Works

The `knowledge/` directory is the **central repository of documentation sources** for prompting-pro.  
Its purpose is to make the skill *self-learning*: as official documentation is updated or new models are released, contributors record the change here so that model reference docs (`docs/`) and tips (`tips/`) can be kept in sync.

## Files

| File | Purpose |
|------|---------|
| [sources.md](sources.md) | Registry of all official documentation sources tracked by this skill |

## Workflow

### Adding a new documentation source

1. Add a row to [sources.md](sources.md) with:
   - Provider, model/scope, URL, date first added, status (`active` / `outdated` / `archived`).
2. Create or update the corresponding file in `docs/<provider>/<model>.md`.
3. Open a pull request — the PR description should quote the key changes in the source.

### Updating an existing source

1. Visit the URL in [sources.md](sources.md) and note what changed.
2. Update the `Last checked` date and status in [sources.md](sources.md).
3. Update the corresponding `docs/` file.
4. If the change is significant, add a `> ⚠️ Changed in <date>: <summary>` callout at the top of the docs file.

### Marking a source as outdated

Set the status column to `outdated` and add a note.  
A maintainer should then update or archive the corresponding docs file.

## Principles

- Only **official** provider documentation goes in `sources.md` and `docs/`.
- Community tips, blog posts, and experimental techniques go in `tips/` instead.
- Keep `sources.md` as the single source of truth for which documentation is currently trusted and current.
