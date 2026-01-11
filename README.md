# Amp Sisyphus

A multi-agent orchestration system for [Amp](https://ampcode.com) - ported from [oh-my-claude-sisyphus](https://github.com/Yeachan-Heo/oh-my-claude-sisyphus).

## Overview

Amp Sisyphus transforms Amp into a coordinated team of specialized agents that persistently work until complex, multi-step engineering tasks are fully complete and verified.

## Features

- **11 Specialized Agents** - Oracle, Librarian, Explorer, Prometheus, Momus, and more
- **Lifecycle Hooks** - Auto-continue, context recovery, rules injection
- **Persistent State** - Survives session boundaries via beads integration
- **Magic Keywords** - `/ultrawork`, `/analyze`, `/git-master` triggers

## Architecture

```
amp-sisyphus/
├── skills/           # Agent definitions as Amp skills
│   ├── oracle/       # Deep reasoning & architecture
│   ├── librarian/    # External research
│   ├── explorer/     # Fast codebase recon
│   ├── prometheus/   # Strategic planning
│   ├── momus/        # Critical review
│   └── sisyphus/     # Main orchestrator
├── hooks/            # Amp lifecycle hooks
│   ├── ralph-loop/   # Auto-continue until complete
│   ├── context-recovery/
│   └── rules-injector/
├── tools/            # Custom tool implementations
└── .beads/           # Persistent state
```

## Installation

```bash
amp skill add masrurimz/amp-sisyphus
```

## Usage

```bash
# Start with planning
/prometheus "Refactor the authentication module"

# Direct orchestration
/sisyphus "Fix all TypeScript errors and add tests"

# Maximum performance mode
/ultrawork "Complete codebase audit"
```

## License

MIT
