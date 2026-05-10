# Project Orchestration Guide

## Entry Point

**Always start with the `project-manager` agent.**
Never invoke specialist agents directly for new projects or features — the project-manager coordinates everything.

```bash
# Launch the orchestrator
claude --agent project-manager
```

Then simply describe what you want to build. The project-manager will:
1. Plan the full agent pipeline
2. Confirm the plan with you
3. Invoke each specialist in the correct order
4. Track progress in `docs/PROJECT_PROGRESS.md`
5. Maintain memory and timeline systems

---

## Agent Roster

| Agent | Role | Invoke After |
|-------|------|-------------|
| `project-manager` | Master orchestrator — coordinates all others | Always first |
| `tech-stack-expert` | Picks and documents the tech stack | Start of new project |
| `uiux-designer` | Design system, colors, typography, component styles | After tech-stack-expert |
| `backend-architecture-designer` | API design, database schema, auth architecture | After tech-stack-expert |
| `frontend-planner` | Pages, routes, component map, data requirements | After uiux-designer + tech-stack-expert |
| `backend-expert` | Implements all backend code | After backend-architecture-designer |
| `frontend-expert` | Implements all frontend code | After frontend-planner + uiux-designer |
| `security-expert` | Security audits, vulnerability assessment | Before deployment, during code review |
| `dev-environment-initiator` | Wires up dev env, validates full app runs | After backend + frontend done |
| `test-agent` | Test strategy, test implementation | Throughout development |
| `git-manager` | Commits and pushes all changes | After any code changes |
| `deployment-expert` | Production deploy, CI/CD, SSL, monitoring | After dev-environment-initiator |

---

## Dependency Graph

```
tech-stack-expert
    ├── uiux-designer ──────────────────┐
    │       └── frontend-planner        │
    │               └── frontend-expert ┤
    │                                   ├── dev-environment-initiator
    └── backend-architecture-designer   │         ├── git-manager
            └── backend-expert ─────────┘                └── deployment-expert
                                │
                    security-expert ◄───────────────────┘
                                │
                            test-agent
```

**Parallel pairs** (run simultaneously when both needed):
- `uiux-designer` ‖ `backend-architecture-designer`
- `backend-expert` ‖ `frontend-expert`

---

## Key Documentation Files

All agents read and write from `docs/`. Never delete these mid-project:

| File | Produced By | Read By |
|------|-------------|---------|
| `docs/MEMORY.md` | All agents | All agents |
| `docs/TIMELINE.md` | All agents | All agents |
| `docs/TECH_STACK.md` | tech-stack-expert | All agents |
| `docs/DESIGN_SYSTEM.md` | uiux-designer | frontend-planner, frontend-expert |
| `docs/BACKEND_ARCHITECTURE.md` | backend-architecture-designer | backend-expert, frontend-expert, dev-environment-initiator |
| `docs/FRONTEND_ARCHITECTURE.md` | frontend-planner | frontend-expert |
| `docs/ROUTE_MAP.md` | frontend-planner | frontend-expert |
| `docs/SECURITY_AUDIT.md` | security-expert | All agents before deployment |
| `docs/DEV_SETUP.md` | dev-environment-initiator | deployment-expert |
| `docs/PRODUCTION_DEPLOYMENT.md` | deployment-expert | — |
| `docs/PROJECT_PROGRESS.md` | project-manager | project-manager (every session) |

---

## Memory and Timeline Systems

Every agent MUST integrate with these systems:

### Memory System (`docs/MEMORY.md`)

Shared project context accessible by all agents:

- **Read at Start**: Every agent reads MEMORY.md at start of session
- **Update After Work**: Log key decisions and context
- **Never Delete**: Preserve all historical context

### Timeline System (`docs/TIMELINE.md`)

Complete chronological history of all work:

- **Timestamped Entries**: Every action with datetime
- **Agent Attribution**: Know who did what
- **Append Only**: Never delete past entries
- **Detailed Logging**: Files, decisions, deliverables

### Integration Requirements

All agents must:
1. Read `docs/MEMORY.md` and `docs/TIMELINE.md` at session start
2. Update memory with decisions and context
3. Log activities with timestamps in timeline
4. Preserve all historical entries

---

## Agent Teams (Parallel Execution)

To enable true parallel execution across backend and frontend:

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
claude --agent project-manager
```

Without this flag, agents run sequentially. With it, the project-manager can spawn backend-expert and frontend-expert simultaneously.

---

## For Small Changes (Skip the Orchestrator)

If you're fixing a single isolated issue, invoke the specialist directly:

```bash
# Frontend bug fix
claude --agent frontend-expert

# Backend bug fix
claude --agent backend-expert

# Security review
claude --agent security-expert

# Testing
claude --agent test-agent

# Just commit what's done
claude --agent git-manager

# Deploy to prod
claude --agent deployment-expert
```

---

## Project Conventions

- All docs live in `docs/`
- Environment variables: `.env.example` committed, `.env` never committed
- Commit style: conventional commits (`feat:`, `fix:`, `docs:`, etc.)
- Never push directly to `main` — git-manager will warn you
- TypeScript strict mode everywhere — no `any` types
- All agents must update MEMORY.md and TIMELINE.md with their activities