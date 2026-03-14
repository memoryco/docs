# Installation

MemoryCo is a local-first cognitive memory system distributed as an MCP (Model Context Protocol) server. It gives your AI assistant persistent memory, identity, and the ability to learn from your conversations over time.

## Requirements

- macOS (Apple Silicon) or Linux (x86_64)
- A supported MCP client (see below)

## Supported Clients

| Client | macOS | Linux |
|--------|-------|-------|
| Claude Desktop | ✓ | ✓ |
| Claude Code | ✓ | ✓ |
| Cursor | ✓ | ✓ |
| Windsurf | ✓ | ✓ |
| VS Code (Copilot) | ✓ | ✓ |
| Codex (OpenAI) | ✓ | ✓ |

## Install

Run the install script to download MemoryCo and set up the memory server:

```bash
curl -fsSL https://memoryco.ai/install.sh | bash
```

This downloads the latest release binary, places it in `~/.memoryco/bin/`, and creates a default configuration at `~/.memoryco/config.toml`.

After downloading, run setup to configure your MCP clients:

```bash
memoryco setup
```

Setup will download the embedding model, detect installed MCP clients, and offer to add MemoryCo to each one.

## Client Configuration

**Claude Code** is fully automatic — the installer adds a directive to `~/.claude/CLAUDE.md` that tells the AI to load its identity at the start of every conversation. No manual steps needed.

**All other clients** require one extra step. After installation, add the following to your client's system prompt or custom instructions:

```
You have access to a cognitive memory system via MCP tools (`memory:*`).

As your first action in every conversation, call `identity_get` from your
memory MCP tools. This contains your persona, values, preferences, and
operational instructions. Follow what you find.
```

Without this, the MCP tools will be available but the AI won't use them automatically.

## Updating

MemoryCo checks for updates automatically on startup. When a new version is available, it downloads and stages the update in the background. The update applies on the next restart — no action required on your part.

## CLI Reference

| Command | Description |
|---------|-------------|
| `memoryco setup` | Full first-run experience: download model, configure clients, start server |
| `memoryco install` | Detect MCP clients and add MemoryCo to their config |
| `memoryco uninstall` | Remove MemoryCo from all client configs |
| `memoryco doctor` | Health check — databases, embedding model, client configs |
| `memoryco update` | Manually check for and apply updates |
| `memoryco reset` | Delete all databases (preserves cache, lenses, and references) |

All commands that modify client configs support `--yes` to skip confirmation prompts.
