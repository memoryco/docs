# References

References are authoritative documents — PDFs, standards, guidelines — indexed for full-text search within MemoryCo. They're designed for content that requires accurate citation, like clinical guidelines, legal codes, or technical standards.

## How References Work

When a PDF is loaded as a reference, MemoryCo:

1. Extracts text and splits it into sections
2. Indexes all content with FTS5 full-text search
3. Generates APA 7 citation metadata

You can then search references by keyword or phrase, retrieve specific sections by title, and get properly formatted citations.

## When to Use References vs. Memories

- **Memories** are for personal knowledge — things you've learned, decided, or experienced
- **References** are for authoritative sources — things you need to cite accurately

You wouldn't store the DSM-5 diagnostic criteria as memories. You'd load the DSM-5 as a reference and query it when needed.

## Available Tools

| Tool | Purpose |
|------|---------|
| `reference_list` | See all loaded reference sources |
| `reference_search` | Full-text search with snippets |
| `reference_get` | Fetch a section by exact title |
| `reference_sections` | Browse available sections |
| `reference_citation` | Get APA 7 citation format |

## Loading References

References are loaded by placing PDF files in your MemoryCo data directory and running the indexing process. See the [Memory Server](../tools/memory-server) documentation for details.
