# Analyze Skill

Deep-dive investigation into a specific module or component.

## Trigger

Use when you need to:
- Understand how a complex module works
- Find the root cause of a bug
- Map dependencies and relationships
- Prepare for refactoring

## Behavior

### Phase 1: Discovery

1. **Find the entry point**
   - Main file/function
   - Public API surface

2. **Map the structure**
   - Files in the module
   - Key classes/functions
   - Configuration

3. **Identify dependencies**
   - Internal imports
   - External packages
   - Shared utilities

### Phase 2: Deep Analysis

1. **Data flow**
   - Input → Processing → Output
   - State transformations
   - Side effects

2. **Control flow**
   - Decision points
   - Error handling
   - Edge cases

3. **Integration points**
   - How other modules use this
   - Events emitted/consumed
   - API contracts

### Phase 3: Documentation

1. **Create diagram**
   - Use Mermaid for visualization
   - Show relationships clearly

2. **Write summary**
   - Purpose and responsibility
   - Key algorithms
   - Known issues

3. **Record in wisdom**
   - Update `.sisyphus/wisdom.md`
   - Add to accumulated knowledge

## Output Format

```markdown
# Analysis: [Module Name]

## Purpose
[One-paragraph summary]

## Architecture
[Mermaid diagram]

## Key Components
| Component | Responsibility |
|-----------|---------------|
| ... | ... |

## Data Flow
[Description or diagram]

## Dependencies
- Depends on: ...
- Used by: ...

## Issues Found
- Issue 1
- Issue 2

## Recommendations
- Recommendation 1
- Recommendation 2
```

## Usage

```
/analyze "the authentication middleware"
/analyze "src/services/payment/"
```

## Integration

- Uses Explorer for fast search
- Uses Oracle for architecture insights
- Updates wisdom.md with findings
