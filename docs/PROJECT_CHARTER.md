# ARES Project Charter

**Project:** ARES — Autonomous Robotic Exploration System  
**Status:** Draft charter; baseline scope awaiting user approval  
**Owner:** Project developer  
**Last updated:** 2026-11-16

## 1. Vision

Build a modular, testable simulation of an autonomous planetary exploration rover. ARES will perceive a simulated environment, estimate terrain traversability, map obstacles, plan routes, rank candidate science targets, and coordinate a mission using an AI-assisted planning layer.

ARES is inspired by selected publicly described ideas from NASA's AEGIS, Perseverance AutoNav, and AI-assisted waypoint-planning research. It is an independent educational prototype—not NASA software and not a reproduction of operational flight systems.

## 2. Problem statement

A simulated rover must move toward mission goals while handling uncertain visual observations, obstacles, terrain risk, and competing science opportunities. The project explores how perception, mapping, planning, and high-level reasoning can work together under explicit safety constraints.

## 3. Objectives

1. Create a reproducible simulated environment and rover.
2. Build a perception pipeline for environmental imagery.
3. Represent obstacles and terrain in a map.
4. Estimate traversability using transparent, testable rules or models.
5. Plan routes using classical algorithms before considering learned planners.
6. Detect and rank candidate visual science targets without overstating geological certainty.
7. Add an AI mission-planning layer that coordinates tools and proposes high-level plans.
8. Validate proposed plans with deterministic constraints before simulated execution.
9. Measure system behavior with defined metrics and reproducible experiments.
10. Document engineering decisions, limitations, and learning.

## 4. Non-goals

- Reproducing NASA flight software or claiming equivalence to AEGIS/AutoNav.
- Controlling a real rover or physical robot in the initial project.
- Inferring mineral composition or scientific truth from RGB images alone.
- Allowing an LLM to issue direct motor commands or override safety checks.
- Building a multi-agent architecture merely for novelty.
- Using every technology listed in the initial brainstorm.
- Claiming autonomy based solely on an LLM generating text or JSON.

## 5. Guiding principles

- **Evidence over claims:** status requires code, tests, metrics, or documented evidence.
- **Deterministic first:** establish reliable conventional algorithms before adding generative components.
- **Safety separation:** mission suggestions and action validation are separate responsibilities.
- **Modularity:** stable interfaces between perception, mapping, planning, targeting, and orchestration.
- **Reproducibility:** record seeds, datasets, configurations, versions, and commands for experiments.
- **Learning:** the developer must understand core algorithms and implementation decisions.
- **Scope discipline:** defer advanced capabilities until their prerequisites work.

## 6. Proposed high-level capabilities

- Environment simulation.
- Camera/image input.
- Obstacle detection.
- Terrain classification.
- Occupancy/cost map generation.
- Traversability estimation.
- A*/Dijkstra route planning.
- Dynamic replanning.
- Candidate target detection and ranking.
- Mission state and tool orchestration.
- Optional LLM/VLM planning assistance.
- Deterministic plan validation.
- Mission telemetry and reporting.

These are proposed capabilities, not claims of current implementation.

## 7. Success criteria

ARES is successful when a reproducible demonstration can:
1. Load or generate a known environment.
2. Observe or receive a representation of that environment.
3. identify obstacles and produce a map/cost representation.
4. Plan a route to a goal.
5. Reject a route that violates defined safety constraints.
6. Replan after an obstacle or map change.
7. Rank candidate targets using documented criteria.
8. Produce a mission summary that distinguishes observations, estimates, and uncertainty.
9. Run automated tests and report meaningful metrics.

Numerical thresholds must be agreed and recorded before claiming validation.

## 8. Safety policy

All LLM/VLM outputs are untrusted proposals. Validate schema, bounds, map consistency, collision risk, rover constraints, and mission policy in deterministic code. Invalid or uncertain plans must be rejected or escalated for human review. The simulator must have a safe stop/fallback behavior.

## 9. Status definitions

- **Planned:** documented, not started.
- **In progress:** work has begun.
- **Implemented:** code exists.
- **Tested:** specified tests pass.
- **Validated:** acceptance criteria have been evaluated with recorded evidence.
- **Blocked:** cannot proceed until a dependency or decision is resolved.

## 10. Change control

Changes to project scope, safety policy, core architecture, or accepted technical decisions must be discussed and recorded in `DECISIONS.md`. Update affected interfaces, roadmap, and tests. Never silently replace a decision.
