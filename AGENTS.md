# Multi-Agent Guide - Codi Workspace

Guidelines for AI agents working in this multi-repo workspace.

## Workspace Discovery

```bash
# Get full agent context (markdown for system prompts)
gr agent context

# Machine-readable context
gr agent context --json

# Per-repo build/test commands
gr agent build          # Build repos with agent config
gr agent test           # Test repos with agent config

# Verify workspace state
gr agent verify         # Check all repos are clean and on expected branches
```

## Repo Responsibilities

| Repo | Language | What To Change |
|------|----------|----------------|
| `codi` | TypeScript | CLI features, commands, tools, providers, agent loop |
| `codi-rs` | Rust | Rust port: TUI, MCP, symbol index, providers |
| `gitgrip` | Rust | Multi-repo workflow: commands, platform adapters, manifest |

Reference repos (`ref/*`) are **read-only** - use for architecture patterns only.

## Build & Test Quick Reference

```bash
# Per-repo
cd codi && pnpm install && pnpm build && pnpm test
cd codi-rs && cargo build && cargo test && cargo clippy
cd gitgrip && cargo build && cargo test && cargo clippy

# Workspace-wide
gr run build-all
gr run test-all
```

## Git Workflow for Agents

**Use `gr` for everything. Never raw `git` or `gh`.**

```bash
# Before starting work
gr sync
gr status

# Create feature branch (spans ALL repos)
gr branch feat/my-feature

# After making changes
gr add .
gr commit -m "feat: description"
gr push -u
gr pr create -t "feat: description" --push

# After PR merge
gr checkout --base
gr sync
gr prune --execute
```

## Multi-Agent Coordination

When multiple agents work in this workspace:

1. **Use griptrees for isolation** - each agent gets its own worktree:
   ```bash
   gr tree add feat/agent-task
   # Creates isolated workspace at ../feat-agent-task/
   ```

2. **Never work on the same branch** - git worktrees enforce branch exclusivity

3. **Check status before acting**:
   ```bash
   gr status          # Are repos clean?
   gr agent verify    # Is workspace healthy?
   ```

4. **Communicate via PRs** - create PRs for review rather than pushing directly

## Conventions

- TypeScript: ES Modules (.js imports), async/await, Vitest
- Rust: anyhow errors, tokio runtime, clippy clean
- Commits: conventional commits (`feat:`, `fix:`, `chore:`)
- Branches: `feat/*`, `fix/*`, `chore/*`
- PRs always target `main`

## Context Files

| File | Format | Purpose |
|------|--------|---------|
| `CLAUDE.md` | Markdown | Claude Code workspace instructions |
| `AGENTS.md` | Markdown | Multi-agent coordination (this file) |
| `CODI.md` | Markdown | General workspace overview |
| `.claude/skills/*/SKILL.md` | Frontmatter + MD | Claude Code per-repo skills |
| `.opencode/skill/*/SKILL.md` | Frontmatter + MD | OpenCode per-repo skills |
| `.codex/skills/*/SKILL.md` | Frontmatter + MD | Codex per-repo skills |
| `gripspace.yaml` | YAML | Manifest with agent config sections |
