# ARES Module Interfaces and Data Contracts

**Status:** Initial contracts proposed; not yet implemented  
**Last updated:** 2026-11-16

This document defines intended boundaries. Do not assume these functions exist until implemented in source code. Keep contracts small and typed. Update this file whenever an accepted interface changes.

## 1. Conventions

- Language: Python.
- Use type hints.
- Use explicit units and coordinate frames.
- Grid coordinates are proposed as `(row, col)` integer pairs.
- World coordinates and camera coordinates must not be mixed implicitly.
- Distinguish measured values, model estimates, and planner outputs.
- Functions should not mutate shared state unless documented.

## 2. Proposed domain types

Illustrative types; refine before implementation.

```python
from dataclasses import dataclass
from typing import Literal

@dataclass(frozen=True)
class GridCell:
    row: int
    col: int

@dataclass(frozen=True)
class RoverPose:
    cell: GridCell
    heading_rad: float

@dataclass(frozen=True)
class Detection:
    label: str
    confidence: float
    # Coordinate frame and geometry must be specified before use.
    source: Literal["camera", "synthetic", "manual"]

@dataclass(frozen=True)
class PlannedPath:
    cells: tuple[GridCell, ...]
    total_cost: float
    map_version: int
    planner: str

@dataclass(frozen=True)
class ValidationResult:
    accepted: bool
    reason_codes: tuple[str, ...]
```

## 3. Initial module contracts

### Simulation
Potential responsibilities:
- Create/load a world.
- Return sensor observations.
- Apply a validated movement step.
- Expose a monotonically increasing world/map version.

Candidate functions:
```python
def create_world(seed: int, width: int, height: int) -> "World": ...
def observe(world: "World", rover: RoverPose) -> "Observation": ...
def apply_validated_step(world: "World", rover: RoverPose, next_cell: GridCell) -> RoverPose: ...
```

### Perception
```python
def detect_objects(image: "ImageInput") -> list[Detection]: ...
def classify_terrain(image: "ImageInput") -> "TerrainEstimate": ...
```
Perception results must include confidence and a defined coordinate mapping before they can update a world map.

### Mapping
```python
def update_occupancy_map(
    current_map: "OccupancyGrid",
    observation: "Observation",
) -> "OccupancyGrid": ...

def build_cost_map(
    occupancy: "OccupancyGrid",
    terrain: "TerrainEstimate",
) -> "CostMap": ...
```

### Navigation
```python
def plan_path(
    cost_map: "CostMap",
    start: GridCell,
    goal: GridCell,
) -> PlannedPath | None: ...
```
A returned path is a proposal, not authorization to execute.

### Target ranking
```python
def rank_targets(
    candidates: list["ScienceCandidate"],
    policy: "TargetRankingPolicy",
) -> list["RankedTarget"]: ...
```
Ranking must expose score components and uncertainty. It must not label a visual estimate as confirmed composition.

### Safety
```python
def validate_path(
    path: PlannedPath,
    cost_map: "CostMap",
    rover_constraints: "RoverConstraints",
) -> ValidationResult: ...
```
Validation must independently check map version, bounds, traversability, collision, and configured risk constraints.

### Mission orchestration
```python
def propose_next_mission_action(state: "MissionState") -> "MissionAction": ...
```
If an LLM is used, its output must be parsed into a constrained schema and validated. It cannot directly execute movement.

## 4. Error handling

Use explicit domain exceptions or structured error results for:
- Invalid map dimensions.
- Out-of-bounds coordinates.
- No valid path.
- Stale map version.
- Invalid model output.
- Perception failure.
- Safety rejection.
- Simulator execution failure.

Do not silently convert failures into a successful-looking default.

## 5. Contract change checklist

When changing an interface:
- [ ] Update this document.
- [ ] Update type definitions and implementations.
- [ ] Update callers.
- [ ] Add or update tests.
- [ ] Record significant architectural changes in `DECISIONS.md`.
- [ ] Update `CURRENT_STATE.md` and `TASKS.md`.
