# Amp Sisyphus

A multi-agent orchestration system for [Amp](https://ampcode.com) - ported from [oh-my-claude-sisyphus](https://github.com/Yeachan-Heo/oh-my-claude-sisyphus).

## Overview

Amp Sisyphus transforms Amp into a coordinated team of specialized agents that persistently work until complex, multi-step engineering tasks are fully complete and verified.

**The Sisyphean Promise**: The boulder rolls until it reaches the top - until EVERY task is COMPLETE.

## Features

- **9 Specialized Skills** - Integrated with Amp's built-in oracle, librarian, finder
- **Lifecycle Hooks** - Auto-continue, session recovery, verification reminders
- **Persistent State** - Survives session boundaries via wisdom accumulation
- **Magic Keywords** - `/ultrawork`, `/analyze`, `/git-master` triggers

## Built-in Tool Integration

Amp Sisyphus leverages Amp's powerful built-in tools:

| Amp Tool | How Sisyphus Uses It |
|----------|---------------------|
| `oracle` | Architecture decisions, code review, debugging (prometheus, sisyphus, analyze) |
| `librarian` | External documentation research (prometheus, ultrawork) |
| `finder` | Semantic codebase search (explorer, analyze, ultrawork) |
| `Task` | Spawn specialist subagents (sisyphus orchestrator) |
| `mermaid` | Visualize architecture and flows (analyze) |

## Installation

### Method 1: Install from GitHub

```bash
amp skill add masrurimz/amp-sisyphus
```

### Method 2: Manual Installation

1. Clone this repository:
```bash
git clone https://github.com/masrurimz/amp-sisyphus.git
```

2. Copy skills to your Amp skills directory:
```bash
cp -r amp-sisyphus/skills/* ~/.config/agents/skills/
```

3. Add hooks to your VS Code settings:
```json
{
  "amp.hooks": [
    // Copy contents from hooks/amp.hooks.json
  ]
}
```

## Skills

| Skill | Purpose |
|-------|---------|
| `sisyphus` | Main orchestrator - delegates, coordinates, verifies |
| `prometheus` | Strategic planner - interviews user, creates detailed plans |
| `momus` | Critical reviewer - validates plans before implementation |
| `explorer` | Fast codebase search with parallel execution |
| `frontend-engineer` | UI/UX implementation specialist |
| `doc-writer` | Documentation specialist |
| `ultrawork` | Maximum performance mode with parallel agents |
| `git-master` | Clean git operations - atomic commits, PRs |
| `analyze` | Deep module investigation |

## Workflow

```
┌─────────────────────────────────────────────────────────┐
│                    USER REQUEST                          │
└─────────────────────┬───────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────┐
│              PROMETHEUS (Planning)                       │
│  • Interview user for requirements                       │
│  • Create detailed plan in .sisyphus/plans/              │
└─────────────────────┬───────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────┐
│                MOMUS (Review)                            │
│  • Critical review of plan                               │
│  • Catch gaps, ambiguities, missing context              │
│  • APPROVE or REJECT with feedback                       │
└─────────────────────┬───────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────┐
│            SISYPHUS (Orchestration)                      │
│  • Break plan into atomic tasks                          │
│  • Delegate to specialists via Task tool                 │
│  • Verify completion before marking done                 │
│  • Never stop until ALL todos complete                   │
└─────────────────────┬───────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────┐
│               SPECIALISTS                                │
│  • Frontend Engineer (UI/UX)                             │
│  • Doc Writer (documentation)                            │
│  • Generic Task subagents                                │
└─────────────────────────────────────────────────────────┘
```

## Usage Examples

### Complex Feature Implementation

```
Use the sisyphus skill to implement user authentication with JWT tokens,
including login, logout, token refresh, and protected routes.
```

### Strategic Planning

```
Use the prometheus skill to plan a migration from REST to GraphQL.
Interview me about requirements first.
```

### Code Analysis

```
Use the analyze skill to understand how the payment processing module works.
```

### Maximum Performance

```
Use the ultrawork skill to audit the entire codebase for security vulnerabilities.
```

## Hooks

The hooks in `hooks/amp.hooks.json` provide:

| Hook | Purpose |
|------|---------|
| `sisyphus-ralph-loop` | Prevents stopping with incomplete todos |
| `sisyphus-session-start` | Loads state and wisdom at start |
| `sisyphus-plan-guard` | Ensures plans exist before implementation |
| `sisyphus-wisdom-capture` | Captures learnings before ending |
| `sisyphus-verification-reminder` | Reminds to verify before completing |

## Persistence

State is maintained in `.sisyphus/`:

```
.sisyphus/
├── state.json      # Session state (iteration count, active plan)
├── wisdom.md       # Accumulated learnings across sessions
├── plans/          # Work plans from Prometheus
│   ├── README.md
│   └── _template.md
└── notepads/       # Execution notes from subagents
    └── README.md
```

## Architecture

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for detailed mapping from original Sisyphus to Amp.

## Comparison with Original

| Feature | oh-my-claude-sisyphus | amp-sisyphus |
|---------|----------------------|--------------|
| Runtime | Claude Code | Amp |
| Agents | TypeScript classes | Amp Skills (SKILL.md) |
| Hooks | Custom TS hooks | Amp hooks (JSON) |
| LSP Tools | Custom implementation | Use Amp's finder/diagnostics |
| AST Tools | ast-grep | Grep + patterns |
| Persistence | .sisyphus/ JSON | .sisyphus/ + beads |

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT
