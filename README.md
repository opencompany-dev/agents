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

## agent.yaml Reference

```yaml
# Short description of the agent (used in listings, chat context, tools)
description: Strategic AI partner for founders and executives

# Skills this agent uses (must be subset of company skills)
skills:
  - opencompany/first-principles-thinking
  - opencompany/yc-group-partner-advice

# Instruction files from instructions/ directory
instructions:
  - soul.md
  - behavior.md

# Knowledge files from knowledge/ directory
knowledge: []

# Memory files from memory/ directory
memory:
  - memory.md
```

| Field | Required | Description |
|-------|----------|-------------|
| `description` | No | Short summary shown in agent listings and chat context. Falls back to first paragraph of AGENT.MD if not provided. |
| `skills` | No | List of skills the agent can use (must be available at company level) |
| `instructions` | No | Behavioral guidance files to include |
| `knowledge` | No | Agent-specific knowledge files |
| `memory` | No | Persistent state files |

## Creating an Agent

1. Create a new directory with your agent name
2. Add `AGENT.MD` (required) - defines core identity
3. Create subdirectories: `instructions/`, `knowledge/`, `memory/`
4. Optionally add `agent.yaml` with instructions, memory, skills
5. Update `index.yaml` with your agent entry
6. Submit a pull request

## License

MIT
