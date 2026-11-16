# ARES Roadmap

**Status:** Proposed; acceptance thresholds need owner approval  
**Last updated:** 2026-11-16

Each phase must have a demonstrable deliverable. Do not start a later phase just because a library is available.

## Phase 0 — Research and project setup

Tasks:
- Read primary NASA/JPL descriptions of AEGIS, AutoNav, and AI-assisted waypoint planning.
- Separate verified public facts from project assumptions.
- Approve charter and architecture.
- Set up Python environment, package layout, linting, and tests.
- Define coordinate conventions and status workflow.

Exit criteria:
- Charter and architecture reviewed.
- Repository runs a minimal test.
- Research notes cite primary sources and clearly state limitations.

## Phase 1 — Deterministic 2D rover simulation

Tasks:
- Represent a grid world.
- Represent rover pose and legal moves.
- Add obstacles and a goal.
- Support reproducible scenario generation.

Exit criteria:
- Rover state updates correctly.
- Invalid moves are rejected.
- Scenarios are reproducible from a seed.
- Unit tests cover boundaries and collisions.

## Phase 2 — Mapping and baseline navigation

Tasks:
- Implement occupancy representation.
- Implement Dijkstra and A*.
- Compare route cost and runtime.
- Visualize path and obstacles.

Exit criteria:
- Planner finds valid paths on known test maps.
- Planner reports no-path cases.
- Path validity is independently checked.
- A* behavior is compared against Dijkstra on suitable cases.

## Phase 3 — Safety and dynamic replanning

Tasks:
- Implement route/action validator.
- Add unknown-cell and risk policy.
- Change map during traversal.
- Trigger replanning and safe stop.

Exit criteria:
- Unsafe paths are rejected with reason codes.
- Dynamic obstacle test demonstrates replanning or safe stop.
- Tests cover stale maps and out-of-bounds paths.

## Phase 4 — Computer vision perception

Tasks:
- Select a suitable, licensed dataset or create synthetic images.
- Build image loading and preprocessing.
- Establish a classical baseline.
- Evaluate object detection or segmentation approach.
- Convert image detections into map-relevant observations.

Exit criteria:
- Dataset and label definitions documented.
- Evaluation split avoids leakage.
- Metrics and failure examples are recorded.
- Coordinate conversion is tested.

## Phase 5 — Terrain and traversability

Tasks:
- Define initial terrain classes.
- Produce terrain labels or probabilities.
- Convert estimates to cost map.
- Handle uncertain/unknown regions conservatively.

Exit criteria:
- Cost-map rules are explicit and configurable.
- Planner uses terrain costs.
- Evaluation includes false-safe and false-unsafe cases.

## Phase 6 — Science target selection

Tasks:
- Detect or ingest candidate targets.
- Extract visual features.
- Define configurable ranking criteria.
- Include accessibility and uncertainty.

Exit criteria:
- Ranking is deterministic for fixed inputs/configuration.
- Score components are inspectable.
- Documentation does not claim mineralogical certainty from RGB imagery.

## Phase 7 — Mission orchestration and optional agent

Tasks:
- Define mission state and tool contracts.
- Implement deterministic controller.
- Add retries, conditional transitions, and approval points if needed.
- Evaluate whether LangGraph is justified.
- Add LLM/VLM proposal generation only after deterministic workflow works.

Exit criteria:
- Tool calls are typed and logged.
- Malformed LLM output is rejected.
- No LLM output bypasses safety validation.
- Deterministic fallback works when model is unavailable.

## Phase 8 — Integration and evaluation

Tasks:
- Run complete mission scenarios.
- Measure navigation, perception, target ranking, and agent performance.
- Add telemetry and mission reports.
- Document limitations and reproducibility.

Exit criteria:
- End-to-end demo works on documented scenarios.
- Metrics, configuration, and test commands are recorded.
- Known failure modes are documented.

## Phase 9 — Optional advanced robotics simulation

Only after the core system is stable:
- Evaluate ROS 2.
- Evaluate Gazebo or another 3D simulator.
- Add richer sensor models, localization, stereo/depth, and SLAM as scoped tasks.

Exit criteria:
- A written justification explains why the additional simulator/robotics middleware is needed.
- Existing module contracts remain testable.
