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

## Phase 2 — Piece supply and assisted play

- [ ] Phase 2 — Piece supply and assisted play
    - [ ] Milestone 2.1 — Bag and Hold
        - [ ] T-008 — Implement shuffled bag supply
            Scope: src/game/supply.ts and tests/unit. Depends on: Phase 1 complete/closed and integrated; phase activation verified..
            Contract: R-SUPPLY in SPEC. Evidence: Two bags contain each shape once; seeded shuffle and boundary draws consume correctly.
        - [ ] T-009 — Implement Hold transitions
            Scope: src/game/engine.ts and tests/unit. Depends on: T-008.
            Contract: R-SUPPLY in SPEC. Evidence: First hold draws, later swap does not; second use rejects; blocked replacement loses; restart resets slot/eligibility.
        - [ ] T-010 — Expose Hold controls and slot
            Scope: src/ui/status.ts, src/app/input.ts, src/app/session.ts and tests/browser. Depends on: T-009.
            Contract: R-SUPPLY in SPEC. Evidence: C/action and empty/occupied slot reflect the engine; verify focus filtering and served-page hold behavior.
            Milestone exit: depend on all earlier tasks in this milestone (T-008, T-009); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/2/2.1.md.
    - [ ] Milestone 2.2 — Landing projection
        - [ ] T-011 — Implement pure landing projection
            Scope: src/game/landing.ts and tests/unit. Depends on: T-010.
            Contract: R-DROP in SPEC. Evidence: Irregular stacks, rotations and grounded pieces yield exact valid destination without side effects.
        - [ ] T-012 — Render and verify ghost-assisted play
            Scope: src/ui/board.ts, tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-011.
            Contract: R-DROP, R-QUALITY in SPEC. Evidence: Outline ghost agrees with engine projection and Hold changes; inspect both browsers and prepare v0.2.0 static build/release notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-011); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/2/2.2.md.
    - [ ] Milestone 2.3 — Phase review
        - [ ] T-013 — Review, test and report phase 2
            Depends on: milestone 2.1 completion/closure, milestone 2.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.2.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/2/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.

## Phase 3 — Rotation and drop timing

- [ ] Phase 3 — Rotation and drop timing
    - [ ] Milestone 3.1 — Rotation and grounded clock
        - [ ] T-014 — Implement horizontal kick search
            Scope: src/game/geometry.ts, src/game/engine.ts and tests/unit. Depends on: Phase 2 complete/closed and integrated; phase activation verified..
            Contract: R-DROP in SPEC. Evidence: Ordered candidate offsets, O stability, blocked rotations and all orientations behave deterministically.
        - [ ] T-015 — Implement grounded lock deadlines
            Scope: src/game/engine.ts, src/app/session.ts and tests/unit. Depends on: T-014.
            Contract: R-DROP, R-TIME in SPEC. Evidence: Grounded spawn, retained support, leaving/regaining support, soft down, suspension and equal-time event ordering preserve exact intervals.
            Milestone exit: depend on all earlier tasks in this milestone (T-014); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/3/3.1.md.
    - [ ] Milestone 3.2 — Hard-drop play
        - [ ] T-016 — Integrate delayed hard drop
            Scope: src/game/engine.ts, src/app/input.ts, src/ui/status.ts and tests/unit. Depends on: T-015.
            Contract: R-DROP in SPEC. Evidence: New grounding starts full interval; repeated/already-grounded hard drop preserves remaining time and never double locks.
        - [ ] T-017 — Verify assisted timing in the browser
            Scope: tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-016.
            Contract: R-DROP, R-QUALITY in SPEC. Evidence: Real Space/rotation/Hold sequences agree with ghost and timers on both browsers; prepare v0.3.0 build/notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-016); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/3/3.2.md.
    - [ ] Milestone 3.3 — Phase review
        - [ ] T-018 — Review, test and report phase 3
            Depends on: milestone 3.1 completion/closure, milestone 3.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.3.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/3/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.

## Phase 4 — Dynamic ghost visibility

- [ ] Phase 4 — Dynamic ghost visibility
    - [ ] Milestone 4.1 — Midline-aware ghost
        - [ ] T-019 — Implement projected-cell visibility policy
            Scope: src/game/ghost.ts and tests/unit. Depends on: Phase 3 complete/closed and integrated; phase activation verified..
            Contract: R-GHOST in SPEC. Evidence: Entirely upper/lower, straddling, row-10 boundary and duplicate projections yield specified visibility.
        - [ ] T-020 — Integrate and verify dynamic ghost rendering
            Scope: src/ui/board.ts, tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-019.
            Contract: R-GHOST, R-QUALITY in SPEC. Evidence: Movement/rotation/Hold/stack/restart update visibility and preserve destination; inspect both browsers and prepare v0.4.0 build/notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-019); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/4/4.1.md.
    - [ ] Milestone 4.2 — Phase review
        - [ ] T-021 — Review, test and report phase 4
            Depends on: milestone 4.1 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.4.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/4/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.

## Phase 5 — Penetrator play

- [ ] Phase 5 — Penetrator play
    - [ ] Milestone 5.1 — Deep landing and activation
        - [ ] T-022 — Implement deepest valid landing strategy
            Scope: src/game/landing.ts, src/game/geometry.ts and tests/unit. Depends on: Phase 4 complete/closed and integrated; phase activation verified..
            Contract: R-PENETRATOR in SPEC. Evidence: Layered gaps, floor, overlapping transit and stranded-candidate rejection preserve the settled board.
        - [ ] T-023 — Implement bonus and activation lifecycle
            Scope: src/game/engine.ts and tests/unit. Depends on: T-022.
            Contract: R-PENETRATOR in SPEC. Evidence: Zero/cap/award/debit/repeated activation/restart cases and active Hold rejection preserve supply and counts.
        - [ ] T-024 — Integrate penetrator movement and timing
            Scope: src/game/engine.ts, src/app/input.ts and tests/unit. Depends on: T-023.
            Contract: R-PENETRATOR, R-DROP in SPEC. Evidence: Gravity/rotation/soft/hard drop use the same terminal destination; activation retains/cancels grounding correctly and no invalid lock commits.
            Milestone exit: depend on all earlier tasks in this milestone (T-022, T-023); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/5/5.1.md.
    - [ ] Milestone 5.2 — Penetrator presentation and regression
        - [ ] T-025 — Render mode and bonus state
            Scope: src/ui/board.ts, src/ui/status.ts and tests/browser. Depends on: T-024.
            Contract: R-PENETRATOR, R-VIEW in SPEC. Evidence: Pure-white penetrator cells, nonwhite regular palette, accessible bonus count and activation/hold states agree with engine snapshots.
        - [ ] T-026 — Verify penetrator round integration
            Scope: tests/unit, tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-025.
            Contract: R-PENETRATOR, R-QUALITY in SPEC. Evidence: Earn-to-activation-to-safe-lock flows, ordinary/penetrator comparison and dynamic ghost pass on both browsers; prepare v0.5.0 build/notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-025); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/5/5.2.md.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-027 — Review, test and report phase 5
            Depends on: milestone 5.1 completion/closure, milestone 5.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.5.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/5/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.

## Phase 6 — Session configuration

- [ ] Phase 6 — Session configuration
    - [ ] Milestone 6.1 — Settings model and preview
        - [ ] T-028 — Implement settings state and spawn snapshots
            Scope: src/config/settings.ts, src/game/types.ts, src/game/engine.ts and tests/unit. Depends on: Phase 5 complete/closed and integrated; phase activation verified..
            Contract: R-SETTINGS in SPEC. Evidence: Defaults, rejected values, next-piece/Hold/restart mechanics and all lock-policy combinations match effective snapshots.
        - [ ] T-029 — Implement display policy and preview
            Scope: src/game/ghost.ts, src/game/supply.ts, src/ui/board.ts and tests/unit. Depends on: T-028.
            Contract: R-SETTINGS in SPEC. Evidence: hidden/dynamic/shown and next preview change display without consuming/reordering supply or affecting active state.
            Milestone exit: depend on all earlier tasks in this milestone (T-028); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/6/6.1.md.
    - [ ] Milestone 6.2 — Configuration controls and round integration
        - [ ] T-030 — Integrate accessible settings panel
            Scope: src/ui/settings.ts, src/ui/status.ts, src/app/session.ts and tests/browser. Depends on: T-029.
            Contract: R-SETTINGS in SPEC. Evidence: Each choice is reachable; controls do not move the board; pending indicators, retained Hold and penetrator prohibition remain clear.
        - [ ] T-031 — Verify session setting combinations
            Scope: tests/unit, tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-030.
            Contract: R-SETTINGS, R-QUALITY in SPEC. Evidence: Exercise lock-policy combinations, mid-piece change, Hold, restart, preview and reload-default behavior on both browsers; prepare v0.6.0 build/notes.
            Milestone exit: depend on all earlier tasks in this milestone (T-030); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/6/6.2.md.
    - [ ] Milestone 6.3 — Phase review
        - [ ] T-032 — Review, test and report phase 6
            Depends on: milestone 6.1 completion/closure, milestone 6.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.6.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/6/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.

## Phase 7 — Persistent configuration

- [ ] Phase 7 — Persistent configuration
    - [ ] Milestone 7.1 — Resolution and storage adapters
        - [ ] T-033 — Implement codecs and independent source resolution
            Scope: src/config/codec.ts, src/config/settings.ts and tests/unit. Depends on: Phase 6 complete/closed and integrated; phase activation verified..
            Contract: R-PERSIST in SPEC. Evidence: All six key/value mappings, duplicate/invalid/malformed/omitted inputs, explicit defaults and mixed-source cases match precedence.
        - [ ] T-034 — Implement cookie and URL adapters
            Scope: src/platform/cookies.ts, src/platform/url.ts and tests/unit. Depends on: T-033.
            Contract: R-PERSIST in SPEC. Evidence: Cookie flags/one-year expiry/readback and replaceState preserve unrelated keys/hash; blocked storage and history errors stay independent.
        - [ ] T-035 — Wire persistent startup and setting changes
            Scope: src/config/persistence.ts, src/main.ts, src/ui/status.ts and tests/browser. Depends on: T-034.
            Contract: R-PERSIST, R-SETTINGS in SPEC. Evidence: Resolve before first spawn, save valid explicit URL defaults, avoid omitted/invalid writes and keep selected settings usable with clear failure notices.
            Milestone exit: depend on all earlier tasks in this milestone (T-033, T-034); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/7/7.1.md.
    - [ ] Milestone 7.2 — Persistence round trips
        - [ ] T-036 — Verify persistent settings round trips
            Scope: tests/browser, README.md, package.json and RELEASE-NOTES.md. Depends on: T-035.
            Contract: R-PERSIST, R-QUALITY in SPEC. Evidence: Both browsers cover all settings, precedence, reload, hash/query preservation, no navigation, cookie-blocked/history failures and full gameplay regression; prepare v0.7.0 build/notes.
            Milestone exit: depend on all earlier tasks in this milestone (none); review all milestone code, execute focused/regression checks, repair blockers, and commit report plus HANDOFF with this task completion. Report: docs/dev/reports/phases/7/7.2.md.
    - [ ] Milestone 7.3 — Phase review
        - [ ] T-037 — Review, test and report phase 7
            Depends on: milestone 7.1 completion/closure, milestone 7.2 completion/closure.
            Scope: complete phase code review, contract/regression checks, blocker repairs, static build/version/v0.7.0 release-note readiness, phase report and HANDOFF. Verify one-task/commit publication evidence before phase integration; report pending integration/release effects accurately.
            Report: docs/dev/reports/phases/7/PHASE-REPORT.md. TODO: carry unresolved eligible noncritical findings with owner/options/provenance. If this phase completes the full intended task list, also include docs/dev/reports/IMPLEMENTATION-REPORT.md aggregating all milestone/phase TODOs, options and resolution provenance.
