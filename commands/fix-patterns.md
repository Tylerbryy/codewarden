---
description: Automatically fix common code patterns and anti-patterns across the codebase
---

# Fix Patterns Command

Automatically detect and fix common anti-patterns in your codebase using Ultracite and modern React/Next.js best practices.

## Instructions

When this command is invoked:

1. **Scan the codebase** for common anti-patterns:
   - `var` declarations → `const`/`let`
   - TypeScript `enum` → `as const` objects
   - Array index keys → proper unique keys
   - `any` types → specific types (where obvious)
   - Missing error handling in async functions
   - `useEffect` for derived state → render calculations
   - Client-side data fetching → Server Components
   - Missing accessibility attributes

2. **Show a preview** of all changes before applying:
   - List all files that will be modified
   - Show number of fixes per category
   - Highlight any potentially breaking changes

3. **Ask for confirmation** before making changes

4. **Apply fixes** in order of safety:
   - First: Safe automated fixes (var → const, enum → as const)
   - Second: Structural changes (component refactoring)
   - Third: Manual review needed (complex logic changes)

5. **Generate a report** of all changes made:
   - Files modified
   - Types of fixes applied
   - Any remaining manual fixes needed

## Safety Features

- **Backup recommendation**: Suggest committing current changes first
- **Dry run mode**: Show what would change without applying
- **Selective fixing**: Allow fixing specific patterns only
- **Test reminder**: Remind to run tests after fixes

## Example Usage

```
/fix-patterns
# Interactive mode - shows all fixable issues

/fix-patterns --dry-run
# Preview changes without applying

/fix-patterns --type=var
# Fix only var declarations

/fix-patterns web/src/app
# Fix patterns in specific directory
```

## Pattern Categories

### 1. Type Safety
- Replace `any` with proper types
- Remove non-null assertions where safe
- Convert enums to const objects
- Add missing type annotations

### 2. Modern JavaScript
- var → const/let
- function expressions → arrow functions
- string concatenation → template literals
- Math.pow → ** operator

### 3. React Patterns
- Index keys → proper keys
- Nested components → top-level components
- useEffect for derived state → calculations
- Missing hook dependencies

### 4. Next.js App Router
- Client-side fetch → Server Components
- API routes for internal data → Server Actions
- <img> → next/image

### 5. Accessibility
- Missing button type attributes
- Poor alt text
- Missing ARIA labels
- Keyboard event handlers

### 6. Error Handling
- Unhandled promises
- Missing try-catch blocks
- Throwing non-Error objects
- Missing error messages
