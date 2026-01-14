# CLAUDE.md

This file provides guidance to AI coding agents (Claude Code, Cursor, Copilot, etc.) when working with code in this repository.

## Repository Overview

CodeWarden is a Claude Code plugin for enforcing modern development practices, code quality standards, and security best practices in TypeScript/React/Next.js applications.

## Plugin Structure

```
codewarden/
├── .claude-plugin/
│   └── plugin.json           # Plugin metadata (name, version, description)
├── skills/                   # Agent Skills (model-invoked)
│   ├── {skill-name}/
│   │   ├── SKILL.md          # Required: skill definition with frontmatter
│   │   └── references/       # Optional: supporting documentation
├── commands/                 # Slash commands (user-invoked via /{name})
│   └── {command-name}.md
├── agents/                   # Specialized subagents
│   └── {agent-name}.md
└── hooks/
    └── hooks.json            # Automation hooks
```

## Creating/Modifying Skills

### SKILL.md Format

```markdown
---
name: skill-name
description: One sentence describing when to use this skill. Include trigger phrases.
---

# Skill Title

Brief description and instructions for Claude to follow.
```

### Best Practices

- **Keep SKILL.md under 500 lines** - put detailed reference material in separate files
- **Write specific descriptions** - helps Claude know exactly when to activate the skill
- **Use progressive disclosure** - reference supporting files that get read only when needed
- **Prefer scripts over inline code** - script execution doesn't consume context (only output does)

### Naming Conventions

- **Skill directories**: `kebab-case` (e.g., `react-best-practices`, `vercel-deploy`)
- **SKILL.md**: Always uppercase, always this exact filename
- **Scripts**: `kebab-case.sh` (e.g., `deploy.sh`)

## Creating/Modifying Commands

Commands are markdown files in `commands/` that become slash commands prefixed with `codewarden:`.

```markdown
---
description: Short description shown in command menu
---

Instructions for Claude when this command is invoked.
```

## Creating/Modifying Agents

Agents are markdown files in `agents/` that define specialized subagents.

```markdown
---
name: agent-name
description: When to use this agent
skills: skill1, skill2  # Optional: skills to inject into agent context
---

Agent instructions and capabilities.
```

## Script Requirements

For skills with scripts (like `vercel-deploy`):

- Use `#!/bin/bash` shebang
- Use `set -e` for fail-fast behavior
- Write status messages to stderr: `echo "Message" >&2`
- Write machine-readable output (JSON) to stdout
- Include a cleanup trap for temp files

## Version Management

When making changes:

1. Update version in `.claude-plugin/plugin.json` (semver)
2. Add entry to `CHANGELOG.md`
3. Update `README.md` if adding new features

## Testing Changes

```bash
# Test plugin locally
claude --plugin-dir /path/to/codewarden

# Verify skills load
"What skills are available?"
```
