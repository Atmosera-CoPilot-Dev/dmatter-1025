# MCP Registry Setup (Section B)

## Purpose
Central list of approved MCP servers for governance and optional restriction.

## Minimal Registry JSON
```json
{
  "version": "1.0",
  "servers": [
    {
      "id": "github",
      "manifest": "https://raw.githubusercontent.com/github/github-mcp-server/main/manifest.json",
      "description": "GitHub repository, issues, PR access"
    },
    {
      "id": "internal-analytics",
      "manifest": "https://mcp.internal.example.com/manifest.json",
      "description": "Internal analytics data access"
    }
  ]
}
```

## Hosting
- Serve over HTTPS at a stable URL.
- Use cache headers (short TTL during iteration, longer once stable).
- Monitor for 200 responses and JSON validity.

## Entry Requirements
- Unique id (matches server’s advertised ID).
- Reachable manifest URL.
- Human-readable description.
- Security review completed (auth method, data domains, logging).

## Policy Integration
Org Settings > Copilot > Policies:
- Enable MCP.
- Set Registry URL.
- Optionally choose “Registry only” to block unlisted servers.

## Change Control
- PR-based updates.
- Mandatory reviewer: security + owning team.
- Version tag each manifest change.

## Security Tips
- Pin container/image digests in manifests.
- Prefer least-privilege scopes for tokens.
- Audit registry quarterly (remove unused servers).

## Troubleshooting
| Issue | Action |
|-------|--------|
| Server blocked | Check ID match & registry policy |
| Missing tools | Confirm manifest tools section present |
| Manifest fails | Validate JSON, remove trailing commas |
| Stale data | Clear IDE cache / restart MCP client |
