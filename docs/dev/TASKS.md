# Implementation tasks

All product tasks are pending. Each task includes focused tests/documentation with its delivered result. SPEC owns behavior, PLAN owns phase/milestone exits, and layout owns placement. Implementation requires accepted integrated documentation, eligible hosted activation and a separately authorized range.

## Phase 1 — Playable classic game

- [ ] Phase 1 — Playable classic game
    - [ ] Milestone 1.1 — Falling-piece play
        - [ ] T-001 — Establish board geometry and deterministic rule harness
            Scope: src/game/geometry.ts, src/game/types.ts, tooling and tests/unit. Depends on: None; preparation integrated and phase activation verified..
            Contract: R-CORE in SPEC. Evidence: Shape masks, four rotations, bounds and occupied-cell rejection; validate locked build/test dependencies.
        - [ ] T-002 — Implement falling-piece lifecycle
            Scope: src/game/engine.ts, src/game/supply.ts, tests/unit. Depends on: T-001.
            Contract: R-CORE, R-TIME in SPEC. Evidence: Spawn, independent draws, movement, fixed gravity, failed-down lock and blocked-spawn loss through deterministic sequences.
        - [ ] T-003 — Integrate keyboard and rendered play
            Scope: src/app/session.ts, src/ui/board.ts, src/ui/status.ts, src/main.ts, index.html and styles. Depends on: T-002.
            Contract: R-TIME, R-VIEW in SPEC. Evidence: Real keyboard/focus and Canvas snapshots demonstrate falling, locking and loss; blur/hidden suspends until explicit resume.
            Milestone exit: depend on all earlier tasks in this milestone (T-001, T-002); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/1/1.1.md.
    - [ ] Milestone 1.2 — Classic round completion
        - [ ] T-004 — Resolve rows and scoring atomically
            Scope: src/game/board.ts, src/game/engine.ts and tests/unit. Depends on: T-003.
            Contract: R-CLEAR in SPEC. Evidence: 0–4 row fixtures prove simultaneous compaction, exact points and immutable pre-lock rejection.
        - [ ] T-005 — Complete restart and accessible game status
            Scope: src/game/engine.ts, src/app/session.ts, src/ui/status.ts and tests/browser. Depends on: T-004.
            Contract: R-TIME, R-VIEW in SPEC. Evidence: Restart resets board/score/supply; input filtering, focus, instructions, loss and resume remain coherent without duplicate listeners.
        - [ ] T-006 — Verify and package the classic game
            Scope: playwright.config.ts, tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-005.
            Contract: R-QUALITY in SPEC. Evidence: Provision isolated compatible browsers per policy, inspect real Canvas output and interactions on Chromium and Firefox, build self-contained assets and prepare v0.1.0 release notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-004, T-005); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/1/1.2.md.
    - [ ] Milestone 1.3 — Phase review
        - [ ] T-007 — Review, test and report phase 1
            Depends on: milestone 1.1 completion/closure, milestone 1.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.1.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/1/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.
