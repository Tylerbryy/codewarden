# CodeWarden Setup Guide 🛡️

Quick guide to get CodeWarden published and installed.

## Step 1: Initialize Git Repository

```bash
cd C:\Users\tyler\OneDrive\Desktop\claude-verity-plugin
git init
git add .
git commit -m "Initial commit: CodeWarden v1.0.0

CodeWarden is your vigilant guardian for code quality:
- Ultracite code quality enforcement
- React 19 & Next.js App Router patterns
- Security auditing
- Automated workflows
"
```

## Step 2: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `codewarden`
3. Description: `🛡️ Your vigilant guardian for code quality - Claude Code plugin`
4. Public repository
5. **Don't** initialize with README (we already have one)
6. Click "Create repository"

## Step 3: Push to GitHub

```bash
# Add remote
git remote add origin https://github.com/tylerbryy/codewarden.git

# Push code
git branch -M main
git push -u origin main

# Tag the release
git tag -a v1.0.0 -m "CodeWarden v1.0.0 - Initial Release"
git push origin v1.0.0
```

## Step 4: Test Locally First

```bash
# In Claude Code:
/plugin marketplace add C:\Users\tyler\OneDrive\Desktop\claude-verity-plugin
/plugin install codewarden

# Try the commands:
/code-review
/security-audit
/help
```

## Step 5: Install from GitHub (After Pushing)

```bash
# In Claude Code:
/plugin marketplace add https://github.com/tylerbryy/codewarden
/plugin install codewarden
```

## Step 6: Add to Your Projects

Add to your project's `.claude/settings.json`:

```json
{
  "pluginMarketplaces": [
    "https://github.com/tylerbryy/codewarden"
  ],
  "plugins": {
    "codewarden": {
      "enabled": true
    }
  }
}
```

## What CodeWarden Includes

### ✅ 2 Agent Skills
- **Ultracite**: Code quality enforcement (446 lines)
- **React Next Modern**: Modern React/Next.js patterns (1,280 lines)

### ✅ 4 Slash Commands
- `/code-review` - Comprehensive code review
- `/fix-patterns` - Auto-fix anti-patterns
- `/migrate-to-app-router` - Next.js migration guide
- `/security-audit` - Security vulnerability scanning

### ✅ 2 Specialized Agents
- **code-refactorer** - Safe refactoring expert
- **security-auditor** - Security expert

### ✅ 4 Automation Hooks
- Welcome message on startup
- Unsafe command prevention
- Code quality reminders
- Optional auto-formatting

### ✅ Complete Documentation
- README.md - Installation & usage
- CHANGELOG.md - Version history
- CONTRIBUTING.md - Contributor guide
- LICENSE - MIT License

## Sharing CodeWarden

### On GitHub
Add topics to your repository:
- `claude-code`
- `claude-plugin`
- `code-quality`
- `react`
- `nextjs`
- `typescript`
- `codewarden`

### On Social Media
```
🛡️ Just released CodeWarden - A comprehensive Claude Code plugin for modern TypeScript/React development!

✨ Features:
• Ultracite code quality enforcement
• React 19 & Next.js App Router patterns
• Security auditing
• Automated workflows

Check it out: https://github.com/tylerbryy/codewarden

#ClaudeCode #TypeScript #React #CodeQuality
```

## Troubleshooting

### Plugin not showing up?
- Make sure the repository is public
- Verify the marketplace URL is correct
- Try refreshing: `/plugin marketplace refresh`

### Commands not working?
- Restart Claude Code after installation
- Check `/help` to see if commands are listed
- Verify plugin is enabled: `/plugin`

### Skills not activating?
- Skills activate automatically based on context
- Try explicitly: "Review this code using Ultracite standards"
- Check the skill description in `skills/*/SKILL.md`

## Next Steps

1. ✅ Push to GitHub
2. ✅ Test installation
3. ✅ Share with community
4. ✅ Gather feedback
5. ✅ Iterate and improve

---

**Need help?** Open an issue at https://github.com/tylerbryy/codewarden/issues
