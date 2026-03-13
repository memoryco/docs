# Installation

MemoryCo is distributed as a set of MCP (Model Context Protocol) servers that give your AI assistant persistent memory, filesystem access, and background agents.

## Requirements

- macOS (Apple Silicon or Intel) or Linux (x86_64)
- An MCP-compatible AI client (Claude Desktop, Claude Code, etc.)

## Quick Install

Run the install script to download and configure the memory server:

```bash
curl -fsSL https://memoryco.ai/install.sh | bash
```

This will:

1. Download the latest release binary for your platform
2. Place it in `~/.memoryco/bin/`
3. Create a default configuration at `~/.memoryco/config.toml`
4. Add the MCP server entry to your Claude Desktop configuration

## Additional Servers

MemoryCo also provides a filesystem server (semantic code search) and an agents server (background Claude Code instances):

```bash
curl -fsSL https://memoryco.ai/install_fs.sh | bash
curl -fsSL https://memoryco.ai/install_agents.sh | bash
```

## Verifying Installation

After installation, restart your AI client. You should see the MemoryCo tools available in your tool list. Try asking your assistant:

> "What do you remember about me?"

If identity hasn't been set up yet, the assistant will walk you through onboarding.

## Updating

MemoryCo includes automatic update checking. When a new version is available, you'll be notified on startup. To update manually:

```bash
memoryco update
```
