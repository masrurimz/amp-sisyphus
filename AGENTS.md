# Agent Instructions

This project is **Amp Sisyphus** - a multi-agent orchestration system for Amp.

## Sisyphus Skills

Available skills in this project:

| Skill | Purpose | Trigger |
|-------|---------|---------|
| `sisyphus` | Main orchestrator - delegates, coordinates, verifies | Complex multi-step tasks |
| `prometheus` | Strategic planner - interviews, creates plans | Planning phase |
| `momus` | Critical reviewer - validates plans | Before implementation |
| `explorer` | Fast codebase search - parallel execution | Quick searches |
| `frontend-engineer` | UI/UX implementation specialist | Frontend tasks |
| `doc-writer` | Documentation specialist | Docs, comments, READMEs |
| `ultrawork` | Maximum performance mode | Comprehensive analysis |
| `git-master` | Clean git operations | Commits, PRs |
| `analyze` | Deep module investigation | Understanding code |

## Sisyphus Workflow

```
User Request → Prometheus (Plan) → Momus (Review) → Sisyphus (Execute) → Done
```

## Sisyphus State

- `.sisyphus/state.json` - Session state
- `.sisyphus/wisdom.md` - Accumulated learnings
- `.sisyphus/plans/` - Work plans
- `.sisyphus/notepads/` - Execution notes

## Issue Tracking

This project uses **bd** (beads) for issue tracking. Run `bd onboard` to get started.

## Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --status in_progress  # Claim work
bd close <id>         # Complete work
bd sync               # Sync with git
```

## Landing the Plane (Session Completion)

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd sync
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds

