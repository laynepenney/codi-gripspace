---
name: codi-rs
description: Codi AI coding wingman (Rust implementation). Use when working on Rust source in codi-rs/.
---

# Codi Rust Implementation

Rust port of Codi, located in `codi/codi-rs/`.

## Build / Test

```bash
cd codi/codi-rs
cargo build            # Debug build
cargo test             # Run tests
cargo clippy           # Lint
cargo bench            # Benchmarks
```

## Architecture

- `src/main.rs` - CLI entry (clap)
- `src/agent/` - Core agent loop
- `src/providers/` - AI backends
- `src/tools/` - Filesystem tools
- `src/tui/` - Terminal UI (ratatui)
- `src/mcp/` - Model Context Protocol
- `src/symbol_index/` - SQLite code navigation (tree-sitter)
- `src/rag/` - RAG system

## Conventions

- anyhow for errors, thiserror for library errors
- async-trait for async traits
- tokio async runtime
