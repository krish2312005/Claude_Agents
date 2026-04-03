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
| `dev-environment-initiator` | Wires up dev env, validates full app runs | After backend + frontend done |
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
    └── backend-architecture-designer   │         └── git-manager
            └── backend-expert ─────────┘                └── deployment-expert
```

**Parallel pairs** (run simultaneously when both needed):
- `uiux-designer` ‖ `backend-architecture-designer`
- `backend-expert` ‖ `frontend-expert`

---

## Key Documentation Files

All agents read and write from `docs/`. Never delete these mid-project:

| File | Produced By | Read By |
|------|-------------|---------|
| `docs/TECH_STACK.md` | tech-stack-expert | All agents |
| `docs/DESIGN_SYSTEM.md` | uiux-designer | frontend-planner, frontend-expert |
| `docs/BACKEND_ARCHITECTURE.md` | backend-architecture-designer | backend-expert, frontend-expert, dev-environment-initiator |
| `docs/FRONTEND_ARCHITECTURE.md` | frontend-planner | frontend-expert |
| `docs/ROUTE_MAP.md` | frontend-planner | frontend-expert |
| `docs/DEV_SETUP.md` | dev-environment-initiator | deployment-expert |
| `docs/PRODUCTION_DEPLOYMENT.md` | deployment-expert | — |
| `docs/PROJECT_PROGRESS.md` | project-manager | project-manager (every session) |

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