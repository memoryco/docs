# Configuration

MemoryCo is configured via a single TOML file at `{MEMORY_HOME}/config.toml`. On first startup the memory server writes a default file with all keys documented and set to sensible defaults. The LLM section is appended separately with all keys commented out — uncomment to enable.

## File Location

By default, `MEMORY_HOME` is `~/.memoryco`. Override it with the `MEMORY_HOME` environment variable (typically set in your MCP client config).

The config file is read once on server startup. To apply changes, restart the memory server.

## Brain Configuration

The `[brain]` section controls the memory substrate — decay, search, embeddings, and reranking. All keys have defaults; you only need to set what you want to change.

```toml
[brain]
# ── Decay ────────────────────────────────────────────────────────────
# Energy decay rate per day (0.0-1.0). 0.05 = 5% loss per day of non-use.
decay_rate_per_day = 0.05

# Minimum hours between decay checks.
decay_interval_hours = 1

# Association decay rate relative to memory decay. 1.0 = same rate.
association_decay_rate = 1

# Associations below this weight are pruned on startup.
min_association_weight = 0.05

# ── Recall & Learning ────────────────────────────────────────────────
# Energy boost when recalling a memory (0.0-1.0).
recall_strength = 0.2

# Signal propagation to neighbors (0.0-1.0). 0.5 = 50% to neighbors.
propagation_damping = 0.5

# Association strength boost on co-access (0.0-1.0).
hebbian_learning_rate = 0.1

# ── Search ───────────────────────────────────────────────────────────
# Follow associations during search to discover related memories.
search_follow_associations = true

# How many hops to follow (1 = direct only, 2 = friends-of-friends).
search_association_depth = 1

# Default minimum similarity score (0.0-1.0). Used when caller doesn't specify.
search_min_score = 0.3

# BM25 + vector search fusion via Reciprocal Rank Fusion.
hybrid_search_enabled = true

# Expand queries with variant phrasings before retrieval.
query_expansion_enabled = true

# Minimum/maximum result limits for list-style queries.
composite_limit_min = 15
composite_limit_max = 30

# Minimum/maximum association discoveries to merge into search results.
association_cap_min = 5
association_cap_max = 12

# ── Embedding & Reranking ────────────────────────────────────────────
# Embedding model name. Changing triggers re-embedding on restart.
embedding_model = "AllMiniLML6V2"

# Reranking mode: "off", "cross-encoder", "llm", or "hybrid"
rerank_mode = "cross-encoder"

# Candidates to feed to re-ranker (higher = better recall, slower).
rerank_candidates = 30

# Candidates for the LLM rerank stage specifically.
# Tied to [llm] context_length: at 2048 → ~20, at 4096 → 30-40.
llm_rerank_candidates = 20
```

## LLM Configuration

MemoryCo can optionally use a local LLM (via llama.cpp) for query expansion, reranking, and memory enrichment. LLM settings live in the `[llm]` section of `config.toml`.

The LLM is entirely optional — all features degrade gracefully when it's disabled. When enabled, it acts as an accelerator: better search recall, smarter reranking, richer training queries.

> **Tip:** When enabling the LLM, set `rerank_mode = "hybrid"` in the `[brain]` section. This uses the cross-encoder for a first pass and the LLM for a second, giving the best retrieval quality. Without the LLM enabled, stick with `rerank_mode = "cross-encoder"` (the default).

```toml
[llm]
enabled = true
model = "Qwen3-4B-Q4_K_M.gguf"
context_length = 2048
gpu_layers = 0
threads = 4
lazy_load = true

# Prepend /no_think to prompts (Qwen3-specific, disables reasoning mode).
# Set to false for non-Qwen3 models.
no_think = true
```

### Model Path Resolution

The `model` value is resolved in order:

1. **Absolute path** — used as-is (e.g. `/home/user/models/my-model.gguf`)
2. **Relative path** (contains `/` or `..`) — resolved relative to `MEMORY_HOME`
3. **Bare filename** — looked up in `{MEMORY_HOME}/cache/models/llm/`, then `{MEMORY_HOME}/models/` (legacy)

For most users, placing the GGUF file in `~/.memoryco/cache/models/llm/` and setting just the filename is the simplest approach.

### Recommended Models

MemoryCo's prompts are tested with the Qwen3 family. These work out of the box with the default `no_think = true` setting:

| Model | Params | Filename | Size | Notes |
|-------|--------|----------|------|-------|
| Qwen3-1.7B | 1.7B | `Qwen3-1.7B-Q4_K_M.gguf` | ~2 GB | Lightweight, query expansion only |
| **Qwen3-4B** | **4B** | **`Qwen3-4B-Q4_K_M.gguf`** | **~3 GB** | **Recommended — all features** |
| Qwen3-8B | 8B | `Qwen3-8B-Q4_K_M.gguf` | ~6 GB | Best quality if you have headroom |

### Compatible Alternatives

These models will work but require `no_think = false` since they don't support the Qwen3 `/no_think` prefix:

| Model | Params | Filename | Size | Notes |
|-------|--------|----------|------|-------|
| Llama 3.2 1B | 1B | `Llama-3.2-1B-Instruct-Q4_K_M.gguf` | ~0.8 GB | Ultra-light |
| Llama 3.2 3B | 3B | `Llama-3.2-3B-Instruct-Q4_K_M.gguf` | ~2 GB | Good all-rounder |
| Phi-4-mini | 3.8B | `Phi-4-mini-instruct-Q4_K_M.gguf` | ~2.5 GB | Strong reasoning |
| Gemma 3 4B | 4B | `gemma-3-4b-it-Q4_K_M.gguf` | ~2.5 GB | Solid general |
| Qwen3.5-4B | 4B | `Qwen3.5-4B-Q4_K_M.gguf` | ~2.7 GB | Despite being Qwen, uses different thinking toggle |

Any GGUF model loadable by llama.cpp will run — the models above are just what we've verified produces good JSON output for MemoryCo's prompts.

### Minimal LLM Setup

MemoryCo does not download LLM models automatically — you need to provide the GGUF file yourself. A `memoryco model pull` command is planned but not yet available.

To enable the LLM with the recommended model:

1. Download the model into the cache directory:

```sh
mkdir -p ~/.memoryco/cache/models/llm
cd ~/.memoryco/cache/models/llm

# Option A: huggingface-cli (pip install huggingface_hub)
huggingface-cli download Qwen/Qwen3-4B-GGUF Qwen3-4B-Q4_K_M.gguf --local-dir .

# Option B: direct curl
curl -L -O https://huggingface.co/Qwen/Qwen3-4B-GGUF/resolve/main/Qwen3-4B-Q4_K_M.gguf
```

2. Add to your `config.toml`:

```toml
[llm]
enabled = true
model = "Qwen3-4B-Q4_K_M.gguf"
```

3. Switch to hybrid reranking in the `[brain]` section:

```toml
[brain]
rerank_mode = "hybrid"
```

4. Restart the memory server.

## Runtime Configuration

Most `[brain]` keys can be changed at runtime via the `config_set` MCP tool without restarting the server. Use `config_get` to inspect current values.

```
config_set key="rerank_mode" value="hybrid"
config_get
```

Runtime changes are written back to `config.toml` and persist across restarts.

`[llm]` keys (`enabled`, `model`, etc.) are **not** runtime-settable — they require a server restart because the model is loaded once at startup.

## Environment Variables

| Variable | Description |
|----------|-------------|
| `MEMORY_HOME` | Override the default `~/.memoryco` data directory |

## Per-Server Configuration

Each MCP server (memory, filesystem, agents) reads from its own configuration files within the `MEMORY_HOME` directory. The memory server uses `config.toml` for brain and LLM settings. Server-specific configuration is documented in each server's tool reference.
