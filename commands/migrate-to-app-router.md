---
description: Migrate Next.js Pages Router code to modern App Router with Server Components
---

# Migrate to App Router Command

Guide migration from Next.js Pages Router to the modern App Router architecture with Server Components, Server Actions, and React 19 patterns.

## Instructions

When this command is invoked:

1. **Analyze current setup**:
   - Detect if project uses Pages Router (`pages/` directory)
   - Identify API routes that can become Server Actions
   - Find client-side data fetching to move to server
   - Locate `getServerSideProps`/`getStaticProps` usage

2. **Create migration plan**:
   - List all pages to migrate
   - Identify shared layouts
   - Map API routes → Server Actions
   - Plan Server vs Client Component boundaries

3. **Execute migration** (with user confirmation at each step):

   **Step 1: Setup App Directory**
   - Create `app/` directory
   - Set up root layout with metadata
   - Configure parallel running (if needed)

   **Step 2: Migrate Pages**
   - Convert pages to Server Components
   - Move `getServerSideProps` logic into component
   - Extract client interactivity to Client Components
   - Update imports and exports

   **Step 3: Convert Data Fetching**
   - Remove `useEffect` data fetching
   - Create cached data fetching functions
   - Implement `use()` for streaming where needed
   - Set up proper loading/error boundaries

   **Step 4: Migrate API Routes**
   - Convert form handlers → Server Actions
   - Keep webhook endpoints as Route Handlers
   - Add Zod validation to actions
   - Implement proper authentication

   **Step 5: Update Components**
   - Split large Client Components
   - Use composition for Server/Client mixing
   - Implement React 19 form hooks
   - Add optimistic updates where appropriate

4. **Validation**:
   - Verify all routes work
   - Check data fetching correctness
   - Test form submissions
   - Validate SEO/metadata

5. **Cleanup**:
   - Remove old Pages Router code (after confirmation)
   - Update documentation
   - Remove unused dependencies

## Migration Patterns

### Page Migration

**Before (Pages Router):**
```tsx
// pages/dashboard.tsx
export async function getServerSideProps() {
  const data = await fetchDashboardData()
  return { props: { data } }
}

export default function Dashboard({ data }) {
  return <DashboardUI data={data} />
}
```

**After (App Router):**
```tsx
// app/dashboard/page.tsx
export default async function Dashboard() {
  const data = await fetchDashboardData()
  return <DashboardUI data={data} />
}
```

### API Route → Server Action

**Before:**
```tsx
// pages/api/update-profile.ts
export default async function handler(req, res) {
  const { name } = req.body
  await updateUser(name)
  res.json({ success: true })
}
```

**After:**
```tsx
// actions/profile.ts
"use server"

export async function updateProfile(formData: FormData) {
  const session = await auth()
  if (!session) return { error: 'Unauthorized' }

  const name = formData.get('name')
  await updateUser(session.user.id, name)
  revalidatePath('/profile')
  return { success: true }
}
```

### Client Fetch → Server Component

**Before:**
```tsx
"use client"

function Users() {
  const [users, setUsers] = useState([])

  useEffect(() => {
    fetch('/api/users').then(r => r.json()).then(setUsers)
  }, [])

  return <UserList users={users} />
}
```

**After:**
```tsx
// Server Component
async function Users() {
  const users = await db.query.users.findMany()
  return <UserList users={users} />
}
```

## Example Usage

```
/migrate-to-app-router
# Full interactive migration

/migrate-to-app-router --analyze-only
# Just show migration plan without executing

/migrate-to-app-router pages/dashboard.tsx
# Migrate specific page

/migrate-to-app-router --api-routes
# Convert API routes to Server Actions only
```

## Safety Checklist

Before migration:
- ✅ Commit all current changes
- ✅ Ensure tests pass
- ✅ Backup database if needed
- ✅ Review breaking changes in Next.js version

During migration:
- ✅ Keep Pages Router running in parallel initially
- ✅ Migrate one route at a time
- ✅ Test each migrated route before continuing
- ✅ Monitor for runtime errors

After migration:
- ✅ Run full test suite
- ✅ Check all forms work
- ✅ Verify SEO/metadata
- ✅ Performance audit
- ✅ Update team documentation
