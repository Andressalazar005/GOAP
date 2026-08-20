# Hell Run GOAP

## Overview
Hell Run GOAP is a data-authored Goal-Oriented Action Planning framework for Unreal Engine 5. It includes the runtime pieces needed to sense world state, choose goals, build plans, execute action tasks, and re-plan as conditions change, plus dedicated editor tooling for authoring and inspecting GOAP domains. The repository also contains deterministic simulation support and runtime automation tests so planning behavior can be exercised outside normal combat play.

## Features
- `UGOAPBrainComponent` for agent-side planning and action execution.
- Data-authored `UGOAPDomain` definitions containing the planner's available goals/actions.
- `FGOAPPlanner` search implementation for producing action plans from world state.
- `UGOAPWorldStateSubsystem` for shared/global world-state data.
- `UGOAPPlanningSubsystem` for centralized planning support.
- Extensible `UGOAPSensor` and `UGOAPActionTask` base types.
- Simulation utilities for testing planner behavior without a full live encounter.
- Runtime automation tests covering planner/domain behavior.
- Dedicated GOAP domain asset type, factory, graph, and editor toolkit.
- Separate runtime/editor modules so graph tooling is excluded from packaged gameplay.

## Architecture
A GOAP agent owns a `GOAPBrainComponent`. Sensors update facts, the brain evaluates its domain and current state, and the planner searches for an action sequence that satisfies the selected goal. Action tasks then execute that plan. Shared facts can live in the world-state subsystem, while planning services and simulations are kept separate from individual agent logic.

The editor module provides a purpose-built domain editor rather than requiring all actions, goals, and relationships to be maintained as raw structs or code.

## Installation
1. Clone or copy this repository to `<Project>/Plugins/HellRunGOAP`.
2. Delete stale `Binaries` and `Intermediate` directories if it was compiled against another Unreal version.
3. Regenerate project files and compile your Editor target.
4. Launch Unreal Editor and verify **Hell Run GOAP** is enabled under **Edit > Plugins**.
5. Restart the editor if Unreal requests it.

```bash
git clone https://github.com/Andressalazar005/HellRunGOAP.git <Project>/Plugins/HellRunGOAP
```

## Basic setup
1. Create a GOAP Domain asset and define the goals/actions available to an AI archetype.
2. Implement or derive sensors that translate gameplay state into GOAP facts.
3. Implement action tasks that perform the actual gameplay work for planned actions.
4. Add a `GOAPBrainComponent` to the AI actor/controller architecture that should plan with the domain.
5. Assign the domain and feed the brain the state/context it needs.
6. Use the domain editor, simulator, and runtime tests to validate planning before relying on it in a full encounter.

## Key types
- `UGOAPBrainComponent` — agent-facing plan selection/execution owner.
- `UGOAPDomain` — authored goals/actions and planning domain data.
- `FGOAPPlanner` — plan search implementation.
- `UGOAPActionTask` — executable action base type.
- `UGOAPSensor` — world-state sensing base type.
- `UGOAPWorldStateSubsystem` — shared world facts.
- `UGOAPPlanningSubsystem` — centralized planner support.
- `FGOAPSimulation` — deterministic/synthetic planning simulation support.

## Status
The plugin is currently marked beta. It is intended as a reusable planning layer; project-specific combat movement, animation, targeting, and encounter direction should stay in actions/sensors or higher-level AI systems rather than inside the generic planner.

## Support
Use GitHub Issues for reproducible planner or editor problems. Include your Unreal Engine version, domain/goal/action setup, starting world state, expected plan, actual plan, and relevant logs.