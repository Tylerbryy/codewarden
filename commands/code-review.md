---
description: Perform comprehensive code review with Ultracite and React/Next.js best practices
---

# Code Review Command

Perform a thorough code review of specified files or the entire codebase, checking for:

1. **Code Quality**: Apply Ultracite rules for TypeScript/JavaScript
2. **React Patterns**: Verify React 19 and Next.js App Router best practices
3. **Security**: Check for common vulnerabilities and security issues
4. **Accessibility**: Ensure WCAG compliance and proper a11y attributes
5. **Performance**: Identify performance bottlenecks and optimization opportunities

## Instructions

When this command is invoked:

1. Ask which files/directories to review (or review recent changes if not specified)
2. Use the Ultracite and React Next Modern skills to analyze the code
3. Provide a structured report with:
   - **Summary**: Overview of findings
   - **Critical Issues**: Must-fix problems
   - **Warnings**: Should-fix improvements
   - **Suggestions**: Nice-to-have enhancements
   - **Code Examples**: Show before/after for key issues

4. Prioritize findings by severity:
   - 🔴 **Critical**: Security vulnerabilities, breaking changes
   - 🟡 **Warning**: Type safety, accessibility issues
   - 🔵 **Info**: Style improvements, optimizations

5. For each issue, provide:
   - File path and line number
   - Clear explanation of the problem
   - Specific fix recommendation
   - Code example if applicable

## Example Usage

```
/code-review
# Reviews recent git changes

/code-review web/src/app
# Reviews specific directory

/code-review web/src/components/Auth.tsx
# Reviews specific file
```
