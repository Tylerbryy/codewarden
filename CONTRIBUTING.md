# Contributing to CodeWarden

First off, thank you for considering contributing to CodeWarden! It's people like you that make this plugin better for everyone.

## Code of Conduct

This project and everyone participating in it is governed by respect, kindness, and professionalism. By participating, you are expected to uphold these values.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the [issue tracker](https://github.com/tylerbryy/codewarden/issues) as you might find that you don't need to create one. When you are creating a bug report, please include as many details as possible:

* **Use a clear and descriptive title**
* **Describe the exact steps to reproduce the problem**
* **Provide specific examples** - Include code snippets or links
* **Describe the behavior you observed** and what you expected
* **Include screenshots or animated GIFs** if relevant
* **Include your environment details**:
  - Claude Code version
  - Operating system
  - Plugin version

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, please include:

* **Use a clear and descriptive title**
* **Provide a detailed description** of the suggested enhancement
* **Provide specific examples** to demonstrate the enhancement
* **Explain why this enhancement would be useful** to most users
* **List any plugins or tools** that have similar features

### Pull Requests

1. Fork the repo and create your branch from `main`
2. Make your changes
3. Test your changes thoroughly
4. Update the documentation if needed
5. Write a clear commit message
6. Open a Pull Request

## Development Setup

### Prerequisites

- Claude Code installed
- Git
- Text editor (VS Code recommended)

### Local Development

```bash
# Clone your fork
git clone https://github.com/YOUR-USERNAME/claude-dev-tools.git
cd claude-dev-tools

# Create a feature branch
git checkout -b feature/amazing-feature

# Make your changes to:
# - skills/ (for Agent Skills)
# - commands/ (for slash commands)
# - agents/ (for specialized agents)
# - hooks/ (for automation hooks)

# Test locally in Claude Code
# In Claude Code:
/plugin marketplace add /path/to/claude-dev-tools
/plugin install tensorpoint-dev-tools
```

### Testing Your Changes

1. **Test the skill activation**:
   ```bash
   # Try writing code that should trigger the skill
   "Write a React component with a form"
   ```

2. **Test slash commands**:
   ```bash
   /code-review
   /fix-patterns --dry-run
   /security-audit
   ```

3. **Test agents**:
   ```bash
   # In Claude Code, invoke the agent
   "Use the code-refactorer agent to refactor this component"
   ```

4. **Test hooks**:
   - Session start hook (restart Claude Code)
   - Tool call hooks (try editing a file)

## Style Guidelines

### Skill Files (SKILL.md)

```markdown
---
name: skill-name
description: Brief description for discovery. Include trigger words.
allowed-tools: Read, Grep, Glob, Edit
globs: "**/*.{ts,tsx}"
---

# Skill Name

## Purpose
Clear explanation of what this skill does

## Instructions
Step-by-step instructions for Claude

## Examples
Concrete before/after code examples

## Additional Resources
Links to relevant docs
```

### Command Files (commands/*.md)

```markdown
---
description: One-line description of the command
---

# Command Name

Clear description of what this command does.

## Instructions

Detailed steps for Claude to follow.

## Example Usage

\```
/command-name
/command-name --option
\```
```

### Agent Files (agents/*.md)

```markdown
---
name: agent-name
description: What this agent specializes in
model: sonnet
---

# Agent Name

Expert in [specialization]

## Capabilities
- Bullet list of what it can do

## Instructions
Step-by-step workflow

## Example Workflow
Concrete example of usage
```

## Commit Messages

Use clear, descriptive commit messages:

```
Add code-review command for comprehensive code analysis

- Checks for Ultracite violations
- Validates React/Next.js patterns
- Generates structured report
- Includes severity levels
```

Format:
- Use present tense ("Add feature" not "Added feature")
- Use imperative mood ("Move cursor to..." not "Moves cursor to...")
- First line should be 50 characters or less
- Reference issues and pull requests after the first line

## Plugin Structure

```
claude-verity-plugin/
├── .claude-plugin/
│   ├── plugin.json           # Plugin metadata
│   └── marketplace.json      # Marketplace config
├── skills/                   # Agent Skills
│   ├── ultracite/
│   │   └── SKILL.md
│   └── react-next-modern/
│       └── SKILL.md
├── commands/                 # Slash commands
│   ├── code-review.md
│   ├── fix-patterns.md
│   ├── migrate-to-app-router.md
│   └── security-audit.md
├── agents/                   # Specialized agents
│   ├── code-refactorer.md
│   └── security-auditor.md
└── hooks/                    # Automation hooks
    └── hooks.json
```

## Adding New Features

### Adding a New Skill

1. Create a directory in `skills/`:
   ```bash
   mkdir skills/my-new-skill
   ```

2. Create `SKILL.md` with proper frontmatter:
   ```markdown
   ---
   name: my-new-skill
   description: What it does and when to use it
   allowed-tools: Read, Edit
   globs: "**/*.ts"
   ---
   ```

3. Add comprehensive instructions and examples

4. Test that Claude activates it appropriately

### Adding a New Command

1. Create `commands/my-command.md`:
   ```markdown
   ---
   description: Brief description
   ---

   # My Command

   Instructions for Claude...
   ```

2. Test with `/my-command`

### Adding a New Agent

1. Create `agents/my-agent.md`:
   ```markdown
   ---
   name: my-agent
   description: Specialization
   model: sonnet
   ---
   ```

2. Define capabilities and workflow

3. Test by asking Claude to use it

### Adding Hooks

1. Edit `hooks/hooks.json`
2. Add your hook to the appropriate event
3. Test that it triggers correctly

## Versioning

We use [Semantic Versioning](https://semver.org/):

- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes (backward compatible)

Update version in `.claude-plugin/plugin.json` and `CHANGELOG.md`.

## Documentation

- Update README.md for user-facing changes
- Update CHANGELOG.md with all changes
- Add examples for new features
- Update command descriptions if needed

## Publishing Changes

1. Update version in `.claude-plugin/plugin.json`
2. Update `CHANGELOG.md`
3. Commit changes:
   ```bash
   git commit -am "Release v1.1.0"
   ```
4. Tag the release:
   ```bash
   git tag v1.1.0
   ```
5. Push to GitHub:
   ```bash
   git push origin main --tags
   ```

## Questions?

Feel free to:
- Open an issue for questions
- Start a discussion on GitHub
- Reach out to tyler.gibbs@tensorpt.com

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing!** 🚀
