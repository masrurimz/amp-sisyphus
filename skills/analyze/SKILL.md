---
name: analyze
description: Deep module investigation using Amp's finder for discovery, oracle for expert analysis, and mermaid for visualization. Use when you need to understand complex code, prepare for refactoring, or debug issues.
---

# Analyze: Deep Module Investigation

Comprehensive code analysis using **Amp's built-in tools**.

## Tools Used

| Tool | Purpose |
|------|---------|
| `finder` | Semantic search to discover relevant code |
| `oracle` | Expert analysis of architecture, patterns, issues |
| `mermaid` | Visualize relationships and flows |
| `Read` | Get full file contents |
| `Grep` | Find exact patterns |

## Analysis Workflow

```
┌─────────────────────────────────────────────────────┐
│                 ANALYZE WORKFLOW                     │
├─────────────────────────────────────────────────────┤
│                                                      │
│  Phase 1: DISCOVERY                                  │
│  ┌─────────────────────────────────────────────┐    │
│  │ finder("how does [module] work?")           │    │
│  │ glob("[module]/**/*")                       │    │
│  │ Grep("import.*from.*[module]")              │    │
│  └─────────────────────────────────────────────┘    │
│                      ↓                               │
│  Phase 2: DEEP READ                                  │
│  ┌─────────────────────────────────────────────┐    │
│  │ Read(discovered_files)                      │    │
│  │ Map: exports, imports, dependencies         │    │
│  └─────────────────────────────────────────────┘    │
│                      ↓                               │
│  Phase 3: EXPERT ANALYSIS                            │
│  ┌─────────────────────────────────────────────┐    │
│  │ oracle(                                     │    │
│  │   task: "Analyze architecture of [module]", │    │
│  │   files: [key_files]                        │    │
│  │ )                                           │    │
│  └─────────────────────────────────────────────┘    │
│                      ↓                               │
│  Phase 4: VISUALIZATION                              │
│  ┌─────────────────────────────────────────────┐    │
│  │ mermaid(architecture_diagram)               │    │
│  │ mermaid(data_flow_diagram)                  │    │
│  └─────────────────────────────────────────────┘    │
│                      ↓                               │
│  Phase 5: DOCUMENT                                   │
│  ┌─────────────────────────────────────────────┐    │
│  │ Update .sisyphus/wisdom.md with findings    │    │
│  └─────────────────────────────────────────────┘    │
│                                                      │
└─────────────────────────────────────────────────────┘
```

## Phase Details

### Phase 1: Discovery

Use `finder` for semantic search:

```
finder("How does the authentication module work?")
finder("What are the entry points for the payment system?")
finder("Find all components that depend on UserContext")
```

Parallel with structural search:
```
glob("src/auth/**/*")
Grep("export.*from.*auth", path="src")
```

### Phase 2: Deep Read

Read key files identified in discovery:
```
Read("src/auth/index.ts")
Read("src/auth/middleware.ts")
Read("src/auth/types.ts")
```

Map the module structure:
- Main entry point
- Public exports
- Internal dependencies
- External dependencies

### Phase 3: Expert Analysis

**USE `oracle`** for expert-level analysis:

```
oracle(
  task: "Analyze the authentication module architecture",
  context: "I need to understand:
    - How authentication flow works
    - Security considerations
    - Potential issues or improvements
    - Integration points with other modules",
  files: ["src/auth/index.ts", "src/auth/middleware.ts"]
)
```

Oracle excels at:
- Finding architectural issues
- Identifying security vulnerabilities
- Suggesting improvements
- Understanding complex flows

### Phase 4: Visualization

**USE `mermaid`** to create diagrams:

```
mermaid(
  code: "flowchart TD
    A[Request] --> B[Auth Middleware]
    B --> C{Token Valid?}
    C -->|Yes| D[Route Handler]
    C -->|No| E[401 Response]",
  citations: {
    "Auth Middleware": "file:///src/auth/middleware.ts#L15-L45",
    "Route Handler": "file:///src/routes/index.ts#L20"
  }
)
```

Create diagrams for:
- Component relationships
- Data flow
- State transitions
- Sequence diagrams

### Phase 5: Document

Record findings in `.sisyphus/wisdom.md`:

```markdown
## Analysis: Authentication Module (2026-01-11)

### DISCOVERIES
- Auth uses JWT with RS256 algorithm
- Token refresh handled via /api/refresh endpoint
- Middleware attached to all /api/* routes

### ISSUES
- No rate limiting on login endpoint
- Token expiry too long (24h)

### DECISIONS
- Consider implementing refresh token rotation

### PATTERNS
- Middleware pattern: validate → decode → attach to req.user
```

## Output Format

```markdown
# Analysis: [Module Name]

## Purpose
[One-paragraph summary of what this module does]

## Architecture
[Mermaid diagram - rendered via mermaid tool]

## Key Components

| Component | File | Responsibility |
|-----------|------|----------------|
| AuthMiddleware | src/auth/middleware.ts | Request validation |
| TokenService | src/auth/token.ts | JWT operations |

## Data Flow

[Description or sequence diagram]

## Dependencies

**Depends on:**
- src/config (JWT secrets)
- src/db (user lookup)

**Used by:**
- All protected API routes
- WebSocket authentication

## Oracle Analysis

[Summary of oracle's expert review]

## Issues Found
- [ ] Issue 1: [description]
- [ ] Issue 2: [description]

## Recommendations
1. [Recommendation with rationale]
2. [Recommendation with rationale]

## Wisdom Captured
[Note that findings were recorded in .sisyphus/wisdom.md]
```

## Quick Reference

```bash
# Typical analyze session
1. finder("how does X work")        # Discover
2. Read(found_files)                # Deep read
3. oracle(analyze X, files=[...])   # Expert review
4. mermaid(architecture)            # Visualize
5. Update wisdom.md                 # Document
```

## Anti-Patterns

❌ Skipping oracle (you lose expert analysis)
❌ No visualization (diagrams clarify understanding)
❌ Not documenting (findings get lost)
❌ Only using Grep (miss semantic understanding)

## The Analyze Mantra

```
finder discovers, oracle analyzes, mermaid visualizes.
Document everything. Build institutional knowledge.
```
