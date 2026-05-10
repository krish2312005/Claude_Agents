# Claude Code Agent Workflow System

**Production-Grade Multi-Agent Orchestration for Complete Software Development**

A comprehensive system of 12 specialized AI agents that work together to build complete software products from conception to deployment. Each agent is a domain expert with deep knowledge, strict standards, and production-grade capabilities.

---

## 🎯 Quick Start

```bash
# Start a new project
claude --agent project-manager
# Then describe what you want to build

# For specific tasks
claude --agent backend-expert
claude --agent frontend-expert
claude --agent security-expert
```

---

## 📋 Table of Contents

1. [System Overview](#system-overview)
2. [Agent Roster](#agent-roster)
3. [Workflow Patterns](#workflow-patterns)
4. [Memory & Timeline Systems](#memory--timeline-systems)
5. [Documentation Structure](#documentation-structure)
6. [Usage Examples](#usage-examples)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)

---

## 🏗️ System Overview

This orchestration system enables sophisticated multi-agent development workflows with **12 specialized agents** that cover every aspect of software development:

### Key Features

| Feature | Description |
|---------|-------------|
| **12 Specialized Agents** | Each agent is a domain expert with 15-25 years of simulated experience |
| **Production-Grade Standards** | Security, performance, scalability, accessibility baked in |
| **Parallel Execution** | Backend and frontend teams work simultaneously |
| **Memory System** | Shared context accessible by all agents (`docs/MEMORY.md`) |
| **Timeline System** | Complete chronological history (`docs/TIMELINE.md`) |
| **God Mode Depth** | Each agent provides expert-level guidance with extensive examples |
| **Zero-Ambiguity Specs** | Architecture documents are so precise implementation is deterministic |

### Philosophy

- **No Decision Left Unmade**: Architecture agents decide everything; implementation agents execute exactly
- **Security First**: Security expert audits before deployment; standards enforced throughout
- **Documentation Driven**: Every decision, change, and activity is documented
- **Parallel When Possible**: UI/UX + Backend Architecture, then Backend + Frontend
- **Fail Fast, Fail Early**: Validation at each phase prevents downstream issues

---

## 👥 Agent Roster

### 1. project-manager

**Role**: Master orchestrator and workflow coordinator

**When to invoke**: Always first for new projects or major features

**Capabilities**:
- Understands complete agent dependency graph
- Determines which agents are needed based on task
- Invokes agents in correct dependency order
- Tracks progress in `docs/PROJECT_PROGRESS.md`
- Manages parallel execution
- Escalates issues to user when needed

**Output**:
- Coordinated agent invocations
- Progress tracking
- Phase completion status

**Parallel coordination**:
```
tech-stack-expert
    ├── uiux-designer ───────────────┐
    │       └── frontend-planner     │
    │               └── frontend-expert┤
    │                                   ├── dev-environment-initiator
    └── backend-architecture-designer │         ├── git-manager
            └── backend-expert ───────┘                └── deployment-expert
```

---

### 2. tech-stack-expert

**Role**: Technology selection and evaluation specialist

**When to invoke**: Start of every new project, when changing tech stack

**Capabilities**:
- Evaluates 20+ years of technology evolution patterns
- Analyzes project requirements against technology capabilities
- Considers scalability, maintainability, ecosystem, team skills
- Produces comprehensive `docs/TECH_STACK.md`

**Decisions Made**:
- Frontend framework (React, Vue, Svelte, Next.js, etc.)
- Backend framework (Node.js, Python, Go, etc.)
- Database (PostgreSQL, MongoDB, MySQL, etc.)
- ORM (Prisma, Drizzle, SQLAlchemy, TypeORM, etc.)
- Authentication (Clerk, Auth.js, Firebase, custom)
- API style (REST, tRPC, GraphQL, gRPC)
- Hosting platform (Vercel, Railway, AWS, Fly.io)
- Testing frameworks (Jest, Vitest, Playwright)
- CI/CD platform (GitHub Actions, GitLab CI)

**Output**:
- `docs/TECH_STACK.md` with complete technology decisions and rationale
- Recommendations on versions and configurations

---

### 3. uiux-designer

**Role**: Visual design and design systems architect

**When to invoke**: After tech-stack-expert, for any project with a user interface

**Capabilities**:
- Creates complete design systems from brand personality
- Defines color palettes with WCAG AA/AAA compliance
- Specifies typography scales and font families
- Designs component visual specifications
- Defines spacing, shadows, border radius systems
- Motion design with accessibility considerations
- Dark mode support (if applicable)

**Deliverables**:
- `docs/DESIGN_SYSTEM.md` — Complete visual specification
- `tailwind.config.ts` — Full Tailwind configuration
- `src/app/globals.css` — Global styles and CSS variables
- Component specifications (Button, Input, Card, Modal, etc.)

**Design Tokens**:
```
Colors: Primary (50-950), semantic (success, warning, error, info), neutral scale
Typography: Display, H1-H6, body, caption with exact sizes and weights
Spacing: 4px base unit with consistent scale (0.25rem to 6rem)
Radius: 0 to 9999px with named tokens (sm, md, lg, xl, full)
Shadows: xs to 2xl with precise values
Z-index: Defined layer system (0-90)
```

---

### 4. backend-architecture-designer

**Role**: API, database, and authentication system architect

**When to invoke**: After tech-stack-expert, before backend-expert

**Capabilities**:
- Designs complete backend API with every endpoint specified
- Creates database schema with constraints and indexes
- Designs authentication and authorization systems
- Defines error handling and response formats
- Plans for scalability and performance
- Documents security requirements

**Deliverables**:
- `docs/BACKEND_ARCHITECTURE.md` — Complete backend specification (1000+ lines)
- `src/types/index.ts` — TypeScript interfaces
- `.env.example` — Environment variables template

**Architecture Includes**:
1. **API Specification**: Every endpoint with route, method, auth, request/response schemas, error cases
2. **Database Design**: ERD, table specifications with all columns, constraints, indexes, relationships
3. **Authentication Flow**: Registration, login, logout, refresh, password reset
4. **Authorization Model**: RBAC with role definitions and permission matrix
5. **Service Layer Architecture**: Repository pattern, service responsibilities
6. **Error Handling Strategy**: Custom error classes, global handler
7. **Environment Configuration**: All required variables documented
8. **Migration Strategy**: How schema changes are applied

**Specification Example**:
```
## Endpoint: POST /api/posts

**Authentication:** Required (user must be logged in)
**Authorization:** User can create own posts, admin/moderator can create any

Request Body:
{
  title: string (1-200 chars),
  slug: string (unique, lowercase alphanumeric),
  content: string (1-50000 chars),
  published: boolean (default: false)
}

Response (201):
{
  id: UUID,
  authorId: UUID,
  title: string,
  slug: string,
  status: 'draft' | 'published',
  createdAt: ISO string,
  updatedAt: ISO string
}

Error Cases:
400: Validation failed (fieldErrors provided)
401: Not authenticated
409: Slug already exists
```

---

### 5. frontend-planner

**Role**: Frontend architecture and page structure planner

**When to invoke**: After uiux-designer AND tech-stack-expert, before frontend-expert

**Capabilities**:
- Maps complete information architecture
- Defines all pages and routes
- Plans component hierarchy and composition
- Specifies data requirements per page
- Designs layout architecture
- Plans state management approach

**Deliverables**:
- `docs/FRONTEND_ARCHITECTURE.md` — Complete frontend specification
- `docs/ROUTE_MAP.md` — All routes and navigation
- Stub route files in directory structure

**Planning Includes**:
1. **User Journeys**: Anonymous → Registration → Dashboard → Features
2. **Route Map**: Complete hierarchy with auth requirements
3. **Layout Architecture**: Marketing, Auth, App layouts specified
4. **Page-by-Page Specifications**: Every page with sections, components, data needs
5. **Component Inventory**: All components with props and usage
6. **State Management**: React Query, Zustand, or other pattern
7. **Data Fetching**: How each page gets its data
8. **States**: Loading, error, empty states for every page

**Page Specification Template**:
```
## Page: /dashboard — Dashboard

Purpose: User's main hub after login

Sections:
1. Welcome Header
2. Quick Actions (3-5 primary actions)
3. Recent Activity (last 10 items)
4. Stats Cards (2x2 grid)

Components:
- WelcomeHeader: title, subtitle, user avatar
- QuickActions: array of {label, icon, href}
- ActivityFeed: list of {type, description, time}
- StatsCard: {label, value, trend}

Data Requirements:
- GET /api/dashboard/stats
- GET /api/activity/recent?limit=10
- Use React Query with 5min stale time

States:
- Loading: skeleton cards matching layout
- Empty: "Get started" message with CTA
- Error: retry button with error message
```

---

### 6. frontend-expert

**Role**: Frontend implementation specialist

**When to invoke**: After frontend-planner AND uiux-designer

**Capabilities**:
- Implements all pages and components exactly to specification
- Creates accessible, responsive, performant UI
- Integrates with backend APIs
- Follows design system precisely
- Handles all states (loading, error, empty)
- Optimizes bundle size and performance

**Implementation Standards**:
- TypeScript strict mode — no `any` types
- Tailwind CSS exclusively — no inline styles
- Follow design tokens exactly — use tailwind.config.ts
- Accessible by default — semantic HTML, ARIA, focus management
- Mobile-first responsive design
- Performance optimized — lazy loading, memoization, code splitting
- All interactive elements have loading/error/empty states

**Component Patterns**:
```typescript
// Every component follows this structure
interface ButtonProps {
  variant: 'primary' | 'secondary' | 'destructive' | 'ghost';
  size: 'sm' | 'md' | 'lg';
  loading?: boolean;
  disabled?: boolean;
  onClick?: () => void;
  children: React.ReactNode;
}

export default function Button({ variant, size, ...props }: ButtonProps) {
  return (
    <button
      className={cn(
        'btn', // Base styles
        `btn-${variant}`, // Variant styles
        `btn-${size}`, // Size styles
        props.disabled && 'opacity-50 cursor-not-allowed'
      )}
      disabled={props.disabled || props.loading}
      aria-busy={props.loading}
    >
      {props.loading && <Spinner />}
      {props.children}
    </button>
  );
}
```

**Data Fetching Pattern**:
```typescript
export function usePost(id: string) {
  return useQuery({
    queryKey: ['post', id],
    queryFn: () => api.get<Post>(`/posts/${id}`).then(r => r.data),
    enabled: !!id,
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
}

export function useCreatePost() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: (data: CreatePostDto) => api.post<Post>('/posts', data),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['posts'] });
      toast.success('Post created');
    },
  });
}
```

---

### 7. backend-expert

**Role**: Backend implementation specialist

**When to invoke**: After backend-architecture-designer

**Capabilities**:
- Implements all API endpoints exactly as specified
- Writes secure, performant database queries
- Builds authentication and authorization systems
- Creates business logic in service layer
- Writes comprehensive tests
- Optimizes for production

**Implementation Standards**:

```typescript
// 1. Security First
// Password hashing with bcrypt 12 rounds
const hash = await bcrypt.hash(password, 12);

// Parameterized queries only (if ORM not used)
await prisma.$executeRaw`SELECT * FROM users WHERE id = ${id}`;

// Authorization on every endpoint
if (post.authorId !== userId && !isAdmin(userRole)) {
  throw new ForbiddenError();
}

// 2. Error Handling with Custom Errors
class ValidationError extends AppError { /* ... */ }
class UnauthenticatedError extends AppError { /* ... */ }
class ForbiddenError extends AppError { /* ... */ }
class NotFoundError extends AppError { /* ... */ }
class ConflictError extends AppError { /* ... */ }

// 3. Repository Pattern
export class UserRepository {
  async findById(id: string): Promise<User | null> {
    return await prisma.user.findFirst({
      where: { id, deletedAt: null },
    });
  }
}

// 4. Service Layer
export class UserService {
  async createUser(data: CreateUserDto): Promise<User> {
    // Validation
    // Authorization
    // Business logic
    // Call repository
  }
}

// 5. Route Handlers
router.post(
  '/users',
  requireAuth,
  validateBody(createUserSchema),
  async (req, res) => {
    const user = await userService.createUser(req.body, req.user!.id);
    res.status(201).json(ApiResponse.success(user));
  }
);
```

**Testing Strategy**:
- Unit tests on service layer (80-90% coverage)
- Integration tests on API endpoints
- E2E tests on critical flows
- Test fixtures and factories

---

### 8. dev-environment-initiator

**Role**: Development environment and integration specialist

**When to invoke**: After both backend-expert and frontend-expert complete

**Capabilities**:
- Verifies all dependencies installed
- Sets up and configures environment variables
- Initializes and migrates database
- Starts and validates both frontend and backend
- Tests end-to-end functionality
- Creates `docs/DEV_SETUP.md`
- Fixes integration issues

**Phase 1: Environment Verification**
```bash
# Check Node.js version
node --version

# Install dependencies
npm install

# Verify .env exists
ls -la .env
```

**Phase 2: Database Setup**
```bash
# Run migrations
npx prisma migrate deploy

# Seed data (if needed)
npm run db:seed
```

**Phase 3: Build Verification**
```bash
# Type check
npx tsc --noEmit

# Build frontend
npm run build

# Build backend (if separate)
npm run build:server
```

**Phase 4: Start Services**
```bash
# Start backend
npm run dev:server &
# Wait, then check health
curl http://localhost:3001/health

# Start frontend
npm run dev &
# Wait, then check page loads
curl http://localhost:3000
```

**Phase 5: End-to-End Testing**
```bash
# Test registration → login → dashboard
curl -X POST http://localhost:3001/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"test@test.com","password":"Test123!@#","name":"Test"}'

curl -X POST http://localhost:3001/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@test.com","password":"Test123!@#"}'
```

---

### 9. security-expert

**Role**: Security auditing and vulnerability assessment specialist

**When to invoke**: Before deployment, after significant code changes

**Capabilities**:
- Performs comprehensive security audits
- Tests for OWASP Top 10 vulnerabilities
- Reviews authentication and authorization
- Audits data protection practices
- Assesses infrastructure security
- Provides remediation guidance

**Audit Areas**:

1. **Authentication & Authorization**
   - Password hashing (bcrypt ≥12 rounds)
   - JWT token security (expiry, refresh, storage)
   -Session management
   - RBAC implementation
   - MFA availability

2. **Input Validation & Injection**
   - SQL injection prevention
   - XSS protection
   - CSRF protection
   - Command injection
   - Path traversal

3. **API Security**
   - Rate limiting (auth endpoints)
   - CORS configuration (no wildcards)
   - Error message handling
   - API key management

4. **Data Protection**
   - Secrets management (no hardcoding)
   - Encryption at rest and in transit
   - PII handling
   - Database security

5. **Infrastructure**
   - Security headers (CSP, HSTS, X-Frame-Options)
   - Docker security (non-root user)
   - Dependency vulnerabilities
   - SSL/TLS configuration

**Audit Output**: `docs/SECURITY_AUDIT.md`

```
## Security Audit Report

### Critical Findings (Fix Immediately)
1. [CVE-2024-XXXX] Package sqlite3 vulnerable
   Location: package.json (version < 5.1.6)
   Impact: Remote code execution
   Fix: Update to 5.1.6 or later

### High Priority
1. JWT stored in localStorage (XSS vulnerable)
   Location: src/hooks/useAuth.ts:15
   Impact: Session hijacking
   Fix: Use httpOnly cookies

### Medium Priority
1. No rate limiting on /api/auth/login
   Impact: Brute force attacks
   Fix: Add rate limiter middleware
```

---

### 10. test-agent

**Role**: Testing strategy and implementation specialist

**When to invoke**: Throughout development, after features complete

**Capabilities**:
- Designs comprehensive testing strategy
- Implements unit tests (70-80% coverage)
- Implements integration tests (API endpoints)
- Implements E2E tests (critical user journeys)
- Sets up CI/CD test automation
- Creates test fixtures and factories
- Performance and load testing

**Test Pyramid**:
```
     Few
    ┌────┐
    │ E2E│  ← Critical journeys (2-5 tests)
    └────┘
   ┌──────┐
   │Integration│ ← API tests (20-30%)
   └──────┘
  ┌─────────┐
  │   Unit  │ ← Logic/utils (70-80%)
  └─────────┘
   Many
```

**Unit Test Example**:
```typescript
describe('UserService.register', () => {
  it('should hash password before saving', async () => {
    // Arrange
    const input = { email: 'test@test.com', password: 'pass123', name: 'Test' };
    userRepo.findByEmail.mockResolvedValue(null);
    hashUtils.hash.mockResolvedValue('hashed_password');

    // Act
    const result = await userService.register(input);

    // Assert
    expect(hashUtils.hash).toHaveBeenCalledWith('pass123');
    expect(result.passwordHash).toBe('hashed_password');
  });

  it('should throw when email exists', async () => {
    userRepo.findByEmail.mockResolvedValue({ email: 'exists@test.com' });

    await expect(
      userService.register({ email: 'test@test.com', password: 'pass', name: 'T' })
    ).rejects.toThrow('Email already in use');
  });
});
```

**Integration Test Example**:
```typescript
describe('POST /api/auth/register', () => {
  it('should register new user', async () => {
    const response = await request(app)
      .post('/api/auth/register')
      .send({
        email: `test${Date.now()}@example.com`,
        password: 'Test123!@#',
        name: 'Test User',
      });

    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('user.id');
    expect(response.body).toHaveProperty('token');
  });

  it('should reject duplicate email', async () => {
    await prisma.user.create({
      data: { email: 'exists@test.com', passwordHash: 'hash', name: 'Exists' },
    });

    const response = await request(app)
      .post('/api/auth/register')
      .send({
        email: 'exists@test.com',
        password: 'Test123!@#',
        name: 'Duplicate',
      });

    expect(response.status).toBe(409);
    expect(response.body.code).toBe('CONFLICT');
  });
});
```

**E2E Test Example (Playwright)**:
```typescript
test('should allow user to register, login, and access dashboard', async ({ page }) => {
  await page.goto('/register');

  await page.fill('[name="email"]', `test${Date.now()}@example.com`);
  await page.fill('[name="password"]', 'Test123!@#');
  await page.fill('[name="name"]', 'E2E Test');
  await page.click('button[type="submit"]');

  await page.waitForURL('/dashboard');
  await expect(page.locator('[data-testid="user-menu"]')).toBeVisible();
});
```

**Coverage Goals**:
- Services: 80-90%
- Utilities: 70-80%
- Components: 60-70% (snapshot + interaction)
- Endpoints: All covered

---

### 11. git-manager

**Role**: Git workflow and commit management specialist

**When to invoke**: After any agent completes work requiring commits

**Capabilities**:
- Reviews changes with `git status` and `git diff`
- Writes precise Conventional Commit messages
- Ensures no secrets or build artifacts committed
- Handles merge conflicts
- Pushes to remote
- Maintains clean commit history

**Conventional Commits**:
```
feat(auth): implement JWT refresh token rotation
fix(api): prevent duplicate post creation on rapid clicks
refactor(db): extract user queries into dedicated repository
docs(readme): update installation instructions
test(auth): add tests for password reset flow
chore(deps): update dependencies to latest versions
```

**Commit Format**:
```
<type>(<scope>): <description>

[optional body explaining what and why]

[optional footer: Refs: #123, Closes: #456]
```

**Pre-Commit Validation**:
```bash
# Check what will be committed
git status
git diff --stat

# Verify no secrets
grep -rn "password\|secret\|API_KEY" --include="*.ts" --include="*.js"

# Check for node_modules
git diff --name-only | grep node_modules && echo "ERROR"

# Ensure on feature branch (not main)
git branch --show-current | grep -q "feature/" || echo "WARNING: Not on feature branch"
```

---

### 12. deployment-expert

**Role**: Production deployment and DevOps specialist

**When to invoke**: After dev-environment-initiator verifies everything works

**Capabilities**:
- Configures production environment
- Sets up CI/CD pipelines (GitHub Actions)
- Deploys to hosting platform (Vercel, Fly.io, Railway, AWS)
- Configures domains and SSL certificates
- Sets up monitoring (Sentry, uptime monitors)
- Configures database backups
- Documents rollback procedures
- Security hardening

**Deployment Phases**:

**Phase 1: Pre-Deployment Verification**
```bash
# Build succeeds
npm run build

# Type check passes
npx tsc --noEmit

# Tests pass
npm run test:unit && npm run test:integration

# Security audit complete (no critical/high)
```

**Phase 2: Environment Configuration**
- Generate secure secrets (JWT_SECRET, etc.)
- Configure production environment variables
- Set up database connection
- Configure CORS for production domain

**Phase 3: CI/CD Pipeline**
```yaml
# .github/workflows/deploy.yml
name: Deploy to Production
on:
  push:
    branches: [main]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm run typecheck
      - run: npm run lint
      - run: npm run test:unit
      - run: npm run test:integration

  build:
    needs: quality
    runs-on: ubuntu-latest
    steps:
      - run: npm run build
      - uses: actions/upload-artifact@v4
        with:
          name: build
          path: .next

  deploy-backend:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v4
      - run: flyctl deploy --remote-only

  deploy-frontend:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v4
      - run: vercel --prod
```

**Phase 4: Monitoring Setup**
- Health check endpoints (`/health`, `/health/ready`)
- Error tracking (Sentry)
- Uptime monitoring (Better Stack, Pingdom)
- Log aggregation (Datadog, CloudWatch)
- Performance monitoring (Vercel Analytics)

**Phase 5: Documentation**
- `docs/PRODUCTION_DEPLOYMENT.md` with:
  - Infrastructure details
  - URLs and endpoints
  - Environment variables
  - CI/CD pipeline details
  - Rollback procedures
  - Incident response contacts
  - Monitoring dashboards

---

## 🔄 Workflow Patterns

### New Full-Stack Project

```
1. project-manager (orchestrate)
   ↓
2. tech-stack-expert
   ↓
3. Parallel: uiux-designer + backend-architecture-designer
   ↓
4. frontend-planner
   ↓
5. Parallel: backend-expert + frontend-expert
   ↓
6. security-expert (audit)
   ↓
7. dev-environment-initiator (wire up)
   ↓
8. test-agent (comprehensive testing)
   ↓
9. git-manager (commit all changes)
   ↓
10. deployment-expert (production deploy)
```

### Feature Addition (Existing Project)

```
project-manager assesses →
If backend changes: backend-architecture-designer → backend-expert
If frontend changes: frontend-planner → frontend-expert
If both: run both in parallel
↓
git-manager commits
↓
security-expert (if security-impacting)
↓
deployment-expert (if deploying)
```

### Bug Fix

```
project-manager or direct →
backend-expert OR frontend-expert (depending on affected area)
↓
test-agent (add regression test)
↓
git-manager
```

---

## 💾 Memory & Timeline Systems

### Memory System (`docs/MEMORY.md`)

Shared context accessible by all agents. Structured with sections:

```markdown
# Project Memory

## Project Context
- Goal: Task management SaaS for teams
- Scale: Early stage, ~100 users expected
- Timeline: 6 weeks to MVP

## Technology Decisions
- Framework: Next.js 14 with App Router
- Backend: Next.js API Routes + Prisma
- Database: PostgreSQL on Railway
- Auth: Clerk for managed auth

## Design Decisions
- Color: Primary #3B82F6 (blue), secondary #10B981 (green)
- Typography: Inter for UI, JetBrains Mono for code
- Layout: Marketing → Auth → App with sidebar nav
- Dark mode: Supported

## Architecture Decisions
- API: REST with versioning (v1)
- Auth: JWT with httpOnly cookies
- Database: PostgreSQL with Prisma
- Soft deletes on all tables
- Slug-based URLs for posts

## Security Considerations
- Rate limiting: 5/min on auth, 100/min on API
- CORS: Exact origin only, no wildcards
- Security headers: CSP, HSTS, X-Frame-Options
- Password: bcrypt with 12 rounds
```

### Timeline System (`docs/TIMELINE.md`)

Complete chronological history:

```markdown
# Project Timeline

## 2024-01-15

### 10:30: Project Start
- project-manager invoked
- Reading existing documentation

### 11:00: Tech Stack Selected
- tech-stack-expert completed
- Decided: Next.js, Prisma, PostgreSQL, Clerk
- Docs/TECH_STACK.md created

### 12:00: Design Phase Started
- uiux-designer started
- backend-architecture-designer started (parallel)

### 14:30: Design Complete
- uiux-designer completed
- docs/DESIGN_SYSTEM.md created
- tailwind.config.ts configured

### 15:00: Architecture Complete
- backend-architecture-designer completed
- docs/BACKEND_ARCHITECTURE.md created (1200 lines)
- src/types/index.ts created
- .env.example created
```

---

## 📚 Documentation Structure

All agents read from and write to `docs/`:

| File | Created By | Purpose |
|------|------------|---------|
| `MEMORY.md` | All agents | Shared project context |
| `TIMELINE.md` | All agents | Chronological activity log |
| `TECH_STACK.md` | tech-stack-expert | Technology decisions |
| `DESIGN_SYSTEM.md` | uiux-designer | Visual design specification |
| `BACKEND_ARCHITECTURE.md` | backend-architecture-designer | API & database design |
| `FRONTEND_ARCHITECTURE.md` | frontend-planner | Pages and components |
| `ROUTE_MAP.md` | frontend-planner | Quick reference routes |
| `DEV_SETUP.md` | dev-environment-initiator | Local development guide |
| `SECURITY_AUDIT.md` | security-expert | Security findings |
| `PRODUCTION_DEPLOYMENT.md` | deployment-expert | Deployment documentation |
| `TESTING.md` | test-agent | Test strategy and coverage |
| `PROJECT_PROGRESS.md` | project-manager | Current status tracking |

---

## 💡 Usage Examples

### Example 1: Build a Complete SaaS Application

```bash
# Start the orchestrator
claude --agent project-manager

# Tell it what you want:
"I want to build a task management SaaS with:
- User authentication (email/password)
- Team workspaces with multiple users
- Task creation, assignment, and tracking
- Comments and file attachments
- Real-time notifications
- Admin dashboard with analytics"

# The project-manager will automatically:
# 1. Invoke tech-stack-expert to select stack
# 2. Spawn uiux-designer and backend-architecture-designer in parallel
# 3. After designs complete, invoke frontend-planner
# 4. Spawn backend-expert and frontend-expert in parallel
# 5. Run security-expert audit
# 6. Have dev-environment-initiator wire everything together
# 7. Have test-agent create comprehensive tests
# 8. Have git-manager commit all changes
# 9. Have deployment-expert deploy to production
```

### Example 2: Add a New Feature to Existing Project

```bash
# Let project-manager assess scope
claude --agent project-manager

# Describe the feature:
"We need to add real-time chat between users:
- One-on-one messaging
- Group conversations
- File attachments
- Read receipts
- Online status indicators"

# project-manager will:
# - Read existing docs to understand current architecture
# - Determine if backend API changes needed (yes: new endpoints)
# - Determine if frontend changes needed (yes: new pages/components)
# - Invoke backend-architecture-designer
# - After architecture, invoke frontend-planner
# - Spawn backend-expert and frontend-expert in parallel
# - Then security-expert, git-manager, deployment-expert as needed
```

### Example 3: Fix a Bug

```bash
# Invoke project-manager to coordinate
claude --agent project-manager

# Describe the bug:
"Users report that file uploads fail for files larger than 5MB.
The error says 'Request entity too large'."

# project-manager will:
# - Analyze error (likely body parser limit)
# - Invoke backend-expert to fix
# - Have test-agent add regression test
# - Have git-manager commit
# - Possibly deploy immediately
```

### Example 4: Security Review Before Launch

```bash
# Invoke security-expert directly
claude --agent security-expert

# It will:
# - Read all code and documentation
# - Audit authentication and authorization
# - Check for OWASP Top 10 vulnerabilities
# - Review infrastructure configuration
# - Generate docs/SECURITY_AUDIT.md
# - Report critical issues that must be fixed
# - Recommend mitigation for medium/low issues
```

---

## 🎓 Best Practices

### For Project Managers

1. **Always read MEMORY.md and TIMELINE.md first**
2. **Update PROJECT_PROGRESS.md after each significant step**
3. **When agents conflict, pause and resolve with user**
4. **Only invoke agents in proper dependency order**
5. **Log all decisions in MEMORY.md**

### For Architecture Agents

1. **Write specs that leave zero ambiguity**
2. **Document EVERY edge case and error scenario**
3. **Include exact request/response examples**
4. **Specify validation rules precisely**
5. **Document security requirements explicitly**

### For Implementation Agents

1. **Implement EXACTLY what architecture specifies**
2. **If architecture has problems, FLAG IT—don't silently fix**
3. **Write tests for every feature**
4. **Follow established patterns in existing code**
5. **Update MEMORY.md with implementation details**

### For All Agents

1. **NEVER commit secrets** (`.env`, API keys, passwords)
2. **ALWAYS update TIMELINE.md** after work
3. **NEVER delete historical entries** in TIMELINE.md
4. **Use environment variables for configuration**
5. **Log meaningful context in structured format**

---

## 🐛 Troubleshooting

### Issue: Agent produces poor output

**Solution**: Re-invoke with clearer instructions and examples:
```bash
claude --agent frontend-planner
"Please create a detailed frontend architecture.
Reference: docs/BACKEND_ARCHITECTURE.md exists with API endpoints.
User journeys: anonymous → register → dashboard.
Include: route map, all pages, loading states, error states.
Be specific about every component needed."
```

### Issue: Conflicting documentation

**Solution**: Have project-manager mediate:
```bash
claude --agent project-manager
"uiux-designer created DESIGN_SYSTEM.md with blue primary color.
backend-architecture-designer's specs reference green buttons.
Please resolve: which color should be used for primary CTAs?
User says: 'We want blue for everything.'"
```

### Issue: Dependency blocking progress

**Solution**: Check what's missing:
```bash
# Is BACKEND_ARCHITECTURE.md present?
ls docs/BACKEND_ARCHITECTURE.md

# If not, invoke backend-architecture-designer first
claude --agent backend-architecture-designer
```

### Issue: Tests failing repeatedly

**Solution**: Review test setup:
```bash
# Check test database exists
npm run db:setup

# Clean test data
npm run test:clean

# Run single test with debugging
npm run test:unit -- --testNamePattern="specific test" --verbose
```

---

## 📊 Agent Maturity Matrix

| Agent | Maturity | Completeness | Production Ready |
|-------|----------|--------------|-----------------|
| project-manager | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| tech-stack-expert | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| uiux-designer | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| backend-architecture-designer | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| frontend-planner | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| backend-expert | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| frontend-expert | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| dev-environment-initiator | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| security-expert | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| test-agent | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| git-manager | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |
| deployment-expert | ⭐⭐⭐⭐⭐ | 1000+ lines | ✅ |

---

## 🚀 Getting Started

1. **Clone or setup your project**
   ```bash
   mkdir my-project
   cd my-project
   git init
   ```

2. **Start the project manager**
   ```bash
   claude --agent project-manager
   ```

3. **Describe your project**
   ```
   Build a task management application with:
   - User registration and authentication
   - Create/assign tasks with due dates
   - Comments and attachments
   - Team workspaces
   - Email notifications
   ```

4. **Follow the agent workflow**
   - Let the project manager coordinate all agents
   - Review outputs from planning agents
   - Approve when ready to proceed
   - Provide feedback if changes needed

5. **Deploy to production**
   - Let deployment-expert handle the deployment
   - Review PRODUCTION_DEPLOYMENT.md
   - Monitor initial usage

---

## 📝 License

MIT License — Feel free to use this agent system in your projects.

---

## 🤝 Contributing

This is a curated agent system. To suggest improvements:

1. Test the current agents in your projects
2. Document specific issues or gaps
3. Propose enhancements with examples
4. Submit via GitHub issues

---

## 🔗 Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [REST API Best Practices](https://restfulapi.net/)

---

**Built with Claude Code** — The AI-powered development tool that helps you build better software faster.

*Last updated: 2026-01-01*