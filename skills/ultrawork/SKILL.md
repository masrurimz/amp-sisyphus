# Ultrawork Skill

Activates maximum performance mode with parallel agent execution.

## Trigger

Use when you need comprehensive, fast results across multiple dimensions:
- Deep codebase analysis
- Multi-faceted research
- Parallel implementation tasks

## Behavior

When activated, Sisyphus will:

1. **Spawn parallel research agents**:
   - Explorer → Fast codebase search
   - Librarian (built-in) → External documentation
   - Oracle (built-in) → Architecture analysis

2. **Run searches in parallel**:
   - Multiple Grep calls simultaneously
   - Multiple glob patterns at once
   - Parallel file reads

3. **Synthesize results**:
   - Combine findings from all agents
   - Prioritize by relevance
   - Present unified view

## Usage

```
/ultrawork "Analyze the authentication system and find all security vulnerabilities"
```

## Parallel Execution Pattern

```
┌─────────────────────────────────────────────────────┐
│                    ULTRAWORK                         │
├─────────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐          │
│  │ Explorer │  │ Librarian│  │  Oracle  │          │
│  │ (search) │  │ (docs)   │  │ (arch)   │          │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘          │
│       │             │             │                 │
│       ▼             ▼             ▼                 │
│  ┌─────────────────────────────────────┐           │
│  │         SYNTHESIS LAYER              │           │
│  │   Combine, dedupe, prioritize        │           │
│  └─────────────────────────────────────┘           │
│                     │                               │
│                     ▼                               │
│            Unified Results                          │
└─────────────────────────────────────────────────────┘
```

## Anti-Patterns

❌ Don't use for simple, focused tasks
❌ Don't use when sequential dependency exists
❌ Don't spawn more than 5 parallel agents

## When to Use

✅ "Audit the entire codebase for X"
✅ "Find all instances of pattern Y across docs and code"
✅ "Research best practices and find our current implementation"
