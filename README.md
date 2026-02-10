# codi-gripspace

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![gitgrip](https://img.shields.io/badge/managed%20by-gitgrip-blue.svg)](https://github.com/laynepenney/gitgrip)

Multi-repository workspace for [Codi](https://github.com/laynepenney/codi), the AI coding wingman. Managed by [gitgrip](https://github.com/laynepenney/gitgrip).

## What's in this workspace

| Repo | Language | Description |
|------|----------|-------------|
| [codi](https://github.com/laynepenney/codi) | TypeScript | AI coding wingman CLI (main) |
| [codi-rs](https://github.com/laynepenney/codi-rs) | Rust | Rust port of codi |
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

## Contributing

This is a workspace manifest repository. For contributions to individual projects, see their respective repos:
- **Codi**: https://github.com/laynepenney/codi
- **Codi (Rust)**: https://github.com/laynepenney/codi-rs
- **gitgrip**: https://github.com/laynepenney/gitgrip

For workspace changes (manifest, documentation, skill files):
1. Fork this repository
2. Create a branch: `git checkout -b feat/your-change`
3. Make changes
4. Submit a PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.

## License

This workspace is licensed under the [MIT License](LICENSE).

Individual projects in this workspace have their own licenses:
- **codi**: AGPL-3.0 or Commercial
- **codi-rs**: AGPL-3.0 or Commercial
- **gitgrip**: MIT

## Support

- **Workspace issues**: [codi-gripspace/issues](https://github.com/laynepenney/codi-gripspace/issues)
- **Codi issues**: [codi/issues](https://github.com/laynepenney/codi/issues)
- **gitgrip issues**: [gitgrip/issues](https://github.com/laynepenney/gitgrip/issues)

## Security

For security issues, please email [security@codi.dev](mailto:security@codi.dev) instead of using the public issue tracker.

See [SECURITY.md](SECURITY.md) for more details.
