# CodeWarden 🛡️

> Your vigilant guardian for code quality and modern development practices

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/tylerbryy/codewarden)

**Created by [Tyler Gibbs](https://www.tylergibbs.dev/about)**

## Overview

**CodeWarden** is a comprehensive Claude Code plugin that watches over your codebase, enforcing modern development practices, code quality standards, and security best practices for TypeScript/React/Next.js applications. Like a vigilant guardian, it ensures your code meets the highest standards of quality, accessibility, and security.

## Features

### 🎯 Agent Skills

#### **Ultracite - Code Quality Enforcer**
Strict enforcement of type safety, accessibility standards, and code quality rules based on Biome's linter.

- **Type Safety**: No `any`, proper TypeScript patterns, enum → const objects
- **Accessibility**: WCAG compliance, proper ARIA attributes, semantic HTML
- **Modern JavaScript**: Arrow functions, template literals, optional chaining
- **React Best Practices**: Proper keys, hook dependencies, component patterns
- **Next.js Optimization**: Image optimization, proper imports, App Router patterns

#### **React Next Modern - Architectural Patterns**
Enforce React 19 and Next.js App Router best practices with server-first architecture.

- **Server Components**: Async-native data fetching, request memoization
- **Server Actions**: Secure mutations with validation and auth
- **Form Hooks**: useActionState, useFormStatus, useOptimistic
- **Performance**: Eliminate waterfalls, optimize bundles
- **Security**: Input validation, authentication, rate limiting

### 🔧 Slash Commands

#### `/code-review`
Comprehensive code review with Ultracite and React/Next.js patterns
```bash
/code-review                    # Review recent changes
/code-review web/src/app        # Review specific directory
/code-review Auth.tsx           # Review specific file
```

#### `/fix-patterns`
Automatically detect and fix common anti-patterns
```bash
/fix-patterns                   # Interactive mode
/fix-patterns --dry-run         # Preview changes
/fix-patterns --type=var        # Fix specific patterns
```

#### `/migrate-to-app-router`
Migrate Next.js Pages Router to App Router with Server Components
```bash
/migrate-to-app-router          # Full migration guide
/migrate-to-app-router --analyze-only  # Just show plan
```

#### `/security-audit`
Comprehensive security audit of your application
```bash
/security-audit                 # Full security scan
/security-audit --critical-only # Show critical issues only
/security-audit --fix           # Auto-fix safe issues
```

### 🤖 Specialized Agents

#### **code-refactorer**
Expert in refactoring code to modern patterns while preserving functionality
- Incremental, safe refactoring
- Type safety improvements
- Performance optimization
- Component extraction

#### **security-auditor**
Specialized in identifying and fixing security vulnerabilities
- Server Action security
- Authentication/authorization audits
- SQL injection prevention
- XSS vulnerability detection
- Dependency security checks

### 🪝 Automation Hooks

- **Session Start**: Welcome message with plugin capabilities
- **Unsafe Command Prevention**: Blocks potentially destructive bash commands
- **Code Quality Reminders**: Best practice reminders during development

## Installation

### Option 1: Install from GitHub (Recommended)

```bash
# In Claude Code
/plugin marketplace add https://github.com/tylerbryy/codewarden

# Install the plugin
/plugin install codewarden
```

### Option 2: Install from Local Marketplace

```bash
# Clone the repository
git clone https://github.com/tylerbryy/codewarden.git
cd codewarden

# Add local marketplace
/plugin marketplace add ./

# Install the plugin
/plugin install codewarden
```

### Option 3: Team Installation (Repository Level)

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

When team members trust the repository, the plugin installs automatically.

## Quick Start

1. **Install the plugin** (see Installation above)

2. **Run a code review**:
   ```bash
   /code-review
   ```

3. **Perform a security audit**:
   ```bash
   /security-audit
   ```

4. **Fix common anti-patterns**:
   ```bash
   /fix-patterns
   ```

5. **The skills activate automatically** when:
   - Writing TypeScript/React code
   - Reviewing pull requests
   - Implementing forms or mutations
   - Working with Server Components/Actions

## Usage Examples

### Enforce Code Quality

The Ultracite skill automatically enforces rules when you write code:

```typescript
// ❌ Claude will suggest fixing these:
var count = 0                              // Use const/let
enum Status { ACTIVE }                     // Use as const
function process(data: any) {}             // Use specific types
items.map((item, i) => <div key={i}>)     // Use proper keys

// ✅ Claude will guide you to write:
let count = 0
const Status = { ACTIVE: 'active' } as const
function process(data: User) {}
items.map(item => <div key={item.id}>)
```

### Modern React Patterns

The React Next Modern skill enforces server-first architecture:

```typescript
// ❌ Claude will suggest refactoring:
"use client"
function Page() {
  const [data, setData] = useState([])
  useEffect(() => {
    fetch('/api/data').then(r => r.json()).then(setData)
  }, [])
}

// ✅ Claude will guide you to:
async function Page() {
  const data = await db.query.data.findMany()
  return <DataList data={data} />
}
```

### Secure Server Actions

The security-auditor agent ensures your Server Actions are secure:

```typescript
// ❌ Claude will flag security issues:
"use server"
export async function updateUser(data: any) {
  await db.update(users).set(data)
}

// ✅ Claude will guide you to:
"use server"
import { z } from 'zod'
import { auth } from '@/lib/auth'

const schema = z.object({
  name: z.string().min(2),
  email: z.string().email()
})

export async function updateUser(formData: FormData) {
  const session = await auth()
  if (!session?.user) throw new Error('Unauthorized')

  const data = schema.parse({
    name: formData.get('name'),
    email: formData.get('email')
  })

  await db.update(users)
    .set(data)
    .where(eq(users.id, session.user.id))

  revalidatePath('/profile')
}
```

## Plugin Structure

```
claude-verity-plugin/
├── .claude-plugin/
│   └── plugin.json           # Plugin metadata
├── skills/
│   ├── ultracite/
│   │   └── SKILL.md          # Code quality rules
│   └── react-next-modern/
│       └── SKILL.md          # React/Next.js patterns
├── commands/
│   ├── code-review.md        # Code review command
│   ├── fix-patterns.md       # Pattern fixing command
│   ├── migrate-to-app-router.md  # Migration guide
│   └── security-audit.md     # Security audit command
├── agents/
│   ├── code-refactorer.md    # Refactoring agent
│   └── security-auditor.md   # Security agent
├── hooks/
│   └── hooks.json            # Automation hooks
├── README.md                 # This file
└── LICENSE                   # MIT License
```

## Configuration

### Customize Hook Behavior

Edit `hooks/hooks.json` to enable/disable automation:

```json
{
  "session-start": [
    {
      "name": "welcome-message",
      "enabled": true  // Set to false to disable
    }
  ]
}
```

### Adjust Skill Activation

Skills activate automatically based on context. To manually invoke:

```bash
# Ask Claude to use a specific skill
"Review this code using Ultracite standards"
"Refactor this to use React Server Components"
```

## Development

### Local Development

```bash
# Clone the repository
git clone https://github.com/tylerbryy/codewarden.git
cd codewarden

# Make your changes to skills, commands, or agents

# Test locally
/plugin marketplace add ./
/plugin install codewarden
```

### Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Publishing Updates

```bash
# Update version in .claude-plugin/plugin.json
# Commit and tag
git commit -am "Release v1.1.0"
git tag v1.1.0
git push origin main --tags
```

## Philosophy

This plugin is built on these core principles:

1. **Safety First**: Never break working code
2. **Server-First**: Leverage Server Components and Server Actions
3. **Type Safety**: Strict TypeScript with no escape hatches
4. **Accessibility**: WCAG compliance is non-negotiable
5. **Security**: Defense in depth, validate everything
6. **Performance**: Optimize for Core Web Vitals
7. **Maintainability**: Code should be easy to understand

## Roadmap

- [ ] GraphQL/tRPC integration patterns
- [ ] Database migration safety checks
- [ ] API versioning enforcement
- [ ] Performance budgets and monitoring
- [ ] Automated test generation
- [ ] CI/CD configuration templates
- [ ] Docker and deployment patterns

## Support

- 🐛 [Issue Tracker](https://github.com/tylerbryy/codewarden/issues)
- 💬 [Discussions](https://github.com/tylerbryy/codewarden/discussions)
- 📧 [Email](mailto:tyler.gibbs@tensorpt.com)

## License

MIT License - see [LICENSE](LICENSE) file for details

---

**Built with ❤️ by [Tyler Gibbs](https://github.com/tylerbryy)**
