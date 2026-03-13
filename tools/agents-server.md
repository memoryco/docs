# Agents Server

The agents server lets you spawn and manage background Claude Code instances. Think of it as a task runner where each task gets its own AI-powered worker.

## Tools

| Tool | Description |
|------|-------------|
| `agent_spawn` | Start a background agent with a working directory and prompt |
| `agent_list` | List all agents with status (running, completed, orphaned) |
| `agent_status` | Detailed view of an agent including output and activity log |
| `agent_respond` | Send a follow-up message to a running agent |
| `agent_kill` | Terminate a running agent |
| `agent_types_list` | List available agent type definitions |
| `agent_types_get` | Get a specific agent type's system prompt |

## Workflow

```
1. agent_spawn   → start a task in a specific directory
2. agent_list    → check on all agents
3. agent_status  → see detailed output and activity
4. agent_respond → give guidance if needed
5. agent_kill    → stop a stuck agent
```

## Agent Types

Agent types are predefined system prompts stored in `~/.claude/agents/`. They let you create specialized agents for common tasks — code review, refactoring, documentation, testing, etc.

## Constraints

- One agent per working directory (prevents conflicts)
- Agents inherit your Claude authentication
- Agents use the `--allowedTools` flag for security
- Recursive agent spawning is blocked
