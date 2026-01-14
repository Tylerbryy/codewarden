# Changelog

All notable changes to CodeWarden will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-01-14

### Added

#### New Agent Skills
- **react-best-practices**: React and Next.js performance optimization guidelines from Vercel Engineering
  - Priority-ordered guidelines (Critical → Low impact)
  - 39 individual rule files covering all optimization categories
  - Quick reference for critical patterns (waterfalls, bundle size)
  - Categories: async, bundle, server, client, rerender, rendering, js, advanced

- **vercel-deploy**: Deploy applications to Vercel instantly
  - No authentication required - returns preview URL and claimable deployment link
  - Auto-detects 40+ frameworks (Next.js, Remix, Astro, SvelteKit, etc.)
  - Supports directory or tarball deployment
  - Static HTML project support with automatic index.html handling
  - Includes `scripts/deploy.sh` for direct execution

- **vercel-design-guidelines**: Review web interfaces against Vercel's design guidelines
  - Audit categories: Interactions, Animations, Layout, Content, Forms, Performance, Design, Copywriting
  - Severity levels: Critical, Warning, Suggestion
  - Quick checklist for rapid reviews
  - Code examples for common fixes

#### Plugin Metadata
- New keywords: `vercel`, `deployment`, `performance`, `design-guidelines`, `react-performance`, `bundle-optimization`

### Changed
- Plugin version bumped from 1.0.3 → 2.0.0 (major release with new skill additions)
- Plugin description updated to include Vercel deployment, React performance, and design guidelines
- Total Skills increased from 3 to 6

### Technical Details
- Total Skills: 6 (was 3)
  - ultracite
  - react-next-modern
  - ui-ux-guidelines
  - react-best-practices (new)
  - vercel-deploy (new)
  - vercel-design-guidelines (new)
- Total reference documents: 47 markdown files across all skills

---

## [1.0.3] - 2025-12-29

### Enhanced
- **UI/UX Guidelines Skill**: Significantly expanded with comprehensive web interface guidelines
  - Added Copywriting Guidelines section (Vercel style guide as reference)
  - Added Cross-Browser Compatibility section (SVG transforms, text anti-aliasing)
  - Expanded Performance section (Web Workers, font subsetting, preconnect to origins)
  - Expanded Design section (theme-color meta tag, color-scheme CSS property, Windows select backgrounds)
  - Enhanced Content & Accessibility section (non-breaking spaces, locale detection via Accept-Language)
  - Enhanced Forms section (password manager compatibility, autocomplete guidance)
  - Enhanced Animation section (transition: all warning, SVG transform workarounds)
  - Added 20+ new code examples demonstrating common violations and fixes

### Added
- **AGENTS.md reference document** for UI/UX Guidelines skill
  - Agent activation patterns and triggers
  - Integration workflows with Ultracite and React Next Modern skills
  - Priority levels for findings (Critical/High/Medium)
  - Vercel-specific guidelines handling guidance
  - Common review workflows (forms, interactive components, responsive layouts, performance)
  - Example agent responses with proper formatting

- New keywords in plugin metadata: `copywriting`, `internationalization`, `browser-quirks`

### Changed
- UI/UX Guidelines skill expanded from 310 to 407 lines while staying well under the 500-line recommendation
- README.md updated with enhanced UI/UX Guidelines feature description
- Plugin version bumped to 1.0.3

### Documentation
- Enhanced README with new UI/UX capabilities
- Added AGENTS.md to plugin structure documentation
- Updated plugin.json with new keywords for better discoverability

## [1.0.0] - 2025-01-10

### Added

#### Agent Skills
- **Ultracite**: Comprehensive code quality enforcement
  - Type safety rules (no any, enum → const objects)
  - Accessibility standards (WCAG compliance, ARIA attributes)
  - Modern JavaScript patterns (arrow functions, template literals)
  - React best practices (proper keys, hook dependencies)
  - Next.js optimization (Image component, proper imports)
  - Error handling patterns
  - Style consistency rules

- **React Next Modern**: React 19 and Next.js App Router patterns
  - useEffect "escape hatch" philosophy
  - Server Components by default
  - Server Actions for mutations
  - React 19 form hooks (useActionState, useFormStatus, useOptimistic)
  - Request memoization with React.cache
  - Performance optimization patterns
  - Security standards for Server Actions
  - Migration guides from legacy patterns

#### Slash Commands
- `/code-review` - Comprehensive code review with quality and security checks
- `/fix-patterns` - Automatically detect and fix common anti-patterns
- `/migrate-to-app-router` - Migrate from Pages Router to App Router
- `/security-audit` - Security vulnerability scanning and remediation

#### Specialized Agents
- **code-refactorer** - Expert refactoring while preserving functionality
- **security-auditor** - Security vulnerability identification and fixing

#### Automation Hooks
- Session start welcome message
- Unsafe bash command prevention
- Code quality reminders
- Optional auto-formatting after edits

#### Documentation
- Comprehensive README with examples
- Installation instructions (GitHub, local, team)
- Usage examples and patterns
- Plugin structure documentation
- Contributing guidelines
- MIT License

### Technical Details
- Minimum Claude Code version: 1.0.0
- Plugin type: Skills + Commands + Agents + Hooks
- Total Skills: 2
- Total Commands: 4
- Total Agents: 2
- Total Hooks: 4

### Notes
- Initial release
- Built by Tyler Gibbs
- Focus on production-grade React/Next.js development
- Emphasis on security, accessibility, and type safety

## [Unreleased]

### Planned
- GraphQL/tRPC integration patterns
- Database migration safety checks
- API versioning enforcement
- Performance budgets and monitoring
- Automated test generation
- CI/CD configuration templates
- Docker and deployment patterns

---

For more information, see the [README](README.md).
