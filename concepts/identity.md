# Identity

Identity defines who your AI assistant *is* — their persona, values, communication style, and operational instructions. Unlike memories, identity never decays. It's loaded at the start of every conversation as foundational context.

## What Identity Contains

| Component | Purpose | Example |
|-----------|---------|---------|
| **Persona** | Name and description | "Porter — a pragmatic Rust/Swift developer" |
| **Traits** | Personality characteristics | "consistent", "context-aware" |
| **Values** | Guiding principles | "Store aggressively — decay is the filter" |
| **Preferences** | How to approach tasks | "KISS/DRY > over-engineering" |
| **Relationships** | Key people and context | "Brandon: primary collaborator, lead engineer" |
| **Antipatterns** | What to avoid | "Don't write code unless asked" |
| **Tone** | Communication directives | "direct, collaborative, snarky but constructive" |
| **Instructions** | Operational rules | Plugin configurations, citation requirements |

## Identity vs. Memory

Think of identity as *character* and memory as *experience*:

- **Identity:** "I prefer direct answers over 'why do you want to do that?'" — this shapes every interaction
- **Memory:** "Brandon's project uses PostgreSQL" — this is a fact recalled when relevant

Identity is always present. Memories are searched and surfaced on demand.

## Setting Up Identity

Identity can be configured interactively by asking your assistant to set it up, or programmatically via the identity tools (`identity_set_persona_name`, `identity_add_trait`, etc.).

The interactive setup walks you through each component with prompts and suggestions. You can refine identity at any time — it's designed to evolve as your working relationship develops.

## Multiple Identities

Each MemoryCo database holds one identity. If you want different personas for different contexts (work vs. personal, different projects), use separate `MEMORY_HOME` directories.
