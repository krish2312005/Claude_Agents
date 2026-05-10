# Claude Code - Agent Workflow Guide

> Multi-agent orchestration system for comprehensive software development.

---

## Overview

This setup enables sophisticated multi-agent development workflows with **12 specialized agents** that work together to build complete software products. Each agent is a domain expert with deep knowledge in their area.

### Key Features

- **Memory System** (`docs/MEMORY.md`) - Shared context accessible by all agents
- **Timeline System** (`docs/TIMELINE.md`) - Complete chronological history of all work
- **Security Expert** - Comprehensive security reviews and vulnerability assessments
- **Parallel Execution** - Backend and frontend built simultaneously
- **God Mode Agents** - In-depth, expert-level agents for every domain

---

## Agent Roster

| Agent | Role | When to Invoke |
|-------|------|---------------|
| **project-manager** | Master orchestrator - coordinates all agents | Always first |
| **tech-stack-expert** | Technology selection and evaluation | New project, tech change |
| **uiux-designer** | Visual design, design system, component styles | UI projects, redesigns |
| **backend-architecture-designer** | API design, database schema, auth system | Backend planning |
| **frontend-planner** | Pages, routes, component architecture | Frontend planning |
| **backend-expert** | Backend implementation, APIs, business logic | Backend development |
| **frontend-expert** | Frontend implementation, UI, components | Frontend development |
| **dev-environment-initiator** | Dev environment setup, integration | Environment setup |
| **security-expert** | Security audits, vulnerability assessment | Security reviews |
| **deployment-expert** | Production deployment, CI/CD, monitoring | Deployment |
| **test-agent** | Testing strategy, test implementation | Quality assurance |
| **git-manager** | Git workflow, commits, PRs | Code commits |

---

## Agents in God Mode

Each agent is designed as an **in-depth, expert-level specialist** with:

### project-manager
- Full orchestration of all other agents
- Dependency management and workflow coordination
- Memory and timeline integration oversight
- Progress tracking and reporting

### tech-stack-expert
- 20+ years experience in technology strategy
- Comprehensive tech evaluation framework
- Integration and compatibility analysis
- Production-ready stack recommendations

### security-expert
- Principal Security Engineer expertise
- Comprehensive vulnerability assessment
- Compliance and security auditing
- Security best practices enforcement

### backend-expert
- 15+ years backend development experience
- Full-stack backend implementation
- Security, performance, and scalability focus
- Clean architecture and best practices

### frontend-expert
- 15+ years frontend development experience
- Accessible, performant, responsive UI
- Design system compliance
- Modern frontend patterns

### Other Expert Agents
- Similar god-mode depth in their respective domains
- Comprehensive documentation and standards
- Memory and timeline integration
- Quality assurance at every step

---

## Commands

Use these terminal commands to launch agents:

```
/build <project description>  - Full project build with all agents
/feature <feature description> - Add new feature to existing project
/fix <issue description> - Fix a bug or issue
/deploy - Deploy project to production
```

### Direct Agent Invocation

```bash
# Start with project manager
claude --agent project-manager

# Or invoke specialists directly
claude --agent tech-stack-expert
claude --agent security-expert
claude --agent backend-expert
claude --agent frontend-expert
```

---

## Memory and Timeline Systems

### Memory System (`docs/MEMORY.md`)

The memory system provides shared context for all agents:

- **Project Context**: High-level goals and requirements
- **Technology Decisions**: Tech stack choices and rationale
- **Design Decisions**: Design system and visual choices
- **Architecture Decisions**: Backend design and API structure
- **Security Considerations**: Security requirements and constraints
- **Agent Activities**: Summary of who did what

**All agents must:**
1. Read MEMORY.md at the start of each session
2. Update MEMORY.md after significant work
3. Never delete historical context

### Timeline System (`docs/TIMELINE.md`)

Complete chronological history of all project activities:

- **Timestamped Entries**: Every action recorded with date/time
- **Agent Attribution**: Know which agent performed each action
- **Complete History**: Never delete past entries
- **Detailed Logging**: Files created, decisions made, deliverables

**All agents must:**
1. Log activities with timestamps
2. Record all deliverables
3. Preserve all historical entries

---

## Dependency Graph

```
tech-stack-expert
    ├── uiux-designer ────────────────┐
    │       └── frontend-planner       │
    │               └── frontend-expert┤
    │                                   ├── dev-environment-initiator
    └── backend-architecture-designer  │         ├── git-manager
            └── backend-expert ───────┘                └── deployment-expert
                                │
                    security-expert ◄───────────────┘
                                │
                            git-manager
```

**Parallel pairs (run simultaneously):**
- `uiux-designer` ‖ `backend-architecture-designer`
- `backend-expert` ‖ `frontend-expert`

---

## Documentation Files

All agents read and write from the `docs/` directory:

| File | Purpose |
|------|---------|
| `docs/MEMORY.md` | Shared project memory and context |
| `docs/TIMELINE.md` | Complete chronological history |
| `docs/TECH_STACK.md` | Technology decisions |
| `docs/DESIGN_SYSTEM.md` | Visual design system |
| `docs/BACKEND_ARCHITECTURE.md` | Backend API and database design |
| `docs/FRONTEND_ARCHITECTURE.md` | Frontend structure and routes |
| `docs/ROUTE_MAP.md` | Quick reference route list |
| `docs/DEV_SETUP.md` | Development environment setup |
| `docs/PRODUCTION_DEPLOYMENT.md` | Production deployment docs |
| `docs/SECURITY_AUDIT.md` | Security review findings |

---

## Example Usage

### Start a New Project

```
/build create a task management SaaS with user authentication and team dashboard
```

The project-manager will:
1. Invoke tech-stack-expert for technology selection
2. Spawn uiux-designer and backend-architecture-designer in parallel
3. Coordinate frontend and backend implementation
4. Run security expert for security review
5. Set up development environment
6. Deploy to production

### Fix a Bug

```
/fix users cannot upload files larger than 5MB
```

The project-manager will:
1. Analyze the issue
2. Invoke backend-expert to fix the issue
3. Run security-expert if needed
4. Commit and deploy

---

## Agent Workflows

### New Project Workflow

1. `project-manager` - Orchestrate the workflow
2. `tech-stack-expert` - Select technologies
3. `uiux-designer` + `backend-architecture-designer` - Design in parallel
4. `frontend-planner` - Plan frontend structure
5. `backend-expert` + `frontend-expert` - Implement in parallel
6. `security-expert` - Security review
7. `dev-environment-initiator` - Set up environment
8. `test-agent` - Testing
9. `git-manager` - Commit and push
10. `deployment-expert` - Deploy to production

### Feature Addition Workflow

1. `project-manager` - Assess scope
2. `tech-stack-expert` (if new tech needed)
3. `backend-architecture-designer` (if API changes)
4. `frontend-planner` (if new pages)
5. `backend-expert` + `frontend-expert`
6. `git-manager`

---

## Memory and Timeline Integration

Every agent follows these rules:

1. **Start**: Read `docs/MEMORY.md` and `docs/TIMELINE.md`
2. **Work**: Perform assigned tasks
3. **Document**: Update MEMORY.md with key decisions
4. **Log**: Add entries to TIMELINE.md with timestamps
5. **Never Delete**: Preserve all historical timeline entries

---

## Security-First Approach

The `security-expert` agent provides:

- Authentication and authorization auditing
- Data protection review
- Input validation verification
- API security assessment
- Infrastructure security review
- Security documentation

---

## Usage Scope

This setup is designed for **personal and professional use** with comprehensive multi-agent capabilities.

---

## Requirements

- Claude Code CLI installed
- Git configured
- Access to Claude API
- Node.js (for JavaScript/TypeScript projects)

---

## License

MIT License