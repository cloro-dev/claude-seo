# cloro extension setup

cloro (https://cloro.dev?utm_source=claude-seo&utm_medium=byok) sends a prompt
to ChatGPT, Google AI Mode, or Gemini, or runs a Google
search with its AI Overview, from a chosen country. It returns the answer text
and the cited sources. The extension connects Claude Code to cloro's hosted MCP
server. Nothing is installed locally except the skill file.

## 1. Get an API key

Get a key at https://dashboard.cloro.dev/api-keys?utm_source=claude-seo&utm_medium=byok.
The Free plan includes 500 credits a month.

## 2. Install

```bash
./extensions/cloro/install.sh        # Linux / macOS
.\extensions\cloro\install.ps1       # Windows
```

The installer asks for the key (input hidden), copies `seo-cloro` to
`~/.claude/skills/`, and adds this entry to `~/.claude.json` (mode 0600 on
Linux and macOS). If `~/.claude.json` is not valid JSON, the installer stops
and changes nothing.

```json
{
  "mcpServers": {
    "cloro": {
      "type": "http",
      "url": "https://mcp.cloro.dev/mcp",
      "headers": { "Authorization": "Bearer <your-cloro-api-key>" }
    }
  }
}
```

## 3. Verify

Open a new Claude Code session, run `/mcp`, and check that `cloro` is
connected. Then run:

```
/seo cloro ask chatgpt "best project management tool for small teams"
```

## Credits

Every tool call is a sync request: the provider's base credits plus 2.
Rates from https://cloro.dev/docs/guides/providers?utm_source=claude-seo&utm_medium=byok,
checked 2026-11-04:

| Engine | Base | Per MCP call |
|---|---|---|
| ChatGPT | 5 | 7 |
| Gemini | 4 | 6 |
| Google AI Mode | 4 | 6 |
| Google Search | 3 | 5 |
| Google Search with AI Overview | 3 + 2 | 7 |

`/seo cloro visibility` runs ChatGPT, Gemini, AI Mode, and Google Search with
AI Overview once: 26 credits.

## Uninstall

```bash
./extensions/cloro/uninstall.sh      # Linux / macOS
.\extensions\cloro\uninstall.ps1     # Windows
```

This removes the skill and the `cloro` entry in `~/.claude.json`.
