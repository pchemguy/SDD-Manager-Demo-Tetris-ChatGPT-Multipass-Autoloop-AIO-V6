# Repository layout

## Ownership and status

The paths below allocate the intended implementation. Existing root policies and the bundled plugin are preserved. Listed product source/tests/build configuration are planned locations, not claims that implementation exists. [DECOMPOSITION](DECOMPOSITION.md) defines logical owners and [PLAN](PLAN.md) defines delivery order.

| Owner | Intended source | Checks / artifacts |
| --- | --- | --- |
| Geometry and state types | src/game/geometry.ts, src/game/types.ts | tests/unit/geometry.test.ts |
| Piece supply | src/game/supply.ts | tests/unit/supply.test.ts |
| Board resolution | src/game/board.ts | tests/unit/board.test.ts |
| Game engine | src/game/engine.ts | tests/unit/engine.test.ts |
| Session and input | src/app/session.ts, src/app/input.ts | tests/unit/session.test.ts, tests/browser/input.spec.ts |
| Board and status views | src/ui/board.ts, src/ui/status.ts, src/styles.css | tests/browser/game.spec.ts and owned screenshot artifacts |
| Application composition | src/main.ts, index.html | Served-page integration |
| Tooling/static package | package.json, package-lock.json, tsconfig.json, vite.config.ts, playwright.config.ts | dist/ generated; README.md and RELEASE-NOTES.md describe actual delivered state |

## Placement rules

Rules import no DOM, cookie or URL APIs. Browser adapters depend inward on typed model contracts. Unit fixtures live under tests/fixtures and use public typed engine boundaries; browser checks exercise the actual served page. Keep generated dist/, browser binaries, profiles, caches and test output untracked and outside production assets. Assign one absolute project-owned PLAYWRIGHT_BROWSERS_PATH consistently for install and execution; never attach personal sessions or use unowned browser installations. Do not modify /pyenv.

Development roots and adjacent scoped QC reports live in docs/dev/. Implementation reports use docs/dev/reports/phases/<phase-id>/<milestone-id>.md and PHASE-REPORT.md; final implementation report uses docs/dev/reports/IMPLEMENTATION-REPORT.md. Report paths are future outputs, not links to missing files. docs/ai-logs contains manual provenance and is excluded from routine source/QC loading. Existing policies and .agents/plugins/sdd-manager remain governing/supporting assets, not product runtime code.

## Assisted-play placement

Landing projection belongs to src/game/landing.ts with tests/unit/landing.test.ts. Hold and grounded timing remain engine state, supply remains in its own module, and Hold controls/slot remain Status view and Input adapter responsibilities. No separate framework or duplicate collision implementation is introduced.

## Ghost policy placement

src/game/ghost.ts owns the pure visibility predicate; tests/unit/ghost.test.ts owns boundary fixtures. Board renderer consumes its result. The path represents one focused rule, not a second landing calculation.

## Penetrator placement

Deep landing stays in src/game/landing.ts; activation/bonuses/timing stay in src/game/engine.ts and shared state types. Board renderer and Status view own white cells/bonus symbols. Extend existing unit/browser suites with layered-stack fixtures under tests/fixtures; do not create a duplicate game engine.
