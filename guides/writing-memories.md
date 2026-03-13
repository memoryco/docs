# Writing Good Memories

The quality of your AI assistant's memory depends entirely on how memories are written. This guide covers the principles that make memories searchable, useful, and durable.

## The Golden Rule: One Fact Per Memory

Each memory generates a semantic embedding — a vector that captures its meaning for search. When a single memory contains multiple unrelated facts, the embedding becomes an average of all of them, making it harder to find any individual fact.

### Bad

> "Design meeting: switching to PostgreSQL, API versioning will use URL paths, auth will use OAuth2 with PKCE, targeting Q2 launch."

This memory contains four separate decisions. A search for "authentication approach" has to compete with database and timeline information in the same embedding.

### Good

> "Design meeting: switching to PostgreSQL for the primary datastore"
> "Design meeting: API versioning will use URL path style"
> "Design meeting: auth will use OAuth2 with PKCE flow"
> "Design meeting: targeting Q2 for launch"

Each fact is independently searchable. A query about authentication finds the auth decision directly.

## Context Anchoring

Repeat shared context as a prefix on related memories. This helps both search and human readability:

- "Project X: database migration completed"
- "Project X: API endpoints updated to v2"
- "Project X: tests passing at 98% coverage"

## What to Store

Store aggressively. Decay handles pruning — unused memories fade naturally, but a missed store is gone forever.

Good candidates:
- Technical decisions and their rationale
- Project facts (stack, architecture, conventions)
- Bugs, gotchas, and workarounds
- Personal context people share with you
- Workflow optimizations
- Corrections to your understanding

Skip:
- Exact duplicates of existing memories
- Ephemeral task state (test counts that change daily)
- Information already in Identity
- Temporary conversation state

## Mechanical Checks

Before storing, verify:

1. Does it contain only one distinct fact?
2. If it lists items (1), (2), (3) — split each into its own memory
3. More than 2 sentences? Check for multiple facts
4. If removing half would leave a complete memory — split it
5. Are you using a date as a prefix? Remove it — `created_at` captures timing automatically
