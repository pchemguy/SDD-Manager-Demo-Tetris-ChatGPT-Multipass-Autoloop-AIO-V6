# Delivery plan

## Delivery strategy and gates

Deliver useful capability increments on a working browser game. Each phase has its own included contracts and usable exit; the full intended scope is covered across the phases below. Review SPEC requirements and their acceptance routes alongside design. A phase's explicit included behavior is its acceptance boundary; later independent requirements do not broaden that earlier exit. Shared code may evolve in later phases while preserving relevant earlier behavior.

Implementation requires a separately authorized task range after whole-documentation QC and verified integration into main. Activate GitHub objects only for the eligible phase. Complete task evidence, publication, issue closure, milestone review/testing/report/HANDOFF and milestone closure in order. Every phase ends in its special one-task review milestone. A delivery milestone has a standalone review task only when it has at least four implementation tasks and its phase has at least two implementation milestones; otherwise its final implementation task owns the same whole-milestone obligations.

Use deterministic unit checks before served-page integration. Browser tasks must follow the root browser policy: pinned compatible isolated Chromium headless shell and managed Firefox, finite deadlines, independent diagnostics, official supported fallbacks and actual interaction/rendering evidence. Missing required evidence blocks the relevant implementation exit. A static build and truthful README/release notes travel with each capability.

Versions begin with v0.1.0 for playable classic delivery, increment minor versions for capability phases, and use patch versions for fixes. Reserve v1.0.0 for a separately agreed stabilized product. After each authorized implementation phase is complete, verified and integrated/published, create its release commit/tag on main and publish the corresponding GitHub release using finalized RELEASE-NOTES.md. Never claim the release before readback. Release handling follows the bundled SDD Manager release workflow rather than implying a side-branch tag is eligible.

Risks: timing races, projection disagreement, browser provisioning and stale input subscriptions. Keep one state writer, deterministic time/projection seams, early browser checks and repeatable teardown. Stop on required acceptance/publication failures; preserve evidence rather than weakening browser or gameplay requirements.

## Phase 1 — Playable classic game

Outcome: A playable fixed-speed classic game from start to loss and restart. Independent piece draws, blocked rotations without kicks, and failed-down locking define this delivery. Hold, ghost, bag, kicks, hard drop, penetrator and configuration are excluded.

Contracts: R-CORE, R-TIME, R-CLEAR, R-VIEW, R-QUALITY. Release target: v0.1.0. Dependency: None; eligible after accepted documentation integration.

### Milestone 1.1 — Falling-piece play

A visible playable piece moves, rotates, falls, locks and spawns until loss. Demonstrate controls and loss to judge basic playability. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 1.2 — Classic round completion

Row resolution, score and fresh restart form the complete classic loop; validate desktop usability, static packaging and both required browsers. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 1.3 — Phase review

After all delivery milestones complete and close, review the complete phase code and interactions, verify its included contracts and prior-phase regressions, repair blockers and retain the phase report. No later independent capability is required at this exit. Integrate the verified phase into main through an explicit two-parent merge, verify/publish the target, then publish the corresponding v0.1.0 tag and GitHub release with current release notes. No phase or release operation executes without the subsequently authorized implementation range.

## Phase 2 — Piece supply and assisted play

Outcome: A bag-fed game with Hold and a truthful always-visible ghost. Keep failed-down locking and blocked rotation behavior for this increment; kicks and delayed hard drop belong to rotation and drop timing.

Contracts: R-SUPPLY and ghost projection from R-DROP. Release target: v0.2.0. Dependency: Phase 1 complete, reviewed, closed and integrated/published; authorized implementation range includes this phase.

### Milestone 2.1 — Bag and Hold

Stable queue consumption and one-use Hold work through blocked spawn and restart; demonstrate supply/hold behavior. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 2.2 — Landing projection

Ghost matches the ordinary first-obstacle landing, without mutating supply or game time. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 2.3 — Phase review

After all delivery milestones complete and close, review the complete phase code and interactions, verify its included contracts and prior-phase regressions, repair blockers and retain the phase report. No later independent capability is required at this exit. Integrate the verified phase into main through an explicit two-parent merge, verify/publish the target, then publish the corresponding v0.2.0 tag and GitHub release with current release notes. No phase or release operation executes without the subsequently authorized implementation range.

## Phase 3 — Rotation and drop timing

Outcome: Horizontal kicks and hard drop operate under a full-interval grounded deadline. Preserve supply, Hold, score and loss. Dynamic ghost visibility is excluded.

Contracts: R-DROP. Release target: v0.3.0. Dependency: Phase 2 complete, reviewed, closed and integrated/published; authorized implementation range includes this phase.

### Milestone 3.1 — Rotation and grounded clock

Deterministic kicked rotation and support-sensitive lock timing integrate with existing movement. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 3.2 — Hard-drop play

Space lands at the ghost destination with the remaining full-interval delay; play remains usable in both browsers. Exit: integrate the milestone capability, review code and run applicable focused/regression checks; fix blockers, retain a milestone report and HANDOFF. Demonstrate the stated result for human continue/amend/simplify/stop judgment without inventing an additional authorization gate.

### Milestone 3.3 — Phase review

After all delivery milestones complete and close, review the complete phase code and interactions, verify its included contracts and prior-phase regressions, repair blockers and retain the phase report. No later independent capability is required at this exit. Integrate the verified phase into main through an explicit two-parent merge, verify/publish the target, then publish the corresponding v0.3.0 tag and GitHub release with current release notes. No phase or release operation executes without the subsequently authorized implementation range.
