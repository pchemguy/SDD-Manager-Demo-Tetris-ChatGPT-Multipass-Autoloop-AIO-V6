# System specification

## Context and ownership

This static single-player keyboard game follows [PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md). Engine owns rules and state; Session owns ordered events and game time; Presentation owns display and browser adapters own external effects. Requirements below describe intended behavior, not verified implementation.

## R-CORE — Board, pieces and transitions

The visible board has 10 columns (x=0–9) and 20 rows (y=0–19), increasing downward. Settled cells are empty or carry a shape/color identity. Active cells are separate until lock. A regular piece is valid only when every occupied cell is inside the board and does not overlap settled cells. Reject invalid lateral or rotation candidates without changing pose or consuming supply. A failed downward attempt locks under the failed-down policy. Lock revalidates the final cells, writes them exactly once, clears rows, scores, then spawns; reject corruption before any partial write. Spawn failure ends play without overwriting the stack.

Spawn orientations use these square masks (slash separates rows): I `..../IIII/..../....`; O `OO/OO`; T `.T./TTT/...`; J `J../JJJ/...`; L `..L/LLL/...`; S `.SS/SS./...`; Z `ZZ./.ZZ/...`. The square size is n. Spawn anchor is (floor((10−n)/2),0). A clockwise rotation maps each local cell (x,y) to (n−1−y,x); counterclockwise is its inverse. O remains unchanged. Four clockwise rotations restore the same cells. Rotation without kicks accepts only the rotated pose at the current anchor. No occupied cell may escape the top boundary during regular play; an invalid lock/top overflow is a loss without committing invalid cells.

Supply uses the bag contract in R-SUPPLY; injected draws are in [0,1). A new game clears all settled cells, sets score to 0, resets supply and spawns one piece. The random source is injectable for deterministic rules tests; seeded replay is a test capability, not a required player feature.

## R-TIME — Input and game lifecycle

The game starts in ready state with Start. Running accepts movement; suspended, ready and game-over states reject movement. Left/Right move one column, Down attempts one row, Up rotates clockwise, Z rotates counterclockwise, Enter starts/restarts or resumes, and buttons provide labeled Start/Restart/Resume actions. Use keydown events: repeated lateral/down events are accepted one command each, rotation/start commands ignore event.repeat. Prevent page scrolling only for handled gameplay keys while the board game region owns focus. Events originating from buttons, links or editable/select controls do not produce gameplay commands; button activation retains native behavior. The game region has a visible keyboard focus indicator.

Gravity attempts one downward step every 1000ms of game time. Successful manual soft descent restarts the gravity interval; failed lateral/rotation input does not. Process an elapsed-time update chronologically across gravity and lock events; equal timestamps resolve an existing piece's lock before another descent/spawn event, with each piece locked at most once. The session must not advance game time while the page is hidden or its window is unfocused. Clear held-key state; resume only through explicit Resume/Enter from the game region, preserving remaining timers. Restart clears board/score, returns to running, and replaces piece state without registering duplicate event handlers or animation loops. Game over freezes game time until restart.

## R-CLEAR — Line resolution and score

After lock, find all full rows simultaneously, remove them, shift remaining rows down without changing their order, and insert empty rows at the top. Award 100/300/500/800 points for 1/2/3/4 rows in that lock, respectively; 0 for none. Do not award points for moves or soft drops. Score never carries across restart. Gravity remains fixed; no speed levels are required.

## R-VIEW — Presentation and accessibility

Show board, active/settled piece cells, score, game state and control hints. Colors for the seven regular shapes are distinguishable and never pure white. Keep settled occupied cells visually separable from empty cells by cell outlines and contrast. Draw the active state and all status fields from one complete snapshot, within the next animation frame after an accepted command. Display game over and a usable restart action. Canvas has a programmatic board description; score/state updates are semantic DOM text, with a polite live status for loss/suspension and labels for controls. A missing 2D Canvas context shows an explanatory message and disables Start. Layout must fit a normal desktop viewport without clipping controls; mobile touch interaction is excluded.

## R-QUALITY — Delivery and verification

Production output is a static asset directory with locally bundled runtime assets. No network service, personal browser session or CDN is needed for gameplay. Build/dependency tooling may require network provisioning; compatibility is determined by the locked toolchain during implementation. Test deterministic geometry, lock/spawn, row clearing, scoring, restart and time suspension, then serve the actual application and exercise real keyboard/focus, visible Canvas and status behavior in isolated Chromium headless shell and managed Firefox under BROWSER_DEV_POLICY.md. Required failure on either browser blocks its acceptance claim; diagnose supported fallbacks rather than dropping coverage.

## Acceptance routes

| Route | Objective outcomes |
| --- | --- |
| A-CORE | Start, move, rotate and fall to a legal lock; wall/stack rejection leaves pose unchanged; blocked spawn reaches game over without stack overwrite. |
| A-CLEAR | Fixtures for 0–4 simultaneous rows produce exact compacted boards and stated score; restart produces empty board/zero score/fresh active piece. |
| A-TIME | Boundary-time and repeated-input checks preserve event order; hidden/blur suspends without catch-up; explicit resume/restart does not duplicate input or loops. |
| A-VIEW | Real served page accepts controls, isolates focused controls, renders recognizable occupied/empty/active cells, shows score/loss/restart and builds self-contained assets in both required browsers. |

## R-SUPPLY — Bag and Hold

Use a Fisher–Yates shuffle of I,O,T,J,L,S,Z with injectable draws, consuming exactly one of each before the next shuffled bag. Hold (C or labeled action) is permitted once between locks; first Hold stores the outgoing shape and consumes one supply shape, subsequent cycles swap without a draw. Stored shape has no position, rotation, timer or penetrator state. Incoming shape uses canonical spawn orientation/anchor and a fresh piece clock; a blocked incoming spawn loses immediately. A second Hold before lock is a no-op. Restart empties Hold and resets its eligibility and supply. Hold affects only shape identity, never score or settled cells.

## R-DROP — Ghost, kicks and grounded timing

Ordinary landing is the last legal pose reached by descending one row at a time before the first collision/floor. Ghost uses exactly this destination without mutating model, timer, hold or supply, subject to the visibility policy; render a hollow outline distinct from the active piece and settled cells. If destination equals active pose, omit duplicate ghost drawing. Hold slot is visible with an empty state.

For clockwise or counterclockwise rotation, try horizontal anchor offsets [0,−1,+1,−2,+2] in that order at unchanged y. Accept the first fully legal candidate; reject if none. O remains unchanged and does not shift. These are horizontal wall kicks, not a claim of Guideline SRS; no upward or vertical kicks are required.

Space invokes hard drop to the same destination as ghost and awards no drop points. Ignore repeated keydown for Hold and hard drop. The default lock policy is full-interval: begin a 1000ms deadline at first grounding, including immediate spawn on support. Lateral/rotation movement retaining support keeps the existing deadline. Leaving support cancels it; later grounding starts a new full interval. A successful soft descent resets the gravity interval and recomputes support. Failed down/hard-drop repetitions do not reset grounding. Hard drop reaching ground begins a deadline only when no valid grounded deadline exists; hard drop on an already grounded piece keeps the remaining time. Lock at deadline even without another down attempt. Fail-down policy, when selected for an increment requiring it, locks on a failed down attempt; reaching a destination by hard drop alone is not a failed attempt. Time suspension preserves all remaining durations.

Acceptance A-ASSIST: two complete bag draws contain seven unique shapes each; Hold draw/swap/block/repeat semantics are exact; ghost and hard-drop landing agree on irregular stacks; edge rotations select the first legal kick or no-op; full-interval lock survives repeated input and cancels/restarts only on actual loss/regain of support. Test exact deadlines and a spawn that is already grounded.

## R-GHOST — Conditional visibility

Dynamic mode shows a non-duplicate ghost only when the minimum y of all projected occupied cells is at least 10. Any projected cell at y<10 hides the whole ghost, including a piece straddling rows 9 and 10. A topmost cell exactly on row 10 is visible. Recompute after movement, rotation, Hold, gravity, stack changes and restart; visibility never changes destination, timers or legality.

Acceptance A-GHOST: fixture landings entirely above, straddling, exactly on and below the midline produce the specified full-ghost visibility after each state transition; the active piece remains visible regardless of ghost status.
