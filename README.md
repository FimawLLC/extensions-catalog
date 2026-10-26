# idexal Os Extensions Catalog

The official, open catalog of extensions for **idexal Os**. Every entry here can
be installed in one click from the in-app marketplace and is delivered to every
desktop in an organization.

An *extension* is one of three kinds:

| Type | Directory | What it is |
| --- | --- | --- |
| **Connector** | `connectors/` | A hosted or self-managed MCP endpoint (GitHub, Vercel, Notion, …). |
| **Skill** | `skills/` | A reusable `SKILL.md` instruction set an agent can follow. |
| **Plugin** | `plugins/` | A bundle that installs one or more skills and connectors together. |

## Repository layout

```
catalog.json            Canonical machine-readable catalog (source of truth)
connectors/<slug>.json  One connector per file
skills/<slug>.md        One skill per file (SKILL.md format)
plugins/<slug>.json     One plugin per file
```

The canonical `catalog.json` is generated from the per-type files and is what
the marketplace serves. The per-type directories exist so contributions are
small, reviewable, and diff-friendly.

## Adding an extension

1. Create a file in the matching directory named `<slug>.json` (or `.md` for
   skills). The slug is lowercase, hyphen-separated, and stable — it becomes the
   public id desktops subscribe to.
2. Fill in the required fields for that type (see below).
3. Open a pull request. Once merged, the extension appears in the marketplace
   on the next catalog refresh.

### Connector

```json
{
  "slug": "example-mcp",
  "type": "connector",
  "name": "Example",
  "description": "What the connector exposes, in one sentence.",
  "version": "1.0.0",
  "source": "https://github.com/owner/example-mcp",
  "url": "https://mcp.example.com/mcp",
  "authType": "oauth",
  "tags": ["mcp"]
}
```

`authType` is one of `oauth`, `apikey`, or `none`. `url` must be an `https://`
MCP endpoint.

### Skill

A skill is a Markdown file with YAML front matter:

```markdown
---
name: Example Skill
description: A one-line description shown in the marketplace.
---

# Example Skill

Instructions the agent follows, in the imperative voice.
```

### Plugin

```json
{
  "slug": "example-starter-pack",
  "type": "plugin",
  "name": "Example Starter Pack",
  "description": "A bundle of skills and connectors.",
  "version": "1.0.0",
  "source": "https://github.com/owner/example-pack",
  "includes": ["example-skill", "example-mcp"],
  "tags": ["starter"]
}
```

## Conventions

- **Write numbers with Western digits** (`123456789`), never Arabic-Indic
  numerals, in every language.
- Descriptions are one sentence, customer-facing, and free of internal links.
- Do not reference private or internal infrastructure.

## Documentation

The catalog contract — entry schema, auth shapes, versioning and review — is
documented in [`docs/`](./docs/README.md):

| Document | Covers |
| --- | --- |
| [Entry Schema](./docs/entry-schema.md) | Required and optional fields for each type |
| [Submitting Entries](./docs/submitting-entries.md) | How to add a connector, skill or plugin |
| [Connector Auth](./docs/connector-auth.md) | `authType` values and the HTTPS endpoint rule |
| [Versioning and Deprecation](./docs/versioning-and-deprecation.md) | Changing an entry without breaking installs |
| [Review Checklist](./docs/review-checklist.md) | What a reviewer checks, in order |
| [FAQ](./docs/faq.md) | The questions we are asked most |

## License

Catalog metadata is released under the MIT License. Each third-party connector
remains governed by its own provider's terms.
