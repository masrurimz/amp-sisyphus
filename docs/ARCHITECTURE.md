# Amp Sisyphus Architecture

## Overview

Port of [oh-my-claude-sisyphus](https://github.com/Yeachan-Heo/oh-my-claude-sisyphus) to [Amp](https://ampcode.com).

## Component Mapping

### Amp Built-in Subagents (USE DIRECTLY)

Amp has specialized subagents powered by different models:

| Subagent | Model | Purpose | Used By Skills |
|----------|-------|---------|----------------|
| `oracle` | GPT-5.1 | Complex reasoning, architecture review, debugging | prometheus, sisyphus, ultrawork, analyze |
| `librarian` | Claude Sonnet 4.5 | External documentation, library research | prometheus, ultrawork |
| `Search` | Gemini 3 Flash | Fast semantic codebase retrieval | explorer, ultrawork, analyze |

These are Amp's built-in tools that Sisyphus skills leverage:

| Amp Tool | Purpose | Used By |
|----------|---------|---------|
| `oracle` | Expert reasoning, architecture review, debugging | prometheus, sisyphus, ultrawork, analyze |
| `librarian` | External documentation, library research | prometheus, ultrawork |
| `Search` | Semantic codebase search | explorer, ultrawork, analyze |
| `Task` | Spawn subagent for implementation | sisyphus |
| `todo_write` | Track task progress | sisyphus |
| `mermaid` | Create diagrams | analyze |
| `Grep` | Exact pattern matching | explorer |
| `glob` | File pattern discovery | explorer |
| `Read` | Read file contents | all |
| `edit_file` / `create_file` | Modify files | frontend-engineer, doc-writer |

### Agents → Amp Skills

| Sisyphus Agent | Amp Skill | Integration |
|----------------|-----------|-------------|
| Oracle | Uses `oracle` tool | Built-in - no custom skill needed |
| Librarian | Uses `librarian` tool | Built-in - no custom skill needed |
| Explore | `explorer` | Uses `Search` + `Grep` + `glob` |
| Prometheus | `prometheus` | Uses `oracle`, `librarian`, `Search` |
| Momus | `momus` | Read-only reviewer |
| Sisyphus Orchestrator | `sisyphus` | Uses `Task`, `oracle`, `librarian` |
| Sisyphus Junior | N/A | Use `Task` tool directly |
| Frontend Engineer | `frontend-engineer` | Full file access |
| Document Writer | `doc-writer` | Documentation focus |

### Hooks Mapping

| Sisyphus Hook | Amp Hook Event | Action Type |
|---------------|----------------|-------------|
| Ralph Loop | `Stop` | `send-user-message` (continue prompt) |
| Context Recovery | `tool:post-execute` | `send-user-message` |
| Rules Injector | `UserPromptSubmit` | `send-user-message` |
| Svelte Guard (example) | `tool:pre-execute` | `send-user-message` |

### Tools Mapping

| Sisyphus Tool | Amp Equivalent | Notes |
|---------------|----------------|-------|
| Read | `Read` | Built-in |
| Grep | `Grep` | Built-in |
| Glob | `glob` | Built-in |
| Write | `create_file` | Built-in |
| Edit | `edit_file` | Built-in |
| Bash | `Bash` | Built-in |
| WebSearch | `web_search` | Built-in |
| WebFetch | `read_web_page` | Built-in |
| TodoWrite | `todo_write` | Built-in |
| Task | `Task` | Built-in (for subagents) |
| lsp_diagnostics | `get_diagnostics` | Built-in (via IDE) |
| lsp_hover | N/A | Not exposed |
| lsp_goto_definition | `Search` | Semantic search alternative |
| ast_grep_search | `Grep` + patterns | Use regex patterns |
| ast_grep_replace | `edit_file` | Manual structural edits |

### Persistence Mapping

| Sisyphus | Amp Sisyphus |
|----------|--------------|
| `.sisyphus/ralph-state.json` | `.sisyphus/state.json` |
| `.sisyphus/plans/*.md` | `.sisyphus/plans/*.md` |
| `.sisyphus/notepads/*.md` | `.sisyphus/notepads/*.md` |
| `.sisyphus/wisdom.md` | `.sisyphus/wisdom.md` |

## Directory Structure

```
amp-sisyphus/
├── skills/
│   ├── sisyphus/          # Main orchestrator
│   │   └── SKILL.md
│   ├── prometheus/        # Strategic planner
│   │   └── SKILL.md
│   ├── momus/             # Critical reviewer
│   │   └── SKILL.md
│   ├── explorer/          # Fast codebase search
│   │   └── SKILL.md
│   ├── frontend-engineer/ # UI/UX specialist
│   │   └── SKILL.md
│   └── doc-writer/        # Documentation specialist
│       └── SKILL.md
├── hooks/
│   └── amp.hooks.json     # Amp hooks configuration
├── .sisyphus/             # Runtime state (gitignored)
│   ├── state.json
│   ├── plans/
│   ├── notepads/
│   └── wisdom.md
└── AGENTS.md              # Project guidance
```

## Key Behaviors

### 1. Sisyphean Promise (Ralph Loop)

The core behavior: **Never stop until all todos are complete**.

Implemented via Amp hook on `Stop` event that checks:
1. Are there incomplete todos?
2. Has the completion promise been output?
3. Is max iteration limit reached?

If work remains, inject continuation prompt.

### 2. Delegation Pattern

Orchestrator Sisyphus NEVER implements directly. It:
1. Breaks work into atomic tasks
2. Creates todo list via `todo_write`
3. Delegates via `Task` tool to specialists
4. Verifies completion before marking done

### 3. Planning Flow

```
User Request
    ↓
Prometheus (Interview → Plan)
    ↓
Momus (Critical Review)
    ↓ (iterate until approved)
Sisyphus Orchestrator (Execute Plan)
    ↓
Task subagents (Implement)
    ↓
Verification & Completion
```

### 4. Accumulated Wisdom

Learnings from each session stored in `.sisyphus/wisdom.md`:
- Discoveries made
- Issues encountered
- Decisions taken
- Patterns identified

Read at session start, updated throughout.
