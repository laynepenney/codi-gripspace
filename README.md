# codi-gripspace

Multi-repository workspace for [Codi](https://github.com/laynepenney/codi), the AI coding wingman. Managed by [gitgrip](https://github.com/laynepenney/gitgrip).

## What's in this workspace

| Repo | Language | Description |
|------|----------|-------------|
| [codi](https://github.com/laynepenney/codi) | TypeScript + Rust | AI coding wingman CLI |
| [gitgrip](https://github.com/laynepenney/gitgrip) | Rust | Multi-repo workflow tool |
| [opencode](https://github.com/anomalyco/opencode) | TypeScript | Reference: TUI patterns |
| [aider](https://github.com/Aider-AI/aider) | Python | Reference: AI pair programming |
| [codex](https://github.com/openai/codex) | TypeScript + Rust | Reference: Rust patterns |

## Quick Start

```bash
# Install gitgrip
brew install laynepenney/tap/gitgrip
# or: cargo install gitgrip

# Initialize workspace
gr init https://github.com/laynepenney/codi-gripspace.git
cd codi-gripspace

# Set up environment
source ./envsetup.sh

# Build everything
gr run build-all
```

## Available Scripts

```bash
gr run --list         # List all scripts
gr run build-ts       # Build codi (TypeScript)
gr run build-rs       # Build codi (Rust)
gr run build-gr       # Build gitgrip
gr run build-all      # Build everything
gr run test-all       # Run all tests
```

## Development Workflow

```bash
gr sync                              # Pull latest
gr branch feat/my-feature            # Branch across all repos
# ... make changes ...
gr add . && gr commit -m "feat: x"   # Commit across repos
gr pr create -t "feat: x" --push     # Create linked PRs
```

See [CODI.md](CODI.md) for full workspace documentation.

## AI Tool Integration

This workspace includes skill files for multiple AI coding tools:
- **Claude Code**: `.claude/skills/` (synced via linkfile from repos)
- **OpenCode**: `.opencode/skill/` (in manifest)
- **Codex**: `.codex/skills/` (in manifest)
