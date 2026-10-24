# System specification

## Context and ownership

This static single-player keyboard game follows [PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md). Engine owns rules and state; Session owns ordered events and game time; Presentation owns display and browser adapters own external effects. Requirements below describe intended behavior, not verified implementation.

## R-CORE — Board, pieces and transitions

The visible board has 10 columns (x=0–9) and 20 rows (y=0–19), increasing downward. Settled cells are empty or carry a shape/color identity. Active cells are separate until lock. A regular piece is valid only when every occupied cell is inside the board and does not overlap settled cells. Reject invalid lateral or rotation candidates without changing pose or consuming supply. A failed downward attempt locks under the failed-down policy. Lock revalidates the final cells, writes them exactly once, clears rows, scores, then spawns; reject corruption before any partial write. Spawn failure ends play without overwriting the stack.

Spawn orientations use these square masks (slash separates rows): I `..../IIII/..../....`; O `OO/OO`; T `.T./TTT/...`; J `J../JJJ/...`; L `..L/LLL/...`; S `.SS/SS./...`; Z `ZZ./.ZZ/...`. The square size is n. Spawn anchor is (floor((10−n)/2),0). A clockwise rotation maps each local cell (x,y) to (n−1−y,x); counterclockwise is its inverse. O remains unchanged. Four clockwise rotations restore the same cells. Rotation without kicks accepts only the rotated pose at the current anchor. No occupied cell may escape the top boundary during regular play; an invalid lock/top overflow is a loss without committing invalid cells.

Independent supply maps each uniform draw u in [0,1) to floor(7u), using order I,O,T,J,L,S,Z. A new game clears all settled cells, sets score to 0, resets supply and spawns one piece. The random source is injectable for deterministic rules tests; seeded replay is a test capability, not a required player feature.

## R-TIME — Input and game lifecycle

The game starts in ready state with Start. Running accepts movement; suspended, ready and game-over states reject movement. Left/Right move one column, Down attempts one row, Up rotates clockwise, Z rotates counterclockwise, Enter starts/restarts or resumes, and buttons provide labeled Start/Restart/Resume actions. Use keydown events: repeated lateral/down events are accepted one command each, rotation/start commands ignore event.repeat. Prevent page scrolling only for handled gameplay keys while the board game region owns focus. Events originating from buttons, links or editable/select controls do not produce gameplay commands; button activation retains native behavior. The game region has a visible keyboard focus indicator.

Gravity attempts one downward step every 1000ms of game time. Successful manual soft descent restarts the gravity interval; failed lateral/rotation input does not. Process an elapsed-time update chronologically across gravity and lock events; equal timestamps resolve an existing piece's lock before another descent/spawn event, with each piece locked at most once. The session must not advance game time while the page is hidden or its window is unfocused. Clear held-key state; resume only through explicit Resume/Enter from the game region, preserving remaining timers. Restart clears board/score, returns to running, and replaces piece state without registering duplicate event handlers or animation loops. Game over freezes game time until restart.

## R-CLEAR — Line resolution and score

After lock, find all full rows simultaneously, remove them, shift remaining rows down without changing their order, and insert empty rows at the top. Award 100/300/500/800 points for 1/2/3/4 rows in that lock, respectively; 0 for none. Do not award points for moves, soft drops or hard drops. Score never carries across restart. Gravity remains fixed; no speed levels are required.

## R-VIEW — Presentation and accessibility

Show board, active/settled piece cells, score, game state and control hints. Colors for the seven regular shapes are distinguishable and never pure white. Keep settled occupied cells visually separable from empty cells by cell outlines and contrast. Draw the active state and all status fields from one complete snapshot, within the next animation frame after an accepted command. Display game over and a usable restart action. Canvas has a programmatic board description; score/state updates are semantic DOM text, with a polite live status for loss/suspension and labels for controls. A missing 2D Canvas context shows an explanatory message and disables Start. Layout must fit a normal desktop viewport without clipping controls; mobile touch interaction is excluded.

## R-QUALITY — Delivery and verification

Production output is a static asset directory with locally bundled runtime assets. No network service, personal browser session or CDN is needed for gameplay. Build/dependency tooling may require network provisioning; compatibility is determined by the locked toolchain during implementation. Test deterministic geometry, lock/spawn, row clearing, scoring, restart and time suspension, then serve the actual application and exercise real keyboard/focus, visible Canvas and status behavior in isolated Chromium headless shell and managed Firefox under BROWSER_DEV_POLICY.md. Required failure on either browser blocks its acceptance claim; diagnose supported fallbacks rather than dropping coverage. No browser installation is needed for documentation authoring.

## Acceptance routes

| Route | Objective outcomes |
| --- | --- |
| A-CORE | Start, move, rotate and fall to a legal lock; wall/stack rejection leaves pose unchanged; blocked spawn reaches game over without stack overwrite. |
| A-CLEAR | Fixtures for 0–4 simultaneous rows produce exact compacted boards and stated score; restart produces empty board/zero score/fresh active piece. |
| A-TIME | Boundary-time and repeated-input checks preserve event order; hidden/blur suspends without catch-up; explicit resume/restart does not duplicate input or loops. |
| A-VIEW | Real served page accepts controls, isolates focused controls, renders recognizable occupied/empty/active cells, shows score/loss/restart and builds self-contained assets in both required browsers. |
