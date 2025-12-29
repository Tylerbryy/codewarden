# UI/UX Guidelines - Agent Integration Reference

## Contents
- Purpose and activation patterns
- Integration with other CodeWarden skills
- Priority levels for violations
- Vercel-specific guidelines handling
- Common review workflows

---

## Purpose

The UI/UX Guidelines skill enforces best practices for accessible, performant, and delightful interfaces. This reference helps Claude Code agents:
- Understand when to activate the skill
- Apply guidelines in context
- Integrate with other CodeWarden skills
- Prioritize findings appropriately

## When to Activate

### Automatic Activation Triggers

The skill should activate when:
- **User mentions**: "review UI", "check accessibility", "improve UX", "review form", "check interactions"
- **File context**: Working with `.tsx`, `.jsx`, `.vue`, or `.svelte` files containing UI components
- **Code patterns**: Forms, inputs, buttons, navigation, animations, modals, dialogs

### Manual Invocation

Users can explicitly request:
- "Review this component for accessibility"
- "Check if this follows UI/UX best practices"
- "Improve the user experience of this form"
- "Verify keyboard navigation works correctly"

## Integration with Other Skills

### With Ultracite (Code Quality)

**Ultracite focuses on:**
- Type safety (no `any`, proper TypeScript patterns)
- Code structure and organization
- Linting rules (unused variables, consistent formatting)

**UI/UX Guidelines focuses on:**
- Accessibility attributes (`aria-label`, semantic HTML)
- User interactions (keyboard navigation, touch targets)
- Visual design (contrast, spacing, responsive behavior)

**Together:** Ensure components are both technically correct AND user-friendly.

**Example workflow:**
1. Ultracite: Check TypeScript types, proper React patterns
2. UI/UX: Check accessibility, keyboard support, mobile responsiveness
3. Result: Type-safe, accessible, delightful component

### With React Next Modern (Architecture)

**React Next Modern focuses on:**
- Server Components vs Client Components
- Data fetching patterns (async Server Components)
- Server Actions for mutations
- Performance optimization (bundle size, waterfalls)

**UI/UX Guidelines focuses on:**
- Client-side interactions and animations
- Form behavior and validation
- Progressive enhancement
- Visual feedback and loading states

**Together:** Build server-rendered, accessible, interactive applications.

**Example workflow:**
1. React Next: Ensure proper Server/Client boundary, async data fetching
2. UI/UX: Add client-side interactivity, form validation, loading states
3. Result: Fast, accessible, interactive application

### Combined Review Pattern

When reviewing UI code, all three skills work together:

```
1. Ultracite Review
   - Type safety ✓
   - No linting errors ✓
   - Proper React patterns ✓

2. React Next Review
   - Server Component for data fetching ✓
   - Server Action for form submission ✓
   - No client-side data fetching ✓

3. UI/UX Review
   - Keyboard navigation ✓
   - ARIA labels ✓
   - Mobile touch targets ✓
   - Loading states ✓
   - Error handling ✓
```

## Priority Levels

### Critical (Must Fix)

**Accessibility violations:**
- Missing keyboard navigation
- Missing or incorrect ARIA labels
- Insufficient color contrast (fails APCA minimum)
- Missing focus indicators
- Form inputs without labels

**Security issues:**
- Blocking password managers unnecessarily
- Missing autocomplete attributes for sensitive fields
- XSS vulnerabilities in user-generated content

**Performance blockers:**
- Layout thrashing (reading/writing layout properties in loops)
- Missing image dimensions causing CLS
- Animations without `prefers-reduced-motion` support

**Examples:**
```tsx
// CRITICAL: Missing keyboard support
<div onClick={handleClick}>Click me</div>

// CRITICAL: Icon button without label
<button><TrashIcon /></button>

// CRITICAL: Blocking password manager
<input type="password" autoComplete="off" />
```

### High (Should Fix)

**Suboptimal UX:**
- Small hit targets (<44px on mobile)
- Missing loading states or feedback
- Poor error messages (vague, no guidance)
- Missing progressive enhancement

**Form issues:**
- No validation feedback
- Submit button doesn't disable during submission
- Missing unsaved changes warning

**Examples:**
```tsx
// HIGH: Small mobile hit target
<button className="w-4 h-4">×</button>

// HIGH: Vague error message
<div>Error occurred</div>

// HIGH: No loading state
<button onClick={handleSubmit}>Submit</button>
```

### Medium (Consider Fixing)

**Style consistency:**
- Non-layered shadows
- Nested radii don't match parent
- Inconsistent color hue in borders/shadows

**Copywriting:**
- Vercel-specific style guide violations (if not using Vercel brand)
- Passive voice in button labels
- Inconsistent terminology

**Edge cases:**
- Missing overflow handling for very long content
- Suboptimal tooltip timing

**Examples:**
```tsx
// MEDIUM: Flat shadow (could be layered)
<div className="shadow-lg">...</div>

// MEDIUM: Passive button label
<button>Deployment will be created</button>
```

## Vercel-Specific Guidelines

The **Copywriting Guidelines** section reflects Vercel's internal style guide. When reviewing for other companies:

**Always apply (universal principles):**
- Error messages should guide recovery
- Button labels should be specific, not generic
- Use positive language ("Try again" vs "Failed")
- Avoid ambiguity

**Apply selectively (Vercel-specific style):**
- Title Case for headings (vs sentence case)
- Numerals for all numbers (vs spelling out small numbers)
- `&` instead of "and" in UI text
- Specific placeholder formats

**Example:**
```tsx
// Universal (always apply): Specific, actionable button
<button>Save API Key</button>  // ✓ Good
<button>Continue</button>       // ✗ Vague

// Vercel-specific (optional): Title Case
<h2>Deploy Your Project</h2>   // Vercel style
<h2>Deploy your project</h2>   // Also acceptable
```

## Common Review Workflows

### Workflow 1: Form Review

When reviewing a form component:

1. **Check Ultracite rules**
   - Proper TypeScript types for form data
   - No `any` types
   - Form validation schema properly typed

2. **Check React Next rules**
   - Using Server Action for submission?
   - Progressive enhancement (works without JS)?
   - Proper error handling and revalidation?

3. **Check UI/UX rules**
   - All inputs have labels?
   - Keyboard navigation works (Tab, Enter)?
   - Error messages inline next to fields?
   - Submit button shows loading state?
   - Password manager compatible?
   - Touch targets ≥44px on mobile?

4. **Report findings by priority**
   - Critical: Missing labels, blocked password managers
   - High: No loading state, poor error messages
   - Medium: Copywriting style inconsistencies

### Workflow 2: Interactive Component Review

When reviewing buttons, modals, dialogs, or interactive widgets:

1. **Check Ultracite rules**
   - Proper types for props and state
   - No unused variables or imports

2. **Check UI/UX rules**
   - Keyboard support (Esc to close, Tab to navigate)?
   - Focus management (trap focus in modal, return focus on close)?
   - ARIA attributes correct?
   - Touch targets adequate?
   - Loading/disabled states handled?

3. **Check animations (if present)**
   - `prefers-reduced-motion` support?
   - Using compositor-friendly properties?
   - Not using `transition: all`?

### Workflow 3: Responsive Layout Review

When reviewing responsive layouts:

1. **Check breakpoints**
   - Mobile (≤640px): Touch targets ≥44px?
   - Tablet (641-1024px): Layout adapts gracefully?
   - Desktop (>1024px): Content doesn't stretch too wide?

2. **Check safe areas**
   - Mobile notches/insets respected?
   - Using `env(safe-area-inset-*)` where needed?

3. **Check overflow**
   - No unwanted scrollbars?
   - Long content handled gracefully?
   - Tested with very long user-generated content?

### Workflow 4: Performance Review

When reviewing for performance:

1. **Check React Next rules**
   - No client-side data fetching that could be Server Component?
   - No request waterfalls?
   - Proper code splitting?

2. **Check UI/UX performance rules**
   - Images have dimensions (no CLS)?
   - Large lists virtualized?
   - Expensive work moved to Web Workers?
   - Animations use `transform`/`opacity` only?

## Example Agent Responses

### Example 1: Accessibility Violation (Critical)

```
Found CRITICAL accessibility violation in LoginForm.tsx:47

❌ Icon button without accessible label:
<button onClick={handleClose}><XIcon /></button>

✓ Fix: Add descriptive aria-label:
<button onClick={handleClose} aria-label="Close dialog"><XIcon /></button>

Priority: CRITICAL
Reason: Screen reader users cannot understand button purpose
Reference: SKILL.md line 136
```

### Example 2: Performance Issue (Critical)

```
Found CRITICAL performance issue in ProductList.tsx:23

❌ Missing image dimensions causing CLS:
<img src={product.image} alt={product.name} />

✓ Fix: Add explicit dimensions:
<img
  src={product.image}
  alt={product.name}
  width={400}
  height={300}
/>

Priority: CRITICAL
Reason: Causes layout shift, hurts Core Web Vitals
Reference: SKILL.md line 153
```

### Example 3: Copywriting Issue (Medium)

```
Found MEDIUM copywriting issue in DeployButton.tsx:12

❌ Passive, vague button label:
<button>Your deployment will be created</button>

✓ Fix: Active, specific label:
<button>Create Deployment</button>

Priority: MEDIUM
Reason: Vercel style prefers active voice; "Deploy" more concise
Reference: SKILL.md line 183 (Copywriting Guidelines)
Note: This is a Vercel-specific style preference
```

## Summary

Use this reference to:
- **Activate skill** when reviewing UI/UX code
- **Integrate** with Ultracite and React Next Modern skills
- **Prioritize** findings (Critical > High > Medium)
- **Handle** Vercel-specific guidelines appropriately
- **Follow** common review workflows for consistency

The UI/UX Guidelines skill ensures interfaces are accessible, performant, and delightful while working seamlessly with CodeWarden's other quality enforcement skills.
