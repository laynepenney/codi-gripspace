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
.claude/skills/         # Claude Code skill files
.opencode/skill/        # OpenCode skill files
.codex/skills/          # Codex skill files
```

## Manifest Schema

The `manifest.yaml` defines everything gitgrip needs:

```yaml
version: 1
manifest:
  url: <gripspace repo URL>
  linkfile:               # Files to link into workspace root
    - src: CLAUDE.md
      dest: CLAUDE.md

repos:
  <name>:
    url: <git URL>
    path: <local path>
    default_branch: main
    reference: true/false  # Read-only repos excluded from branch/PR ops
    linkfile:              # Per-repo file links
      - src: .claude/skills/<name>
        dest: .claude/skills/<name>
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
allowed-tools: Bash(cargo *)    # Claude Code only
---

# Title
Content with build commands, architecture, conventions...
```

Skill files live in three format-specific directories:
- `.claude/skills/<name>/SKILL.md` - Claude Code
- `.opencode/skill/<name>/SKILL.md` - OpenCode
- `.codex/skills/<name>/SKILL.md` - Codex

## How Linkfiles Work

The `linkfile` entries in `manifest.yaml` create symlinks from the gripspace into the workspace:
- `src` is relative to this repo
- `dest` is relative to the workspace root
- Directories are linked recursively

CLAUDE.md is special: it gets **composed** (concatenated) with any local CLAUDE.md in the manifest repo, so private workspace context merges with the shared gripspace context.

## Making Changes

1. Edit files in this repo (the gripspace working copy is at `.gitgrip/spaces/codi-gripspace/`)
2. Copy changes to the repo clone: `cp <file> ./codi-gripspace/`
3. Use `gr` to branch, commit, push, and create PRs
4. After merge, `gr sync` propagates changes to the workspace via linkfiles
