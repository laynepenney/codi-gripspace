---
name: codi-gripspace
description: Codi gripspace configuration repo. Use when editing manifest.yaml, skill files, context docs, envsetup.sh, or linkfile mappings.
---

# Codi Gripspace

Configuration repository for the Codi multi-repo workspace. Defines repos, agent context, skill files, scripts, and file links consumed by gitgrip.

## Repo Structure

```
manifest.yaml           # Gripspace manifest (repos, agent config, scripts, links)
CLAUDE.md               # Workspace guide for Claude Code (linked into workspace)
AGENTS.md               # Multi-agent coordination guide (linked into workspace)
CODI.md                 # General workspace overview (linked into workspace)
envsetup.sh             # Shell functions and env vars (linked into workspace)
skills/                 # Canonical skill files (single source of truth)
  codi/SKILL.md         # Codi TypeScript CLI skill
  codi-rs/SKILL.md      # Codi Rust skill
  gitgrip/SKILL.md      # gitgrip multi-repo workflow skill
  codi-gripspace/SKILL.md  # This file - gripspace configuration skill
```

## Skills Convention

All skill files live in `skills/<name>/SKILL.md` as the single canonical source. Linkfile entries in `manifest.yaml` distribute each skill into the three agent-format directories:

- `.claude/skills/<name>/` - Claude Code
- `.opencode/skill/<name>/` - OpenCode
- `.codex/skills/<name>/` - Codex

The `allowed-tools` frontmatter field is Claude-specific but harmlessly ignored by OpenCode and Codex.

## Manifest Schema

The `manifest.yaml` defines everything gitgrip needs:

```yaml
version: 1
manifest:
  url: <gripspace repo URL>
  linkfile:               # Files to link into workspace root
    - src: CLAUDE.md
      dest: CLAUDE.md
    - src: skills/codi    # Canonical skill -> all three formats
      dest: .claude/skills/codi
    - src: skills/codi
      dest: .opencode/skill/codi
    - src: skills/codi
      dest: .codex/skills/codi

repos:
  <name>:
    url: <git URL>
    path: <local path>
    default_branch: main
    reference: true/false  # Read-only repos excluded from branch/PR ops
    agent:                 # Per-repo agent context for `gr agent context`
      description: "..."
      language: typescript|rust|python
      build: "command"
      test: "command"
      lint: "command"
      format: "command"

workspace:
  agent:                   # Workspace-level agent context
    description: "..."
    conventions: [...]
    workflows: {...}
  scripts:
    <name>:
      command: "..."
      description: "..."

settings:
  pr_prefix: "..."
  merge_strategy: all-or-nothing
```

## Skill File Format

All skill formats use frontmatter + markdown:

```markdown
---
name: <skill-name>
description: <when to use this skill>
allowed-tools: Bash(cargo *)    # Claude Code only, ignored by others
---

# Title
Content with build commands, architecture, conventions...
```

## How Linkfiles Work

The `linkfile` entries in `manifest.yaml` create symlinks from the gripspace into the workspace:
- `src` is relative to this repo
- `dest` is relative to the workspace root
- Directories are linked recursively
- Multiple `dest` entries can share the same `src` (used for skill distribution)

CLAUDE.md is special: it gets **composed** (concatenated) with any local CLAUDE.md in the manifest repo, so private workspace context merges with the shared gripspace context.

## Making Changes

1. Edit files in the repo clone (`./codi-gripspace/`)
2. Use `gr` to branch, commit, push, and create PRs
3. After merge, `gr sync` propagates changes to the workspace via linkfiles
