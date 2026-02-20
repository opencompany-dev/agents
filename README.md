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
├── BOOTSTRAP.md          # First-run setup (optional)
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
| `BOOTSTRAP.md` | No | First-run onboarding — agent deletes after setup |
| `agent.yaml` | No | Configuration (skills, instructions, memory) |
| `instructions/` | No | Instruction files referenced in yaml |
| `knowledge/` | No | Agent-specific knowledge files |
| `memory/` | No | Persistent memory state |

## Bootstrap Flow

Agents can include a `BOOTSTRAP.md` for first-run onboarding:

1. Agent checks if `BOOTSTRAP.md` exists
2. If yes — follows it to get to know the user, establish working style
3. Updates `memory/` and `instructions/` based on what it learns
4. Deletes `BOOTSTRAP.md` when done

This creates a personalized first experience without interrogating users with forms.

## Dynamic Session Preamble

The CLI automatically generates an "Every Session" section based on `agent.yaml`. This tells the agent which files to read at the start of each session.

**You don't need to hardcode file lists in AGENT.MD** — the CLI generates them from your config:

```markdown
## Every Session

Before doing anything else, read these files:

**Instructions** — who you are and how you work
- `instructions/soul.md`
- `instructions/behavior.md`

**Memory** — your persistent context
- `memory/memory.md`

**Knowledge** — facts and context
- `company/knowledge/values.md`

Don't ask permission. Just do it.
```

This keeps `agent.yaml` as the single source of truth. Add or remove files from the yaml, and the session preamble updates automatically.

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
2. Add `AGENT.MD` (required) — defines core identity and session behavior
3. Optionally add `BOOTSTRAP.md` — first-run onboarding flow
4. Create subdirectories: `instructions/`, `knowledge/`, `memory/`
5. Optionally add `agent.yaml` with instructions, memory, skills
6. Update `index.yaml` with your agent entry
7. Submit a pull request

## License

MIT
