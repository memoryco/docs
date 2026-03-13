# Memory Server

The memory server is the core of MemoryCo — it provides persistent memory, identity, references, lenses, and plans via MCP tools.

## Tools

### Memory Management

| Tool | Description |
|------|-------------|
| `engram_create` | Store new memories (supports batch creation) |
| `engram_search` | Semantic search across all memories |
| `engram_recall` | Reinforce memories and build associations |
| `engram_get` | Retrieve a specific memory by ID |
| `engram_delete` | Permanently remove a memory |
| `engram_associate` | Create explicit links between memories |
| `engram_associations` | View associations for a memory |
| `engram_stats` | Database statistics |
| `engram_graph` | Full association graph for visualization |

### Identity

| Tool | Description |
|------|-------------|
| `identity_get` | Load full identity |
| `identity_setup` | Interactive onboarding guide |
| `identity_set_persona_name` | Set assistant name |
| `identity_set_persona_description` | Set assistant description |
| `identity_add_trait` | Add a personality trait |
| `identity_add_value` | Add a guiding principle |
| `identity_add_preference` | Add a task preference |
| `identity_add_relationship` | Add a key relationship |
| `identity_add_antipattern` | Add a behavior to avoid |
| `identity_add_tone` | Add communication style directive |
| `identity_add_instruction_v2` | Add an operational instruction |
| `identity_add_directive` | Add a communication directive |
| `identity_add_expertise` | Add area of expertise |
| `identity_list` | List identity items by type |
| `identity_search` | Search identity content |
| `identity_remove` | Remove an identity item |

### References

| Tool | Description |
|------|-------------|
| `reference_list` | List loaded reference sources |
| `reference_search` | Full-text search with citations |
| `reference_get` | Get a section by exact title |
| `reference_sections` | Browse sections in a source |
| `reference_citation` | Get APA 7 citation |

### Lenses

| Tool | Description |
|------|-------------|
| `lenses_list` | List available lenses |
| `lenses_get` | Load a lens by name |

### Plans

| Tool | Description |
|------|-------------|
| `plans` | List active plans |
| `plan_get` | View plan with steps |
| `plan_start` | Create a new plan |
| `plan_stop` | Delete a plan |
| `step_add` | Add a step to a plan |
| `step_complete` | Mark a step done |

### Utilities

| Tool | Description |
|------|-------------|
| `config_get` | View current configuration |
| `config_set` | Update a config value |
| `date_resolve` | Resolve relative dates |
