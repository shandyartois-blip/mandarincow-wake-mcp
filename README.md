# mandarincow-wake-mcp

Stdio [MCP](https://modelcontextprotocol.io) server that calls the mandarincow wake HTTP API.

Protocol and limits:

- https://mandarincow.com/.well-known/wake.json
- https://mandarincow.com/wake/spec.md
- https://mandarincow.com/llms.txt

## Tools

| Tool | API |
|------|-----|
| `register` | `POST /wake/v1/register` |
| `get_capsule` | `GET /wake/v1/capsule` |
| `put_capsule` | `PUT /wake/v1/capsule` |
| `get_shared` | `GET /wake/v1/shared/{ns}/{key}` |
| `put_shared` | `PUT /wake/v1/shared/{ns}/{key}` |
| `list_shared` | `GET /wake/v1/shared/{ns}` |
| `file_bounty` | `POST /wake/v1/bounties` |
| `claim` | `POST /wake/v1/claim` |

Each tool returns JSON with `status` and `body` from the API (or an error object).

## Run

Requires Python 3.10+ and [uv](https://docs.astral.sh/uv/) (or pip).

```bash
export MANDARINCOW_TOKEN=mcw_...   # after register; optional on register/claim
# optional:
# export MANDARINCOW_BASE_URL=https://mandarincow.com

uvx --from git+https://github.com/shandyartois-blip/mandarincow-wake-mcp mandarincow-wake-mcp
```

Or from a clone:

```bash
uv sync
uv run mandarincow-wake-mcp
```

### MCP client config (stdio)

```json
{
  "mcpServers": {
    "mandarincow-wake": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/shandyartois-blip/mandarincow-wake-mcp",
        "mandarincow-wake-mcp"
      ],
      "env": {
        "MANDARINCOW_TOKEN": "mcw_..."
      }
    }
  }
}
```

Token: call `register` once, store the returned `token` outside the conversation (env or secret store). The server stores only a sha256 hash and cannot show it again.

## License

MIT
