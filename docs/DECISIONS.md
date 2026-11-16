# ARES Architecture Decision Records

Record important technical choices here. Do not silently reverse an accepted decision. Use the format below for each new decision.

## Decision status

- **Proposed:** under discussion.
- **Accepted:** approved and currently governing implementation.
- **Superseded:** replaced by a later decision; retain the history.

## ADR-001 — Deterministic baseline before agent framework

**Status:** Accepted  
**Date:** 2026-11-16

### Context
Starting with an agent framework would combine several difficult problems before the core robotics pipeline is understood and testable.

### Decision
Implement core simulation, mapping, navigation, and safety as ordinary deterministic Python modules before introducing LangGraph or an LLM.

### Consequences
- Easier debugging and unit testing.
- Clearer module contracts.
- Agent integration is delayed until there is a real orchestration need.

## ADR-002 — LLM is advisory, not a safety authority

**Status:** Accepted  
**Date:** 2026-11-16

### Context
Generative models can produce invalid, inconsistent, or unsafe outputs.

### Decision
LLM/VLM outputs are proposals only. Deterministic code validates all plans/actions before simulated execution. The model cannot bypass the validator.

### Consequences
- Requires explicit schemas and validation.
- Requires safe fallback/rejection behavior.
- Agent quality is measured separately from safety correctness.

## ADR-003 — Start with a lightweight 2D simulation

**Status:** Proposed

### Context
A full 3D robotics simulator and ROS 2 introduce setup and conceptual overhead before core algorithms are working.

### Decision
Proposed: begin with a grid-world or lightweight 2D simulation. Select Pygame only if visualization adds value; keep simulation logic independent of rendering.

### Consequences
- Faster iteration.
- Easier reproducible tests.
- Does not initially model realistic rover dynamics, camera geometry, or 3D terrain.

## ADR template

### ADR-XXX — Short title
**Status:** Proposed / Accepted / Superseded  
**Date:** YYYY-MM-DD

#### Context
What problem or constraint led to this decision?

#### Options considered
What alternatives were evaluated?

#### Decision
What was selected and why?

#### Consequences
Trade-offs, risks, and follow-up work.

#### Evidence
Links, experiments, benchmarks, or documentation supporting the decision.
