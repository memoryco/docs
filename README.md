# MemoryCo Documentation

Source files for [memoryco.ai/docs](https://memoryco.ai/docs).

## Structure

```
docs/
├── manifest.json              # Sidebar navigation and page ordering
├── getting-started/
│   ├── installation.md
│   ├── quickstart.md
│   └── configuration.md
├── concepts/
│   ├── memories.md
│   ├── identity.md
│   ├── references.md
│   └── lenses.md
├── tools/
│   ├── memory-server.md
│   ├── filesystem-server.md
│   └── agents-server.md
└── guides/
    ├── writing-memories.md
    └── procedures.md
```

## How It Works

The website at memoryco.ai fetches docs from the latest **tagged release** of this repo. Pushing to `main` does not publish — you must create a release.

A Cloudflare Worker handles `/docs/*` routes:
1. Checks KV cache for the rendered page
2. On miss: fetches the latest release tag, pulls markdown + manifest, renders to HTML
3. Stores rendered HTML in KV with the design system shell
4. A GitHub webhook on `release` events purges the KV cache

## Adding a Page

1. Create a `.md` file in the appropriate section directory
2. Add an entry to `manifest.json` with the slug and title
3. Commit, push, and create a release

## Writing Guidelines

- Use standard Markdown (rendered via marked.js)
- Code blocks with language hints for syntax highlighting
- Relative links between docs pages use the slug path (e.g., `[Installation](getting-started/installation)`)
- Images go in an `assets/` directory (create if needed) and are fetched from the same release tag

## Local Preview

*Coming soon* — a local preview server for testing docs before publishing.
