# ARES — Autonomous Robotic Exploration System

ARES is a student-built research and engineering prototype inspired by selected ideas from NASA's AEGIS science-targeting system, Perseverance AutoNav, and recent AI-assisted waypoint-planning demonstrations.

ARES is **not** NASA flight software and does not claim scientific or operational equivalence. Its purpose is to demonstrate an integrated, testable pipeline for simulated planetary exploration.

## Project goals

ARES aims to combine:
- Visual perception of a simulated environment.
- Terrain classification and traversability estimation.
- Obstacle-aware mapping and path planning.
- Ranking of visually interesting candidate science targets.
- A mission-planning agent that coordinates tools and proposes high-level actions.
- Independent deterministic safety validation before simulated actions execute.

## Engineering principles

1. Build a deterministic baseline before adding an LLM or agent framework.
2. Treat model outputs as uncertain estimates, not facts.
3. Never allow an LLM to bypass deterministic safety checks.
4. Record evidence for completion: code, tests, metrics, and reproducible experiments.
5. Keep this repository as the source of truth for project state.
6. Distinguish planned, implemented, tested, and validated capabilities.

## Repository layout

```text
ARES/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── PROJECT_CHARTER.md
│   ├── SYSTEM_ARCHITECTURE.md
│   ├── ROADMAP.md
│   ├── CURRENT_STATE.md
│   ├── DECISIONS.md
│   ├── LEARNING_LOG.md
│   ├── TASKS.md
│   └── INTERFACES.md
├── src/ares/
├── tests/
└── experiments/
```

## Initial development environment

Target Python: 3.11 or newer (verify compatibility of selected dependencies before pinning).

Create an environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

Install only the dependencies required for the first milestone. Do not install ROS 2, Gazebo, PyTorch, LangGraph, and every other candidate dependency at the start.

## Current status

The repository begins in the **planning / project setup** stage. No rover capability should be considered implemented until code and tests demonstrate it.

Read `docs/CURRENT_STATE.md` and `docs/TASKS.md` before starting work.

## How to work with an AI coding mentor

At the beginning of a new working session, ask the mentor to:
1. Read `CLAUDE.md`.
2. Read `docs/PROJECT_CHARTER.md`, `docs/CURRENT_STATE.md`, `docs/TASKS.md`, `docs/DECISIONS.md`, and relevant architecture/interface documents.
3. Summarize the verified state and identify the next task.
4. Ask before changing scope or architecture.

At the end of each session, update the relevant project documents and identify exact files changed, commands run, test results, and remaining risks.

## Status vocabulary

- **Planned:** specified but not implemented.
- **In progress:** implementation has started.
- **Implemented:** code exists, but may not be adequately tested.
- **Tested:** relevant tests have passed.
- **Validated:** behavior has been evaluated against defined acceptance criteria and recorded evidence.
- **Blocked:** progress depends on an unresolved issue.

Never upgrade a status without evidence.
