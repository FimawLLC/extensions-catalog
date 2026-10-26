# Submitting Entries

## The short version

1. Create a file in the matching directory, named after the slug:
   `<slug>.json` for a connector or plugin, `<slug>.md` for a skill.
2. Fill in the required fields for that type.
3. Open a pull request. Once merged, the entry appears in the marketplace on the
   next catalog refresh.

Do not edit `catalog.json` by hand — it is generated from the per-type files.

## Checklist

- [ ] The file is in `connectors/`, `skills/` or `plugins/`.
- [ ] The file is named `<slug>.json` or `<slug>.md`.
- [ ] The `slug` is unique, lowercase and hyphen-separated.
- [ ] `type` matches the directory.
- [ ] `version` is set, and bumped if the content changed.
- [ ] `description` is one customer-facing sentence.
- [ ] `source` points at the content a client should materialise.
- [ ] For a connector: `url` is `https://` and `authType` is one of `oauth`,
      `apikey` or `none`.
- [ ] For a plugin: every slug in `includes` resolves.
- [ ] No secret, internal link or private infrastructure reference is present.

## Per type

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

State the auth shape up front; never leave the credential requirement to be
discovered at runtime. See [Connector Auth](./connector-auth.md).

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

Keep the skill scoped to one job, and state anything it assumes about the
workspace.

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

List the member slugs in `includes`, confirm every one resolves, and do not
duplicate a member's content inside the plugin.

## After you open the pull request

A reviewer checks three things: that the entry validates, that the identity
(slug and version) is sound, and that nothing in the entry asks for more access
than it explains. Questions during review are normal — answer them in the pull
request, not in a new thread, so the discussion stays with the change.

## What gets an entry rejected

| Reason | Why it matters |
| --- | --- |
| A slug that changed between versions | Installs are keyed on it; the change orphaned them |
| A description written for machines | The marketplace reads entries to users |
| A connector whose `url` is not `https://` | The endpoint cannot be reached safely |
| A connector that hides its `authType` | The user discovers it at runtime, mid-task |
| A plugin whose `includes` do not resolve | Install fails for everyone who tries |

## Blocked?

Open a **Q&A** discussion in this repository with the entry you are adding and the
problem you hit.
