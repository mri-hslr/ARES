# ARES — Project Knowledge Index

This file explains the purpose and priority of every document in the ARES project.

## 1. Project identity

ARES (Autonomous Robotic Exploration System) is an educational robotics and AI engineering project inspired by publicly documented NASA/JPL planetary exploration systems.

## 2. Document hierarchy

### Level 1 — Project specification
- MASTER_PROMPT.md: Complete project requirements, modules, teaching methodology and roadmap.
- PROJECT_CHARTER.md: Authoritative project vision, objectives, non-goals and safety requirements.

### Level 2 — Technical design
- SYSTEM_ARCHITECTURE.md: System architecture and module responsibilities.
- INTERFACES.md: Data structures, function signatures and module contracts.
- DECISIONS.md: Accepted and proposed engineering decisions.

### Level 3 — Execution and progress
- ROADMAP.md: Project phases and completion criteria.
- CURRENT_STATE.md: Latest verified project state.
- TASKS.md: Active, completed, pending and blocked tasks.
- LEARNING_LOG.md: Developer knowledge, learning gaps and unresolved doubts.

### Level 4 — Repository guidance
- README.md: Repository overview and setup.
- CLAUDE.md: Instructions for Claude Code.
- PROJECT_INSTRUCTIONS.md: Instructions for Claude.ai.
- PROJECT_DESCRIPTION.txt: Short project description.

## 3. Authority rules

1. PROJECT_CHARTER.md governs project objectives and non-negotiable safety requirements.
2. MASTER_PROMPT.md governs the detailed technical mentoring methodology and intended capabilities.
3. SYSTEM_ARCHITECTURE.md and accepted entries in DECISIONS.md govern approved technical design.
4. CURRENT_STATE.md and actual source code determine implementation status.
5. ROADMAP.md and TASKS.md govern development priorities.
6. INTERFACES.md governs approved module contracts.
7. LEARNING_LOG.md tracks the developer's learning progress.

If documents contradict one another, identify the contradiction and request clarification. Never silently invent a resolution.

## 4. Critical instruction

These documents are persistent project references, not proof that their described features have been implemented.

Always inspect actual code and tests before reporting implementation status.

At the beginning of a new session, recover the current state from the latest project documents and available repository files.