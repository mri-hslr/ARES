# ARES Task Board

**Last updated:** 2026-11-16

## Status definitions

- **Backlog:** not started.
- **Ready:** requirements and acceptance criteria are clear.
- **In progress:** currently being worked on.
- **Review:** implementation awaits review/tests.
- **Done:** acceptance criteria met with evidence.
- **Blocked:** dependency or decision prevents progress.

## Current priority

### ARES-001 — Review and approve project charter
**Status:** Ready  
**Phase:** 0  
**Acceptance criteria:**
- [ ] Read `PROJECT_CHARTER.md`.
- [ ] Confirm goals and non-goals.
- [ ] Confirm safety policy.
- [ ] Record changes and approval.

### ARES-002 — Research NASA/JPL inspiration accurately
**Status:** Ready  
**Phase:** 0  
**Acceptance criteria:**
- [ ] Find primary NASA/JPL sources for AEGIS.
- [ ] Find primary NASA/JPL sources for Perseverance AutoNav.
- [ ] Find primary source for AI-assisted waypoint planning demonstration.
- [ ] Summarize what each system does and does not establish.
- [ ] Separate source-backed facts from ARES design choices.

### ARES-003 — Select initial 2D simulator approach
**Status:** Backlog  
**Phase:** 0  
**Acceptance criteria:**
- [ ] Compare custom grid simulation and lightweight visualization options.
- [ ] Decide whether rendering is needed in the first milestone.
- [ ] Record decision in `DECISIONS.md`.

### ARES-004 — Bootstrap Python package and test runner
**Status:** Backlog  
**Phase:** 0  
**Acceptance criteria:**
- [ ] Create package structure.
- [ ] Configure test runner.
- [ ] Add one minimal passing test.
- [ ] Document exact setup and test commands.

## Backlog by phase

### Phase 1 — Simulation
- [ ] Define world/grid data model.
- [ ] Define rover pose and movement rules.
- [ ] Implement deterministic scenario generation.
- [ ] Add boundary and collision tests.

### Phase 2 — Mapping and navigation
- [ ] Implement occupancy grid.
- [ ] Implement Dijkstra.
- [ ] Implement A*.
- [ ] Validate paths independently.
- [ ] Record planner comparisons.

### Phase 3 — Safety and replanning
- [ ] Implement safety validator and reason codes.
- [ ] Add dynamic obstacle scenario.
- [ ] Add safe-stop fallback.
- [ ] Test stale-map and invalid-path rejection.

### Phase 4 — Perception
- [ ] Select dataset and document license.
- [ ] Define labels and evaluation split.
- [ ] Implement image input pipeline.
- [ ] Establish baseline and evaluation metrics.

### Phase 5 — Traversability
- [ ] Define terrain classes.
- [ ] Define terrain-to-cost mapping.
- [ ] Handle uncertainty and unknown regions.
- [ ] Test planner integration.

### Phase 6 — Target ranking
- [ ] Define candidate target representation.
- [ ] Define transparent ranking criteria.
- [ ] Implement ranking and tests.
- [ ] Document scientific limitations.

### Phase 7 — Mission orchestration
- [ ] Define mission state.
- [ ] Define tool contracts.
- [ ] Implement deterministic orchestration.
- [ ] Evaluate need for LangGraph.
- [ ] Add constrained LLM proposal interface only if justified.

### Phase 8 — Integration and evaluation
- [ ] Create end-to-end scenarios.
- [ ] Add metrics and telemetry.
- [ ] Run regression tests.
- [ ] Document results and failure cases.

## Task hygiene

Every active task must have:
- A clear problem statement.
- A bounded scope.
- Acceptance criteria.
- Relevant interfaces/files.
- Tests or evidence required.
- A known status and owner.

Do not mark a task Done because code was generated. Mark it Done only after acceptance criteria are satisfied.
