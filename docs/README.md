# extensions-catalog documentation

This repository is the canonical index of the **connectors**, **skills** and
**plugins** that Fimaw Code can surface in the marketplace. The desktop app, the
platform marketplace and the MCP gateway all read this catalog, so it is the one
source of truth rather than a hand-maintained list per surface.

Product-level questions about the app or the platform belong in the
[Fimaw Code discussions](https://github.com/FimawLLC/FimawCode/discussions). These
documents are about catalog entries and the catalog contract.

---

## Start here

| If you want toâ€¦ | Read |
| --- | --- |
| Understand what an entry is | [Entry Schema](./entry-schema.md) |
| Add a connector, skill or plugin | [Submitting Entries](./submitting-entries.md) |
| Wire up authentication for a connector | [Connector Auth](./connector-auth.md) |
| Change something without breaking consumers | [Versioning and Deprecation](./versioning-and-deprecation.md) |
| Know what a reviewer checks | [Review Checklist](./review-checklist.md) |
| Get a quick answer | [FAQ](./faq.md) |

---

## The three entry types

| Type | Directory | What it is | Delivered as |
| --- | --- | --- | --- |
| `connector` | `connectors/` | A hosted or self-managed MCP endpoint | JSON with `url` + `authType` |
| `skill` | `skills/` | An instruction set an agent follows | Markdown with YAML front matter |
| `plugin` | `plugins/` | A bundle that installs several components together | JSON referencing member slugs |

## The one rule to remember

The **slug** is the identity. Installs, marketplace lookups and uninstall all key
on it. Changing a slug is publishing a **new entry**, never editing an existing
one. If you take one thing from these documents, take that.

## How an entry reaches a user

```text
you  â”€â”€â–¶  pull request  â”€â”€â–¶  review  â”€â”€â–¶  this repository
                                             â”‚
                                             â–¼
                              catalog.json (generated)
                                             â”‚
                                             â–¼
                       marketplace  â”€â”€â–¶  desktop library / MCP gateway
```

Because the platform derives its marketplace revision from this catalog, a merged
change becomes visible to desktops through the normal inventory sync â€”
[Fimaw Code Sync Contract](https://github.com/FimawLLC/FimawCode/blob/main/docs/sync-contract.md).

## Conventions

- **Numbers use Western digits** (`123456789`) in every language, never
  Arabic-Indic numerals.
- Descriptions are one sentence, customer-facing, and free of internal links.
- Do not reference private or internal infrastructure.


