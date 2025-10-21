# Developer-Side MCP Configuration (Section C)

## Options
1. Remote GitHub MCP (OAuth) – simplest.
2. Remote GitHub MCP (PAT) – fine-grained scopes.
3. Local Docker server – isolation / GHES support.

## VS Code (OAuth)
1. Ctrl+Shift+P → mcp: add server.
2. Type: HTTP.
3. URL: https://api.githubcopilot.com/mcp/
4. ID: github
5. Save (workspace or user).
6. Authorize popup.
7. Use tools in Copilot Chat (Agent mode).

## VS Code (PAT)
Create PAT (minimal scopes: repo, issues, pull_request as needed).
Example mcp.json:
```json
{
  "servers": {
    "github": {
      "transport": {
        "type": "http",
        "url": "https://api.githubcopilot.com/mcp/",
        "headers": {
          "Authorization": "Bearer ${env:GITHUB_PAT}"
        }
      }
    }
  }
}
```
Set env var GITHUB_PAT before launching IDE.

## Local Docker
Example:
```json
{
  "servers": {
    "github": {
      "command": "docker",
      "args": [
        "run","-i","--rm",
        "-e","GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
      }
    }
  }
}
```

## Tool Access Control
- Use separate PATs per function set if needed.
- Document approved actions (e.g., issue create, PR comment).

## Common Issues
| Symptom | Fix |
|---------|-----|
| Auth failure | Check PAT scopes / OAuth allowed |
| Tools absent | Refresh Copilot panel; ensure server started |
| Docker error | Verify Docker daemon running |
| Registry block | Confirm server ID in registry |

## Best Practices
- Store workspace config in .vscode/mcp.json.
- Rotate PATs regularly.
- Avoid broad scopes (no admin unless required).
- Keep a local README referencing this file.
