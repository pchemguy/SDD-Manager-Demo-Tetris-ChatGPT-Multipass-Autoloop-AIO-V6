# Browser Tetris

## Purpose and outcome

Provide a single-player falling-block game that a player can open in a desktop browser and play with a keyboard. The game should make movement, rotation, falling, line clearing and loss understandable, and allow a fresh game immediately after game over.

## Scope

The game has a rectangular board, the seven tetromino shapes and one active falling piece. The player moves and rotates that piece while gravity advances it. A piece that cannot move down locks into the board; complete rows clear, remaining rows collapse and the score increases. Play ends when a new piece cannot enter or a locking piece exceeds the playable top boundary. Restart clears the board and score and begins a new game.

The proposed minimal rules use a 10-column, 20-row visible board, a fixed gravity speed, independently randomized pieces and simple rotation that rejects blocked positions. Controls and score must remain visible. Moving focus to controls must not also move a piece; hiding or leaving the game suspends game time until deliberate resumption.

## Qualities and delivery constraints

Deliver the game as static browser assets without an application backend or account. Keyboard input should feel responsive, the active piece and settled blocks must be distinguishable, and game state and score must agree with the displayed board. Restart must work reliably without reloading the page.

Use Chromium as the primary verification browser and include Firefox according to the repository's browser policy. Actual browser provisioning and execution evidence belong to implementation; document preparation claims no browser compatibility result.

The recommended technical direction is TypeScript, a Canvas board and semantic HTML status/controls. Architecture will define component boundaries and tooling after acceptance of this brief.

## Proposed boundaries

Keep the playable scope focused on the rules above. Exclude multiplayer, accounts, network leaderboards, mobile touch input, audio and a speed-level progression system from the current target. No runtime dependencies on external services are needed.

## Decision state

The user's classic gameplay requirements define the requested outcome. Board size, fixed speed, randomization, blocked-rotation behavior, background suspension, technical direction and the proposed boundaries above are agent recommendations awaiting acceptance. Precise controls, scoring values, spawn rules and timing will be specified consistently with the accepted brief.
