---
description: Perform comprehensive security audit of the codebase
---

# Security Audit Command

Perform a thorough security audit of your application, focusing on common vulnerabilities in React/Next.js applications, Server Actions, API routes, and authentication flows.

## Instructions

When this command is invoked:

1. **Scan for common vulnerabilities**:

   **Server Action Security**
   - Missing authentication checks
   - Missing input validation (Zod schemas)
   - Unsafe FormData handling
   - SQL injection risks
   - Closure-based actions with sensitive data

   **Authentication & Authorization**
   - Hardcoded credentials or API keys
   - Exposed environment variables (not NEXT_PUBLIC_*)
   - Missing rate limiting
   - Insecure session handling
   - Missing CSRF protection

   **Data Exposure**
   - Sensitive data in client bundles
   - Database queries without authorization checks
   - API endpoints without authentication
   - Overly permissive CORS settings
   - Logs containing sensitive information

   **Input Validation**
   - Unvalidated user input
   - Missing sanitization before DB queries
   - XSS vulnerabilities in dangerouslySetInnerHTML
   - Path traversal risks in file operations

   **Dependency Security**
   - Outdated packages with known vulnerabilities
   - Unused dependencies

2. **Generate security report**:

   **Critical (🔴 Fix Immediately)**
   - Authentication bypasses
   - SQL injection vulnerabilities
   - Exposed secrets
   - XSS vulnerabilities

   **High (🟠 Fix Soon)**
   - Missing rate limiting
   - Weak input validation
   - Insecure data exposure
   - Missing authorization checks

   **Medium (🟡 Address)**
   - Outdated dependencies
   - Missing security headers
   - Insufficient error handling
   - Weak password requirements

   **Low (🔵 Consider)**
   - Security best practices
   - Code quality improvements
   - Documentation gaps

3. **Provide remediation guidance**:
   - Specific fix for each issue
   - Code examples
   - Links to security resources
   - Testing recommendations

## Security Checklist

### Server Actions
```tsx
// ❌ BAD: No authentication, no validation
"use server"
export async function deleteUser(userId: string) {
  await db.delete(users).where(eq(users.id, userId))
}

// ✅ GOOD: Auth + validation + authorization
"use server"
import { z } from 'zod'
import { auth } from '@/lib/auth'

const schema = z.object({
  userId: z.string().uuid()
})

export async function deleteUser(userId: string) {
  // 1. Authenticate
  const session = await auth()
  if (!session?.user) throw new Error('Unauthorized')

  // 2. Validate input
  const { userId: validId } = schema.parse({ userId })

  // 3. Authorize (check ownership/permissions)
  if (session.user.role !== 'admin' && session.user.id !== validId) {
    throw new Error('Forbidden')
  }

  // 4. Execute
  await db.delete(users).where(eq(users.id, validId))

  // 5. Audit log
  await logAction('delete_user', { userId: validId, by: session.user.id })
}
```

### Environment Variables
```tsx
// ❌ BAD: Exposing secret in client
"use client"
const apiKey = process.env.SECRET_API_KEY // Exposed in bundle!

// ✅ GOOD: Use on server only
// Server Component or Server Action
const apiKey = process.env.SECRET_API_KEY // Never sent to client

// ✅ GOOD: Public vars explicitly marked
"use client"
const publicKey = process.env.NEXT_PUBLIC_API_KEY // OK to expose
```

### SQL Injection Prevention
```tsx
// ❌ BAD: String interpolation = SQL injection
const results = await db.execute(
  `SELECT * FROM users WHERE email = '${userInput}'`
)

// ✅ GOOD: Parameterized queries
const results = await db.select()
  .from(users)
  .where(eq(users.email, userInput))

// ✅ GOOD: Validated input
const schema = z.object({ email: z.string().email() })
const { email } = schema.parse({ email: userInput })
const results = await db.select().from(users).where(eq(users.email, email))
```

### XSS Prevention
```tsx
// ❌ BAD: Unescaped user content
<div dangerouslySetInnerHTML={{ __html: userComment }} />

// ✅ GOOD: Sanitize first
import DOMPurify from 'isomorphic-dompurify'
<div dangerouslySetInnerHTML={{
  __html: DOMPurify.sanitize(userComment)
}} />

// ✅ BETTER: Avoid dangerouslySetInnerHTML
<div>{userComment}</div> // React escapes automatically
```

### Rate Limiting
```tsx
// ✅ GOOD: Rate limit sensitive actions
"use server"
import { Ratelimit } from '@upstash/ratelimit'

const ratelimit = new Ratelimit({
  redis: Redis.fromEnv(),
  limiter: Ratelimit.slidingWindow(10, '1 h'),
})

export async function sendEmail(formData: FormData) {
  const session = await auth()
  if (!session?.user) throw new Error('Unauthorized')

  const { success } = await ratelimit.limit(session.user.id)
  if (!success) {
    return { error: 'Too many requests. Try again later.' }
  }

  // Send email...
}
```

## Example Usage

```
/security-audit
# Full security audit

/security-audit --server-actions
# Audit Server Actions only

/security-audit --critical-only
# Show only critical issues

/security-audit web/src/app/api
# Audit specific directory

/security-audit --fix
# Auto-fix safe issues (with confirmation)
```

## Reporting

Generate reports in multiple formats:
- **Console**: Interactive terminal output
- **Markdown**: `security-report.md` for documentation
- **JSON**: `security-audit.json` for CI/CD integration
- **SARIF**: For GitHub Security tab integration

## Integration

Can be run as:
- **CLI command**: `/security-audit`
- **Git hook**: Pre-commit/pre-push
- **CI/CD**: GitHub Actions, etc.
- **Scheduled**: Daily/weekly automated scans
