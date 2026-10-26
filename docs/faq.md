# FAQ

### What is this repository for?

It is the official, open catalog of extensions for idexal Os. Every entry here can
be installed from the in-app marketplace and is delivered to every desktop in an
organization. The marketplace serves `catalog.json`, which is generated from the
per-type files.

### What is the difference between a skill, a connector and a plugin?

- A **skill** is an instruction set the agent follows, in Markdown with YAML
  front matter.
- A **connector** is a hosted or self-managed MCP endpoint with a `url` and an
  `authType`.
- A **plugin** bundles several components, listing their slugs in `includes`.

### Which files do I edit?

| Type | Directory | File |
| --- | --- | --- |
| Connector | `connectors/` | `<slug>.json` |
| Skill | `skills/` | `<slug>.md` |
| Plugin | `plugins/` | `<slug>.json` |

Never edit `catalog.json` by hand; it is generated.

### Can I rename an entry?

Not in place. The slug is the public id desktops subscribe to, and installs are
keyed on it. Publish a new entry and retire the old one. See
[Versioning and Deprecation](./versioning-and-deprecation.md).

### How do I bump the version?

| Change | Bump |
| --- | --- |
| Wording that does not change behaviour | `patch` |
| New optional capability or tag | `minor` |
| Changed endpoint, auth type or output shape | `major` |

### What values does `authType` accept?

`oauth`, `apikey` or `none`. See [Connector Auth](./connector-auth.md).

### Does `url` have to be HTTPS?

Yes. A connector that cannot be reached over TLS cannot be shipped.

### Where do I put a secret?

Nowhere in this repository. An entry declares *that* a credential is needed and
*which shape* it takes; the secret itself is stored by the platform or by the
user's machine.

### How long until my entry is visible to users?

Once merged, the marketplace picks it up on the next catalog refresh. The
platform's marketplace revision then advances, and desktops see it through the
normal inventory sync —
[Sync Contract](https://github.com/idexal/idexal-OS/blob/main/docs/sync-contract.md).

### My entry is rejected — where do I get help?

Open a **Q&A** discussion with the entry and the exact problem.

### Where do product questions go?

[idexal Os discussions](https://github.com/idexal/idexal-OS/discussions). This
repository is about the catalog.
