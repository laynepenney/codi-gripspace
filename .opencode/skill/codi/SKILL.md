---
name: codi
description: Codi AI coding wingman (TypeScript CLI). Use when working on codi TypeScript source.
---

# Codi TypeScript CLI

AI coding wingman - TypeScript CLI with agent loop, tools, commands, and multiple AI providers.

## Build / Dev / Test

```bash
cd codi
pnpm install          # Install dependencies
pnpm build            # Compile TypeScript
pnpm dev              # Dev mode
pnpm test             # Run Vitest tests
```

## Architecture

- `src/index.ts` - CLI entry, REPL loop
- `src/agent.ts` - Core agent loop
- `src/commands/` - Slash command system
- `src/tools/` - Filesystem interaction tools
- `src/providers/` - AI backends (Anthropic, OpenAI, Ollama)
- `src/orchestrate/` - Multi-agent orchestration (IPC)
- `src/rag/` - Semantic code search
- `src/model-map/` - Multi-model orchestration

## Conventions

- ES Modules with `.js` extensions in imports
- Async/await, TypeScript interfaces, avoid `any`
- Vitest for tests in `tests/`
