# Project Memory System

This document tracks the project's memory and context for all agents to ensure consistency and shared understanding across the entire multi-agent system.

## Memory Access

All agents must read this file to understand the current state of the project and maintain context between sessions. The memory system is the single source of truth for project-wide decisions, constraints, and history.

## Memory Structure

```markdown
## Project Context
[Brief overview of what we're building]

## Current Phase
[Which phase of the workflow]

## Technology Decisions
[Summary of tech stack choices]

## Design Decisions
[Summary of design system choices]

## Architecture Decisions
[Summary of backend/API design]

## Security Considerations
[Security requirements and constraints]

## Active Constraints
[Any limitations or requirements to consider]

## Agent Activities Log
[Summary of recent agent activities]

## Project State
[Current status of the project]
```

## Memory Access Rules

1. **Read Memory First**: Every agent must read `docs/MEMORY.md` at the start of each session
2. **Update After Significant Work**: After completing significant work, update the memory
3. **Never Delete Historical Context**: Preserve all past decisions and activities
4. **Maintain Consistency**: Ensure MEMORY.md matches other documentation
5. **Track Agent Interactions**: Document which agents have worked on what

## Writing to Memory

When updating memory, follow this format:

```markdown
## [Date/Time] - Agent Name

<type>
- Summary of work done
- Key decisions made
- Files created/modified
- Next steps
```

## Integration with Timeline

The memory system works alongside `docs/TIMELINE.md` to provide:
- **Memory**: High-level context and decisions
- **Timeline**: Detailed chronological activities

Both must be updated by agents to maintain complete project history.