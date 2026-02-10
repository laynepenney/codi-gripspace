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
# Initialize the workspace
gr init https://github.com/laynepenney/codi-gripspace.git
cd codi-gripspace

# Set up environment
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
pnpm install          # Install dependencies
pnpm build            # Compile TypeScript
pnpm dev              # Run in dev mode
pnpm test             # Run Vitest tests
```

Or via `gr run`:
```bash
gr run build-ts
gr run dev-ts
gr run test-ts
```

### Codi Rust

```bash
cd codi-rs
cargo build           # Debug build
cargo build --release # Release build
cargo test            # Run tests
cargo bench           # Benchmarks
```

Or via `gr run`:
```bash
gr run build-rs
gr run dev-rs
gr run test-rs
```

### gitgrip

```bash
cd gitgrip
cargo build           # Debug build
cargo build --release # Release build
cargo test            # Run tests
cargo clippy          # Lint
```

Or via `gr run`:
```bash
gr run build-gr
gr run test-gr
```

## Environment Setup

Source `envsetup.sh` to set up variables and shell functions:

```bash
source ./envsetup.sh
codi-help               # Show all available commands
```

### Environment Variables

| Variable | Value | Description |
|----------|-------|-------------|
| `CODI_WORKSPACE` | workspace root | Root of this workspace |
| `CODI_SRC` | `./codi` | Codi TypeScript source |
| `CODI_RS_SRC` | `./codi-rs` | Codi Rust source |
| `CODI_HOME` | `./.codi` | Local data directory |

### Shell Functions

| Command | Description |
|---------|-------------|
| **TypeScript** | |
| `codi-dev` | Run codi TypeScript in dev mode |
| `codi-build` | Build codi TypeScript |
| `codi-test` | Run codi TypeScript tests |
| **Rust** | |
| `codi-dev-rs` | Run codi Rust (`cargo run`) |
| `codi-build-rs` | Build codi Rust |
| `codi-test-rs` | Run codi Rust tests |
| **Both** | |
| `codi-build-all` | Build TypeScript + Rust |
| **Navigation** | |
| `cdc` | `cd` to `codi/` |
| `cdcr` | `cd` to `codi-rs/` |
| `cdg` | `cd` to `gitgrip/` |
| `cdw` | `cd` to workspace root |
| **Help** | |
| `codi-help` | Show all commands |

## `gr run` Scripts

```bash
gr run --list           # Show all available scripts
```

| Script | Description |
|--------|-------------|
| `build-ts` | Build codi TypeScript |
| `dev-ts` | Run codi TypeScript in dev mode |
| `test-ts` | Run codi TypeScript tests |
| `build-rs` | Build codi Rust |
| `dev-rs` | Run codi Rust |
| `test-rs` | Run codi Rust tests |
| `build-gr` | Build gitgrip |
| `test-gr` | Run gitgrip tests |
| `build-all` | Build everything |
| `test-all` | Run all tests |

## gitgrip Workflow Rules

### CRITICAL: Always Use `gr`

**NEVER use raw `git` or `gh` commands.** Always use `gr` for ALL operations.

```
WRONG:
   git checkout -b feat/x
   git add . && git commit -m "msg"
   gh pr create --title "msg"

CORRECT:
   gr branch feat/x
   gr add . && gr commit -m "msg"
   gr pr create -t "msg" --push
```

### Standard Workflow

```bash
# Start work
gr sync                           # Pull latest from all repos
gr status                         # Check state
gr branch feat/my-feature         # Create branch across ALL repos

# During development
gr diff                           # Review changes
gr add .                          # Stage across repos
gr commit -m "feat: description"  # Commit across repos
gr push -u                        # Push with tracking

# Pull requests
gr pr create -t "description" --push    # Create linked PRs
gr pr status                            # Check PR status
gr pr merge                             # Merge all linked PRs

# Post-merge cleanup
gr checkout --base                      # Return to base branch
gr sync                                 # Pull latest
gr prune                                # Dry-run cleanup
gr prune --execute                      # Delete merged branches
```

### Workflow Rules

1. **Always run `gr sync` before starting new work**
2. **Always use `gr branch`** to create branches across all repos
3. **Use `gr add`, `gr commit`, `gr push`** instead of raw git
4. **Always use pull requests** - no direct pushes to main
5. **Check `gr status` frequently**
6. **After merge, always cleanup** - `gr checkout --base && gr sync && gr prune --execute`

## Reference Repos

Reference repos are marked `reference: true` in the manifest. They:
- Sync with `gr sync` (read-only)
- Are excluded from branch, push, and PR operations
- Serve as architecture/pattern references

| Repo | What to learn |
|------|---------------|
| opencode | TUI patterns, agent architecture |
| aider | Terminal AI pair programming patterns |
| codex | Rust reference implementation |

## Per-Repository Docs

Each repo has its own detailed guide:

- `codi/AGENTS.md` - Codi CLI architecture, features, coding patterns
- `gitgrip/CLAUDE.md` - gitgrip development guide, command reference

## Testing Guidelines

### TypeScript
```bash
pnpm test              # Run all tests
pnpm test:watch        # Watch mode
# Tests in codi/tests/
```

### Rust
```bash
cargo test             # Run all tests
cargo test -- --nocapture    # Show output
cargo bench            # Run benchmarks
```

### Critical: Use Temp Directories for Tests

```rust
// CORRECT
let temp_dir = tempfile::tempdir()?;
let workspace_root = temp_dir.path().join("workspace");

// WRONG - never test on real workspace
let workspace_root = "/Users/someone/codi-gripspace";
```
