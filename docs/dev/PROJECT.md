# Browser Tetris

## Purpose and outcome

Provide a single-player desktop keyboard falling-block game, delivered as static browser assets. Players move and rotate falling tetrominoes, clear lines for points, recover from game over through restart and understand game state from the board and semantic controls.

## Intended scope

Use a 10×20 board, the seven tetrominoes, fixed-speed gravity, collision-safe placement, simultaneous line clears, scoring, game over and restart. TypeScript and Canvas provide the board, with HTML controls/status for readable labels and keyboard focus. Hiding or leaving the game suspends game time until explicit resumption.

Play includes shuffled 7-bag supply, once-per-cycle Hold, a projected ghost, horizontal wall kicks and hard drop. A piece normally locks after one full gravity interval from becoming grounded, including after hard drop. Supported movement does not renew the deadline; leaving support permits a fresh interval on re-grounding.

The ghost hides whenever any projected occupied cell lies above the board midline. A straddling ghost is hidden and one whose topmost cell is exactly at the midline is visible.

Players earn one penetrator bonus for a four-line clear, up to three. A hotkey spends a bonus to turn the active piece white until lock. It traverses occupied cells without destruction, lands in the deepest safe placement, and uses the same destination for ghost and hard drop. Hold is disabled while active; the side panel shows each available bonus.

Six side-panel settings select ghost visibility, hard drop, next preview, hard-drop lock policy, general lock policy and Hold. Display changes apply immediately; mechanical changes apply at the next piece. Restart retains selected settings. Next preview does not consume supply.

All six settings restore independently from explicit valid URL value, saved cookie or default, in that order. Selected-value changes save cookies and update URL parameters without reloading. Explicit valid URL values, including defaults, save to cookies; omitted parameters preserve saved values. Invalid input falls through independently and failed persistence preserves usable session state.

## Qualities, constraints and exclusions

Keep gameplay local and self-contained, with responsive input, distinguishable occupied/empty/active states, labeled controls and reliable restart. Chromium is the primary verification browser; managed Firefox is also required by the repository browser policy. Actual compatibility requires later execution evidence. Multiplayer, accounts, network leaderboards, mobile touch, audio and speed-level progression are outside the target.

## Decision basis

The classic brief and principal cross-scope interactions were accepted at initial review. The design uses their applicable behavior and agent-delegated detail; precise contracts and acceptance belong to SPEC. No implemented or tested product is claimed here.
