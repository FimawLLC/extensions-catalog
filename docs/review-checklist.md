# Review Checklist

What a reviewer checks, in order. Keeping this list close to the pull request
template means fewer review round trips.

## 1. Placement and validity

- [ ] The file is in `connectors/`, `skills/` or `plugins/`.
- [ ] The file is named after the slug (`<slug>.json` or `<slug>.md`).
- [ ] All required fields for that type are present and correctly typed.
- [ ] `catalog.json` was **not** edited by hand.

## 2. Identity

- [ ] The `slug` is unique, lowercase and hyphen-separated.
- [ ] The `slug` did not change. A rename is a new entry, not an edit.
- [ ] `version` is bumped relative to what was published.
- [ ] `type` matches the directory and did not change.

## 3. Access

- [ ] For a connector: `url` is an `https://` MCP endpoint.
- [ ] For a connector: `authType` is one of `oauth`, `apikey` or `none`, and
      matches what the endpoint actually requires.
- [ ] No secret, token or key appears anywhere in the entry.

## 4. Quality

- [ ] `description` is one customer-facing sentence, not an implementation note.
- [ ] A skill ships the Markdown the agent reads, scoped to one job.
- [ ] A plugin's `includes` all resolve and none of them duplicate content.
- [ ] Names and tags follow the surrounding entries.
- [ ] Numbers are written with Western digits in every language.

## 5. Retirement (if applicable)

- [ ] Any entry being retired is announced, with the reason and the successor.
- [ ] Existing installations are not broken by the change.

See [Versioning and Deprecation](./versioning-and-deprecation.md).

## Outcome

| Result | Meaning |
| --- | --- |
| Approved | Placement, identity, access and quality all check out |
| Changes requested | A specific item above is unmet; the reviewer names which |
| Rejected | The entry cannot be made acceptable as proposed â€” for example it takes a live slug |

## A note on tone

Review comments are about the entry, not the author. If an item above is unclear,
say so â€” the checklist is itself improvable.


