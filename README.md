# OpenCompany Agents Registry

Pre-configured agents for OpenCompany.

## Available Agents

| Agent | Description |
|-------|-------------|
| `co-ceo` | Strategic AI partner for founders and executives |

## Installation

```bash
# List available agents
oc agent list

# Install an agent
oc agent add co-ceo

# Use the agent
oc spawn co-ceo
```

## Agent Structure

Each agent directory contains:

```
agent-name/
├── AGENT.MD              # Core identity (required)
├── agent.yaml            # Configuration
├── instructions/         # Behavioral guidance
│   ├── soul.md
│   └── behavior.md
├── knowledge/            # Agent-specific context
└── memory/               # Persistent state
    └── memory.md
```

| Component | Required | Purpose |
|-----------|----------|---------|
| `AGENT.MD` | Yes | Core identity (WHO the agent IS) |
| `agent.yaml` | No | Configuration (skills, instructions, memory) |
| `instructions/` | No | Instruction files referenced in yaml |
| `knowledge/` | No | Agent-specific knowledge files |
| `memory/` | No | Persistent memory state |

## Creating an Agent

1. Create a new directory with your agent name
2. Add `AGENT.MD` (required) - defines core identity
3. Create subdirectories: `instructions/`, `knowledge/`, `memory/`
4. Optionally add `agent.yaml` with instructions, memory, skills
5. Update `index.yaml` with your agent entry
6. Submit a pull request

## License

MIT
