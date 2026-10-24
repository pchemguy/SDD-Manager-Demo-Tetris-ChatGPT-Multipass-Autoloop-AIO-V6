# Component decomposition

## Component ownership

Components refine [ARCHITECTURE](ARCHITECTURE.md); exact behavior belongs to SPEC. Names identify logical responsibilities, not mandatory classes.

| Component | Provides / owns | Requires / excludes | Verification seam |
| --- | --- | --- | --- |
| Geometry | Shape cells, clockwise/counterclockwise transforms, bounds/collision queries | Read-only board and pose; no timers or scoring | Small coordinate fixtures |
| Supply | Next shape draw | Injected uniform random source; no rendering | Fixed draws |
| Board resolution | Commit legal cells, simultaneous full-row removal, compacted board and clear count | Geometry validation; no input or score UI | Board before/after fixtures |
| Game engine | Active pose, score, status, spawn/lock/restart transitions | Geometry, Supply and Board resolution | Commands + elapsed time → state |
| Session controller | Current engine state, elapsed game time, command ordering and subscriptions | Injected clock; no shape rules | Fake clock and command sequences |
| Input adapter | Keyboard/button → semantic commands; focus filtering and repeat policy | Session command entry | Event boundary checks |
| Board renderer | Canvas grid, active/settled piece rendering | Read-only snapshot; no state mutation | Pixel/screenshot inspection |
| Status view | Score, game-over/restart/resume controls and instructions | Snapshot + command callback | DOM and keyboard/focus checks |
| Application entry | Create/wire/dispose one session, renderer and event lifecycle | Browser environment | Repeated startup/restart/teardown |

## Collaboration and lifecycle

Input and clock events enter Session in order. Engine validates a candidate pose, advances gravity, commits a lock when due, clears rows, awards score and requests a spawn. Presentation receives only complete post-transition snapshots. Restart replaces the game model and resets its random supply; it retains a single owned event/animation lifecycle. Time suspension clears pressed-key state and preserves the remaining gravity duration. Resume uses a fresh monotonic timestamp, preventing a hidden-page catch-up burst.

Invalid commands are ordinary no-op results. Unsupported rendering is handled at Application entry; programming invariant violations are surfaced rather than committing corrupt cells. Tests may call engine constructors and transitions directly, keeping fixture construction out of production UI globals. No dependency points from Rules into browser/session presentation.

## Assisted-play components

Supply maintains the shuffled queue and draw cursor; consuming a piece is explicit. Hold stores a shape identity, not a pose, and one-use eligibility. Engine owns spawn on hold and loss on blocked replacement. Projection takes board, active shape/rotation/column and landing strategy and returns a destination without consuming supply or changing time. Rotation chooses the first legal kicked pose; Grounding tracks grounded-start/deadline through motion and clock advances. Renderer and Status view consume ghost/hold information but cannot debit draws or reset timers.

## Visibility component

Ghost visibility accepts projected occupied cells and visible board height, returning a Boolean. Renderer owns its application on every redraw; Engine and Projection remain independent of whether a ghost is drawn. Tests cover positions entirely above, straddling and exactly at the midline.
