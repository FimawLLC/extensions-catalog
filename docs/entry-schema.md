# Entry Schema

Every catalog entry is a structured record. This page lists the fields, which are
required, and the rules a reviewer checks them against.

The repository layout is:

```text
catalog.json            Canonical machine-readable catalog (generated)
connectors/<slug>.json  One connector per file
skills/<slug>.md        One skill per file (SKILL.md format)
plugins/<slug>.json     One plugin per file
```

`catalog.json` is generated from the per-type files. Edit the per-type file, not
the generated catalog.

## Required fields (connector and plugin)

| Field | Type | Rules |
| --- | --- | --- |
| `slug` | string | Unique, lowercase, hyphen-separated. The stable public id |
| `type` | enum | `connector`, `skill` or `plugin` |
| `name` | string | Human readable; what a user sees |
| `description` | string | One sentence, customer-facing |
| `version` | semver | Bumped whenever the content changes |
| `source` | string | Where a consumer fetches the content |

## Connector-only fields

| Field | Type | Rules |
| --- | --- | --- |
| `url` | string | An `https://` MCP endpoint |
| `authType` | enum | `oauth`, `apikey` or `none` |

## Plugin-only fields

| Field | Type | Rules |
| --- | --- | --- |
| `includes` | string[] | Member slugs the plugin bundles; each must resolve |

## Optional fields

| Field | Type | Notes |
| --- | --- | --- |
| `tags` | string[] | Free-form discovery hints |

## Example: connector

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

## Example: plugin

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

## Example: skill

A skill is a Markdown file with YAML front matter, not JSON:

```markdown
---
name: Example Skill
description: A one-line description shown in the marketplace.
---

# Example Skill

Instructions the agent follows, in the imperative voice.
```

## Identity rules

1. **Slug is immutable.** The slug is the public id desktops subscribe to.
   Renaming it is publishing a new entry, never editing an existing one.
2. **Version is monotonic.** A content change ships a higher version.
3. **Type is immutable.** A skill that becomes a connector is two entries.
4. **`includes` must resolve.** A plugin that names a member slug must name one
   that exists.

## Description rules

Write for the person installing it, not for the machine reading it.

| Good | Bad |
| --- | --- |
| "Read and write Gmail, Drive, Calendar and Docs on a user's behalf." | "MCP server implementing Google APIs v3." |
| "Summarise a directory of PDFs into one Markdown report." | "Skill that calls the summarise tool." |

## Conventions

- **Numbers use Western digits** (`123456789`) in every language, never
  Arabic-Indic numerals.
- Descriptions are one sentence and free of internal links.
- Do not reference private or internal infrastructure.

See [Submitting Entries](./submitting-entries.md) and
[Review Checklist](./review-checklist.md).


