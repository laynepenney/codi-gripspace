# Codi Gripspace - Workspace Guide

Multi-repository workspace for **Codi**, the AI coding wingman, managed by **gitgrip**.

## Workspace Structure

| Repository | Path | Language | Description |
|------------|------|----------|-------------|
| `codi` | `./codi` | TypeScript | Main CLI application |
| `codi-rs` | `./codi-rs` | Rust | Rust port of codi |
| `gitgrip` | `./gitgrip` | Rust | Multi-repo orchestration tool |

### Reference Repositories (Read-Only)

| Repository | Path | Language | Use For |
|------------|------|----------|---------|
| `opencode` | `./ref/opencode` | TypeScript | TUI patterns, agent architecture |
| `aider` | `./ref/aider` | Python | Terminal AI pair programming |
| `codex` | `./ref/codex` | TypeScript + Rust | Rust reference patterns |

## Quick Start

```bash
# Set up environment (every session)
source ./envsetup.sh

# Build everything
gr run build-all

# Or build individually
gr run build-ts     # TypeScript codi
gr run build-rs     # Rust codi
gr run build-gr     # gitgrip
```

## Build / Dev / Test

### Codi TypeScript

```bash
cd codi
pnpm install && pnpm build    # Build
pnpm dev                       # Dev mode
pnpm test                      # Tests
```

### Codi Rust

```bash
cd codi-rs
cargo build                    # Build
cargo test                     # Tests
cargo clippy                   # Lint
```

### gitgrip

```bash
cd gitgrip
cargo build                    # Build
cargo test                     # Tests
cargo clippy                   # Lint
```

## Environment (envsetup.sh)

Source `envsetup.sh` to get shell functions:

| Command | Description |
|---------|-------------|
| `codi-build` / `codi-build-all` | Build TypeScript + Rust |
| `codi-dev` | Run TypeScript codi in dev mode |
| `codi-dev-rs` | Run Rust codi |
| `codi-test` / `codi-test-rs` | Run tests |
| `cdc` / `cdcr` / `cdg` / `cdw` | Navigate to codi / codi-rs / gitgrip / workspace root |

## CRITICAL: Always Use `gr`

**NEVER use raw `git` or `gh` commands.** Always use `gr` for ALL operations.

```
WRONG:    git checkout -b feat/x
CORRECT:  gr branch feat/x

WRONG:    git add . && git commit -m "msg"
CORRECT:  gr add . && gr commit -m "msg"

WRONG:    gh pr create --title "msg"
CORRECT:  gr pr create -t "msg" --push
```

### Standard Workflow

```bash
gr sync                              # Pull latest
gr branch feat/my-feature            # Branch across ALL repos
# ... make changes ...
gr add . && gr commit -m "feat: x"   # Stage + commit
gr push -u                           # Push
gr pr create -t "feat: x" --push     # Create linked PRs
# After merge:
gr checkout --base && gr sync        # Return + pull
gr prune --execute                   # Cleanup merged branches
```

### Workflow Rules

1. Always `gr sync` before starting new work
2. Always `gr branch` to create branches across repos
3. Use `gr add`, `gr commit`, `gr push` - not raw git
4. Always use pull requests - no direct pushes to main
5. After merge: `gr checkout --base && gr sync && gr prune --execute`

## Per-Repository Docs

Each repo has detailed guides:

- `codi/CLAUDE.md` - Codi TypeScript architecture and conventions
- `gitgrip/CLAUDE.md` - gitgrip development guide and command reference
- `codi-rs/` - Rust port (see cargo docs)

## Agent Context

Run `gr agent context` to get a full workspace context dump for AI agents.
Run `gr agent context --json` for machine-readable output.

## `gr run` Scripts

```bash
gr run --list          # Show all scripts
gr run build-all       # Build everything
gr run test-all        # Run all tests
gr run dev-ts          # Dev mode (TypeScript)
gr run dev-rs          # Dev mode (Rust)
```
