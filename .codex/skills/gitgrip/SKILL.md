---
name: gitgrip
description: Multi-repository workflow using gitgrip (gr). Use when working with multiple repos, creating branches, syncing, or creating linked pull requests.
---

# gitgrip Multi-Repository Workflow

Always use `gr` commands for git operations across repos. Never use raw `git` or `gh`.

## Essential Commands

```bash
gr status                    # Check status
gr sync                      # Pull latest from all repos
gr branch feat/my-feature    # Create branch across ALL repos
gr checkout feat/my-feature  # Switch branch across repos
gr add .                     # Stage all changes
gr commit -m "message"       # Commit across repos
gr push -u                   # Push with upstream tracking
gr diff                      # Show diff across repos
```

## PR Workflow

```bash
gr pr create -t "title" --push   # Create linked PRs
gr pr status                     # Check PR status
gr pr checks                     # Check CI status
gr pr merge                      # Merge all linked PRs
```

## Post-Merge Cleanup

```bash
gr checkout --base           # Return to base branch
gr sync                      # Pull latest
gr prune --execute           # Delete merged branches
```

## Griptrees (Parallel Workspaces)

```bash
gr tree add feat/auth        # Create griptree
gr tree list                 # List all griptrees
gr tree lock feat/auth       # Protect from removal
gr tree remove feat/auth     # Cleanup when done
```

## Rules

1. Always `gr sync` before starting new work
2. Always use `gr branch` for branches
3. Always use pull requests - no direct pushes to main
4. Never use raw `git` or `gh` commands
5. After merge: `gr checkout --base && gr sync && gr prune --execute`
