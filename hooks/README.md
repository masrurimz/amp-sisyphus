# Amp Sisyphus Hooks

This directory contains Amp hooks that implement the Sisyphean workflow.

## Hooks Overview

| Hook ID | Event | Purpose |
|---------|-------|---------|
| `sisyphus-ralph-loop` | `Stop` | Prevents stopping with incomplete todos |
| `sisyphus-session-start` | `UserPromptSubmit` | Loads state and wisdom at start |
| `sisyphus-plan-guard` | `tool:pre-execute` (Task) | Ensures plans exist before implementation |
| `sisyphus-wisdom-capture` | `Stop` | Captures learnings before ending |
| `sisyphus-verification-reminder` | `tool:pre-execute` (todo_write) | Reminds to verify before completing |

## Installation

Copy `amp.hooks.json` to your VS Code settings or add to your Amp configuration:

```json
// In VS Code settings.json or Amp config
{
  "amp.hooks": [
    // ... hooks from amp.hooks.json
  ]
}
```

Or reference in your project's `.vscode/settings.json`:

```json
{
  "amp.hooks": "@./hooks/amp.hooks.json"
}
```

## How It Works

### Ralph Loop (The Sisyphean Promise)

When the agent attempts to stop, the hook checks if todos are complete:
- If incomplete items exist → continue working
- If all items complete → allow stop

This ensures work is never abandoned mid-task.

### Session Start

On first prompt, reminds the agent to:
1. Load accumulated wisdom from previous sessions
2. Check for in-progress work
3. Resume where the last session left off

### Plan Guard

Before executing implementation tasks:
1. Verify a plan exists
2. Ensure Momus has reviewed it
3. Block implementation without approved plan

### Wisdom Capture

Before ending, prompts the agent to document:
- What was learned
- Problems and solutions
- Key decisions
- Reusable patterns

This builds institutional knowledge across sessions.
