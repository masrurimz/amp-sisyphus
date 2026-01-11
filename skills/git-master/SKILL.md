# Git Master Skill

Specialized skill for clean git operations: atomic commits, clean PRs, proper history.

## Trigger

Use when you need to:
- Create atomic, well-organized commits
- Prepare a clean PR
- Manage git history

## Principles

### 1. Atomic Commits

Each commit should:
- Do ONE thing
- Be self-contained
- Have a clear message
- Pass all tests independently

### 2. Commit Message Format

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

**Types**: feat, fix, docs, style, refactor, test, chore

**Examples**:
```
feat(auth): add JWT token refresh endpoint
fix(api): handle null response in user lookup
docs(readme): add installation instructions
refactor(db): extract connection pooling logic
```

### 3. PR Preparation

Before creating PR:
1. Rebase on latest main
2. Squash fixup commits
3. Ensure each commit passes CI
4. Write comprehensive PR description

## Workflow

### Stage Changes Atomically

```bash
# Stage related changes only
git add -p  # Interactive staging

# Commit with clear message
git commit -m "type(scope): description"
```

### Clean Up History

```bash
# Interactive rebase to squash/reorder
git rebase -i main

# Fixup minor corrections into parent commit
git commit --fixup <commit>
git rebase -i --autosquash main
```

### PR Description Template

```markdown
## Summary
[What does this PR do?]

## Changes
- Change 1
- Change 2

## Testing
- [ ] Tests pass
- [ ] Manual verification done

## Screenshots (if UI)
[Before/After]
```

## Anti-Patterns

❌ Giant commits with unrelated changes
❌ "WIP" or "fix" commit messages
❌ Merge commits when rebase is cleaner
❌ Force-pushing shared branches

## Integration

Works with Sisyphus workflow:
1. Sisyphus completes task
2. Git Master creates atomic commit
3. Repeat until PR-ready
4. Git Master prepares PR
