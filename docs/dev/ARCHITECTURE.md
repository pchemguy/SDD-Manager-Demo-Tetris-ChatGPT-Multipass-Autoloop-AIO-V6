# Architecture

## Arrangement

The [project brief](PROJECT.md) defines a local single-player browser game. Use TypeScript with a pure game model, a browser session controller, a Canvas board renderer and semantic HTML status/controls. Vite supplies development/build tooling, Vitest exercises deterministic rules, and Playwright exercises the served application in isolated Chromium headless shell and managed Firefox. Resolve compatible package versions and lock them during implementation; no runtime framework or server is needed.

| Block | Responsibility / ownership | Dependencies |
| --- | --- | --- |
| Rules | Board, piece geometry, legal transitions, line resolution, scoring and game lifecycle | Plain values and injected random source; no browser APIs |
| Session | Own the current model; serialize commands and elapsed game time; publish snapshots | Rules, monotonic clock and input adapter |
| Presentation | Draw snapshots; expose score, state and keyboard/control hints | Read-only snapshots and semantic commands |
| Browser boundary | Translate keyboard, focus and visibility; own animation frame and application teardown | Session and presentation |

Commands enter the single session owner. It applies one atomic transition, then publishes the resulting snapshot. Rendering never mutates the model. The animation loop advances a monotonic game clock and renders; hidden/unfocused sessions suspend elapsed game time and require deliberate resumption. Restart replaces game state without duplicating listeners or animation loops.

## State and dependency rules

Use plain typed records and functions rather than a service framework or inheritance hierarchy. Game transitions receive explicit elapsed time and random draws; tests can replay inputs without wall clocks or DOM. The board owns settled cells, the active piece owns its pose, and line resolution owns score changes. A locked piece is committed once, complete lines are removed atomically, then the next piece is spawned or game over is declared. View code consumes state through a stable snapshot boundary.

Canvas is suitable for a small regular grid; DOM status and controls provide readable text, focus behavior and accessible labels. This trades a single rendering surface for explicit state and screenshot checks. DOM-per-cell rendering and a UI framework add reconciliation machinery without a required product benefit. Keep static assets self-contained; no CDN, backend, account or external gameplay service.

## Invariants and failures

Settled cells are always in bounds and non-overlapping. Only a successful legal lock mutates settled cells. Rejected commands leave game state unchanged. The session is the sole writer; input handlers never race timers. Dispose cancels owned callbacks/listeners. Missing Canvas support produces a visible unsupported-renderer message rather than an invisible game. Browser provisioning failures block affected acceptance; they do not justify silently dropping Firefox or using personal browsers.

## Verification seams

Rules accept deterministic random and clock inputs. Session checks use synthetic time and complete snapshots; browser checks use the real page, keyboard/focus/visibility handling and inspected Canvas output. Test fixtures may construct model states through exported typed engine functions; production code contains no test-only global mutation hook. Browser-independent checks do not establish browser compatibility.

## Piece services and projections

Piece supply owns a seeded-testable 7-bag queue; hold owns its slot and cycle eligibility. The engine exposes a pure landing projection for the active pose. The renderer draws a ghost from that result and never performs its own collision search. Rotation search uses documented horizontal kick candidates; lock timing remains a game-clock concern in the engine, driven by Session. This keeps keyboard and gravity behavior consistent. Hold produces a fresh active piece through the same spawn path and resets that piece's local timing.

## Ghost presentation policy

A pure visibility predicate consumes the landing projection and board geometry. It classifies the topmost occupied projected cell against the midline. The policy never changes the active piece, collision handling, supply or clock. Presentation recomputes it from each published snapshot so it cannot lag a changed landing.

## Penetrator landing strategy

The landing service selects an ordinary first-obstacle destination or a penetrator deepest valid destination. The engine owns activation eligibility, bonus debit/award, and mode lifetime; all movement, gravity, ghost and hard drop use this same strategy. Transient overlap is represented only by the active piece, never by overwriting settled cells. Candidate moves require a legal destination at or below them; a grounded penetrator is at its terminal destination. This prevents a piece from passing below every legal locking position.

## Configuration boundary

A typed settings owner stores selected values. Presentation reads display settings immediately; spawn snapshots mechanical settings into the active-piece state. The settings panel dispatches typed changes rather than touching the board. Pending changes are visible beside controls; restarting adopts the selected settings. The settings owner is page-session memory and has no persistence side effects.

## Browser persistence adapters

Settings codecs are pure allowlist parsers. A persistence adapter reads URL query and cookies at startup, resolves each key separately, and writes valid explicit URL values into cookies. A selected-value change attempts cookie storage and URL replacement independently after updating session state. Browser APIs stay outside Rules; persistence cannot mutate active-piece mechanics or block gameplay. URL changes preserve unrelated parameters/hash and use history replacement without navigation. Failed storage/history operations expose a concise notice while retaining selected session values.
