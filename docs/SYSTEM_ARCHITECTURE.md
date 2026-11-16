# ARES System Architecture

**Status:** Proposed baseline architecture  
**Last updated:** 2026-11-16

## 1. Architectural strategy

Build a deterministic modular application first. Start with a lightweight 2D simulator and classical planning. Add camera-based perception and learned models after the simulation and interfaces are stable. Add an LLM/agent layer last.

Do not begin with ROS 2, Gazebo, multi-agent orchestration, or a complex 3D digital twin unless a milestone demonstrates the need.

## 2. Logical data flow

```text
Mission Objective
       |
       v
Mission Controller / State
       |
       +------------------------------+
       |                              |
       v                              v
Environment Simulator            Mission Policy
       |
       v
Sensor / Camera Observation
       |
       v
Perception
  - obstacle detection
  - terrain classification
  - candidate target detection
       |
       v
World Model / Map
  - occupancy grid
  - terrain labels
  - traversability / cost map
       |
       +-------------------------+
       |                         |
       v                         v
Navigation Planner         Science Target Ranker
  - A* / Dijkstra             - candidate features
  - replanning                - priority score
       |                         |
       +------------+------------+
                    |
                    v
          Proposed Mission Plan
                    |
                    v
          Deterministic Validator
          - schema / bounds
          - map consistency
          - collision / risk
          - rover constraints
                    |
             +------+------+
             |             |
           Reject        Accept
             |             |
       Safe fallback       v
                    Simulated Executor
                           |
                           v
                    Telemetry / Logs
                           |
                           v
                    Mission Report
```

An optional LLM/VLM may assist with high-level interpretation or mission-plan proposals. It does not replace perception, path planning, or safety validation.

## 3. Module responsibilities

### 3.1 Simulator
Owns the world state, rover pose, obstacles, terrain, and simulated movement. Provides repeatable scenarios and observations.

### 3.2 Perception
Converts sensor observations into structured detections and estimates. Must expose confidence and coordinate/frame conventions. Initial implementation may use synthetic map data before real image inference.

### 3.3 World model
Maintains the map and combines occupancy, terrain labels, and traversability costs. Defines coordinate systems and map resolution.

### 3.4 Traversability estimator
Computes a cost/risk representation from terrain and obstacle information. Unknown areas must not automatically be treated as safe.

### 3.5 Navigation planner
Consumes start, goal, and a cost/occupancy map. Produces a candidate path and planning metadata. Initial baseline: A* on a grid; compare with Dijkstra.

### 3.6 Science target ranker
Ranks visual candidate targets using explicit features and configurable weights. Scores indicate prioritization, not verified scientific value or composition.

### 3.7 Mission controller / agent
Tracks mission state and invokes tools in a controlled workflow. Start as ordinary Python orchestration. Introduce LangGraph only when branching, state persistence, retries, or human approval create a concrete need.

### 3.8 Deterministic safety validator
Checks every proposed route/action independently. Rejects malformed, out-of-bounds, colliding, over-risk, stale-map, or otherwise prohibited actions. Provides a reason code.

### 3.9 Telemetry and reporting
Records observations, decisions, paths, validator outcomes, model versions, timing, and mission results.

## 4. Proposed repository package layout

```text
src/ares/
  __init__.py
  config.py
  domain/
    models.py
    enums.py
  simulation/
    world.py
    rover.py
    sensors.py
  perception/
    interface.py
    classical.py
  mapping/
    occupancy.py
    costmap.py
  navigation/
    astar.py
    planner.py
  targeting/
    features.py
    ranking.py
  mission/
    state.py
    controller.py
  safety/
    validator.py
  telemetry/
    logger.py
```

This is a proposed future layout. Create modules only when the relevant milestone begins.

## 5. Key design constraints

- Define coordinate frames and units explicitly.
- Keep perception output separate from world-map representation.
- Keep planner output separate from execution commands.
- Every route must carry enough metadata to validate it against the map version used.
- Record confidence/uncertainty where estimates are involved.
- Ensure reproducible simulation seeds.
- Use typed data structures at module boundaries.
- Keep LLM outputs schema-constrained and independently validated.

## 6. Initial implementation sequence

1. Domain types and a deterministic grid world.
2. Rover pose and movement model.
3. Occupancy grid and A*.
4. Safety validation and tests.
5. Dynamic obstacle update and replanning.
6. Synthetic perception interface.
7. Image-based perception.
8. Terrain costs and target ranking.
9. Mission orchestration.
10. Optional LLM/VLM integration.
11. Optional ROS 2 / Gazebo migration.

## 7. Open architecture questions

- Which 2D simulator: custom grid/Pygame or another tool?
- What is the initial grid coordinate convention and cell size?
- Which camera/image dataset will be used, and what license applies?
- What terrain classes are in the first classifier?
- What rover motion model is sufficient for the first milestone?
- Which model/provider, if any, will be used for vision-language reasoning?
- At what point would ROS 2 provide enough value to justify its complexity?
