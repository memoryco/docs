# Procedure Chains

Procedure chains let you store repeatable multi-step processes as linked memories. When you describe a process to your assistant — a deployment workflow, a review checklist, a troubleshooting sequence — it can be stored as a chain and recalled as a complete ordered sequence later.

## How Chains Work

A procedure chain consists of:

1. **An anchor memory** — tagged with "PROCEDURE:" prefix, discoverable via search
2. **Step memories** — one per step, each a standalone memory
3. **Ordered associations** — the anchor points to each step with an ordinal (1, 2, 3...)

When search finds the anchor, a hint indicates a procedure chain exists. The assistant then walks the chain via `engram_associations` to retrieve all steps in order.

## Example

Suppose you describe your release process:

> "To release: first bump the version in Cargo.toml, then run the test suite, tag the commit, push the tag, and verify CI passes."

This becomes:

- **Anchor:** "PROCEDURE: MemoryCo release process"
- **Step 1:** "Release step: bump version in Cargo.toml"
- **Step 2:** "Release step: run full test suite"
- **Step 3:** "Release step: tag the commit with version"
- **Step 4:** "Release step: push the tag to origin"
- **Step 5:** "Release step: verify CI pipeline passes"

Each step is associated to the anchor with ordinals 1–5 and weight 0.8.

## When to Use Chains

Use procedure chains for any repeatable process with 3 or more ordered steps. If it's only 2 steps, regular memories are fine. If the steps don't have a meaningful order, use unordered associations instead.

## Recalling Chains

When your assistant searches and finds a procedure anchor (indicated by a chain hint in results), it should:

1. Call `engram_associations` on the anchor with `direction: outbound`
2. Sort by ordinal
3. Present the steps in order
4. Recall all step IDs to reinforce the chain
