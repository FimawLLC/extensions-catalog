# Connector Auth

A connector declares the shape of its authentication through `authType`, so a
client can render the right setup flow from the entry alone, without a client
release.

## Supported values

| `authType` | Use when | Secret lives |
| --- | --- | --- |
| `none` | The endpoint is open, or authentication is out of band | â€” |
| `apikey` | The endpoint accepts a token or API key | per user |
| `oauth` | The vendor issues tokens through a redirect flow | platform, per user |

## The endpoint

`url` must be an `https://` MCP endpoint. Plain `http://` is rejected; a
connector that cannot be reached over TLS cannot be shipped.

```json
{
  "slug": "example-mcp",
  "type": "connector",
  "url": "https://mcp.example.com/mcp",
  "authType": "oauth"
}
```

## Examples

### OAuth

```json
{
  "slug": "google-workspace",
  "type": "connector",
  "name": "Google Workspace",
  "description": "Read and write Gmail, Drive, Calendar and Docs on a user's behalf.",
  "version": "1.0.0",
  "source": "https://github.com/owner/google-workspace-mcp",
  "url": "https://mcp.example.com/google",
  "authType": "oauth",
  "tags": ["email", "files", "calendar"]
}
```

### API key

```json
{
  "slug": "example-api",
  "type": "connector",
  "name": "Example API",
  "description": "Query the Example service from an agent task.",
  "version": "1.0.0",
  "source": "https://github.com/owner/example-api-mcp",
  "url": "https://mcp.example.com/api",
  "authType": "apikey",
  "tags": ["api"]
}
```

## Rules

1. **Declare, do not imply.** If a connector needs a credential, the entry says
   so. A requirement that only appears at runtime is a defect.
2. **Least function.** The endpoint you point at should do what the description
   says and not more.
3. **No secrets in the entry.** An entry describes where a secret comes from; it
   never contains one.
4. **Stable endpoint.** A published `url` is part of the contract; moving it is a
   breaking change and needs a new entry plus a deprecation note.

## Related reading

- [Entry Schema](./entry-schema.md)
- [Submitting Entries](./submitting-entries.md)
- [Review Checklist](./review-checklist.md)


