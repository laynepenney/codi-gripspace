# Codi - AI Coding Wingman

Multi-repo workspace for Codi development, managed by gitgrip.

## What is Codi?

Codi is an AI coding assistant for the terminal. It supports multiple AI providers (Claude, OpenAI, Ollama) and gives AI models access to filesystem tools, code search, and multi-agent orchestration.

Two implementations exist:
- **codi** (TypeScript) - Primary CLI with full feature set
- **codi-rs** (Rust) - Port with TUI, MCP support, and tree-sitter symbol index

## What is gitgrip?

gitgrip (`gr`) is a multi-repo workflow tool that manages synchronized branches, linked PRs, and atomic merges across repositories. This workspace is a gitgrip "gripspace".

## Repositories

| Repo | Path | Language | Description |
|------|------|----------|-------------|
| `codi` | `./codi` | TypeScript | Main CLI: agent loop, tools, commands, providers |
| `codi-rs` | `./codi-rs` | Rust | Rust port: TUI, MCP, symbol index |
| `gitgrip` | `./gitgrip` | Rust | Multi-repo orchestration tool |
| `opencode` | `./ref/opencode` | TypeScript | Reference: TUI patterns |
| `aider` | `./ref/aider` | Python | Reference: pair programming |
| `codex` | `./ref/codex` | TS + Rust | Reference: Rust patterns |

## Getting Started

```bash
source ./envsetup.sh       # Set up environment
gr sync                    # Pull latest from all repos
gr run build-all           # Build everything
gr run test-all            # Run all tests
```

## Development

```bash
# TypeScript codi
cd codi && pnpm dev

# Rust codi
cd codi-rs && cargo run

# gitgrip
cd gitgrip && cargo build
```

## Workflow

All git operations go through `gr`:

```bash
gr sync                              # Pull latest
gr branch feat/my-feature            # Branch across repos
gr add . && gr commit -m "feat: x"   # Commit
gr push -u                           # Push
gr pr create -t "feat: x" --push     # Create PRs
```

See `CLAUDE.md` for detailed workflow and `AGENTS.md` for multi-agent coordination.
