# Browser Tetris

## Purpose and outcome

Provide a single-player desktop keyboard falling-block game, delivered as static browser assets. Players move and rotate falling tetrominoes, clear lines for points, recover from game over through restart and understand game state from the board and semantic controls.

## Intended scope

Use a 10×20 board, the seven tetrominoes, fixed-speed gravity, collision-safe placement, simultaneous line clears, scoring, game over and restart. TypeScript and Canvas provide the board, with HTML controls/status for readable labels and keyboard focus. Hiding or leaving the game suspends game time until explicit resumption.

Play includes shuffled 7-bag supply, once-per-cycle Hold, a projected ghost, horizontal wall kicks and hard drop. A piece normally locks after one full gravity interval from becoming grounded, including after hard drop. Supported movement does not renew the deadline; leaving support permits a fresh interval on re-grounding.

The ghost hides whenever any projected occupied cell lies above the board midline. A straddling ghost is hidden and one whose topmost cell is exactly at the midline is visible.

## Qualities, constraints and exclusions

Keep gameplay local and self-contained, with responsive input, distinguishable occupied/empty/active states, labeled controls and reliable restart. Chromium is the primary verification browser; managed Firefox is also required by the repository browser policy. Actual compatibility requires later execution evidence. Multiplayer, accounts, network leaderboards, mobile touch, audio and speed-level progression are outside the target.

## Decision basis

The classic brief and principal cross-scope interactions were accepted at initial review. The design uses their applicable behavior and agent-delegated detail; precise contracts and acceptance belong to SPEC. No implemented or tested product is claimed here.
