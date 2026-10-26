# Versioning and Deprecation

An entry is executable intent. Treating it like a document that can be edited in
place is how a workspace becomes non-reproducible.

## The two identities

- The **slug** identifies the entry. It is the public id desktops subscribe to.
- The **version** identifies the content.

Keep them separate. Do not encode a version in a slug (`my-skill-v2`); if the
identity genuinely changes, publish a new entry and retire the old one.

## Versioning

`version` is semantic:

| Change | Bump |
| --- | --- |
| Typo, or wording that does not change behaviour | `patch` |
| New optional capability, new tag, widened compatibility | `minor` |
| Changed endpoint, changed auth type, changed output shape | `major` |

A content change ships as a **new version**, never as a silent rewrite of the
version already published.

## Changing an entry

| You want to… | Do |
| --- | --- |
| Fix a typo | Same slug, `patch` bump |
| Add a tag | Same slug, `minor` bump |
| Point a connector at a new endpoint | Same slug, `major` bump |
| Rename the entry | New slug, and retire the old one |
| Split one entry into two | New slugs, and retire the old one |
| Merge two entries into one | New slug, and retire the old ones |

## Deprecation

Deprecation retires an entry without breaking anyone who already installed it.

**The rule:** a deprecated entry stays resolvable while existing installations
depend on it. Removing it is a separate, announced step.

**The process:**

1. Announce the deprecation, with the reason and the successor.
2. Keep the entry resolvable for a defined window.
3. Withdraw only after the window has passed and a migration path is published.

> **Status.** A machine-readable `deprecated` marker is not part of the schema
> yet. Until it is, deprecation is recorded in the pull request that retires the
> entry and announced in
> [Announcements](https://github.com/idexal/extensions-catalog/discussions/categories/announcements).
> The proposed shape is discussed in
> [Ideas](https://github.com/idexal/extensions-catalog/discussions/categories/ideas).

## Why this matters

- **Reproducibility** — a workspace that worked yesterday still works today.
- **Auditability** — you can say which version ran.
- **Trust** — a user can accept an update deliberately, or pin and ignore it.

## Open questions

These are live design questions:

- Should a pinned version hard-fail or warn when it is withdrawn?
- How long does a withdrawn version remain fetchable?
