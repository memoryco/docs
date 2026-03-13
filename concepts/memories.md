# Memories & Engrams

Memories are the core unit of storage in MemoryCo. Each memory — called an **engram** — is a single atomic fact or concept stored with a semantic embedding for retrieval.

## The Cognitive Model

MemoryCo is modeled on how biological memory works, not how databases work:

- **Memories have energy** — newly created memories start with full energy. Energy decays over time without use, just like biological memories fade when not reinforced.
- **Recall strengthens memories** — when a memory is referenced in conversation, it gets recalled, boosting its energy. Frequently useful memories stay alive; irrelevant ones fade naturally.
- **Memories form associations** — memories that are recalled together become linked automatically through Hebbian learning ("neurons that fire together wire together"). These associations help surface related context during search.

## Lifecycle

1. **Created** — stored with full energy and a semantic embedding
2. **Active** — energy above the archive threshold, searchable and retrievable
3. **Archived** — energy dropped below threshold, hidden from default search but not deleted
4. **Deep Storage** — long-dormant memories moved to cold storage, retrievable on request

## Atomicity

Each engram should contain exactly one fact or concept. This is a design principle, not just a suggestion — compound memories produce averaged embeddings that reduce search accuracy.

**Good:** "Project X uses PostgreSQL for the primary datastore"

**Bad:** "Project X uses PostgreSQL for the primary datastore, targets Q2 launch, and the team decided on OAuth2 with PKCE for auth"

The bad example contains three separate facts. Each would retrieve better as its own engram.

## Search

Memories are found via semantic search — you describe what you're looking for in natural language, and MemoryCo finds memories with similar meaning. This works even when the query and the memory use different words for the same concept.

Search can be enhanced with:

- **Query expansion** — the query is enriched with related terms before searching
- **Multi-vector enrichment** — memories are indexed with additional embedding vectors from different angles
- **LLM reranking** — search results are re-scored by an LLM for contextual relevance
