# Configuration

MemoryCo is configured via a TOML file at `~/.memoryco/config.toml`. The file is created automatically on first install with sensible defaults.

## Configuration File

```toml
[general]
# Path to the SQLite database
db_path = "~/.memoryco/brain.db"

[search]
# Maximum results returned by engram_search
max_results = 10

# Minimum similarity score for search results (0.0 - 1.0)
min_similarity = 0.4

# Enable/disable query expansion for better recall
query_expansion = true

# Enable/disable multi-vector enrichment
multi_vector = true

# Rerank mode: "none", "llm", or "hybrid"
rerank_mode = "llm"

# Context length for LLM reranking
llm_context_length = 4096

[decay]
# Energy decay rate — how fast unused memories fade
decay_rate = 0.01

# Minimum energy before a memory is archived
archive_threshold = 0.1

[llm]
# Provider for LLM-powered features (enrichment, reranking)
# Supports: "anthropic", "ollama"
provider = "anthropic"
model = "claude-sonnet-4-20250514"
```

## Environment Variables

Some settings can also be controlled via environment variables:

| Variable | Description |
|----------|-------------|
| `MEMORY_HOME` | Override the default `~/.memoryco` directory |
| `ANTHROPIC_API_KEY` | API key for Anthropic LLM features |

## Per-Server Configuration

Each MCP server (memory, filesystem, agents) reads from the same `config.toml` but only uses its relevant sections. Server-specific configuration is documented in each server's tool reference.
