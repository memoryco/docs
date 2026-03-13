# Lenses

Lenses are task-specific context guides that get loaded entirely into your assistant's working memory for the duration of a task. Unlike memories (searched on demand) or references (queried for specific sections), lenses are meant to be held in context and applied consistently throughout a piece of work.

## Use Cases

- **Style guides** — load before writing or editing tasks
- **Review checklists** — load before code review
- **Documentation standards** — load before writing docs
- **Project conventions** — load before working on a specific codebase

## How Lenses Work

Lenses are stored as text content in MemoryCo and retrieved whole via the `lenses_get` tool. Your assistant loads the relevant lens at the start of a task and applies its guidance throughout.

```
1. lenses_list       → see available lenses
2. lenses_get "name" → load into context
3. Apply throughout the task
```

## Creating Lenses

Lenses can be created through conversation with your assistant or programmatically. A lens is just a named block of text — there's no special format required, though structured content (checklists, rules, examples) tends to work best.

## Lenses vs. Identity Instructions

Identity instructions apply to *every* conversation. Lenses apply to *specific tasks*. If a rule should always be followed, put it in identity. If it only matters for certain work, make it a lens.
