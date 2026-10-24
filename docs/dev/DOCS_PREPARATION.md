# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, explicitly requested with six predefined cumulative scopes.
- Delivery mode: strict multipass (default); preserve earlier PLAN/TASKS ranges, identities, membership, order, dependencies and exits. Add later scope through subsequent bounded phases. Flexible integration has not been authorized.
- Current pass: 4. Cursor: DOCS-008; authoritative checkboxes are in DOCS_TASKS.
- Approval basis: first PROJECT approved by the user ("Approve") for published proposal 4956e55ca34db646224af4c647958cc4cc6d5d47, PROJECT SHA-256 7e19287725d97e6e8b56e4f554b4af14a99b9ba9e6ffeec9e06578742d7d9965 and its cross-scope proposals. Later PROJECT approvals are waived under the announced autoloop policy; ARCHITECTURE through TASKS are preapproved within each agreed scope. New material choices after first approval are delegated to the agent, with visible rationale and durable records.
- Tracking: enabled for preparation and implementation by root AGENTS.md. The sdd-docs-main milestone #1 and DOCS-001–009 issues #1–9 were created from this repository's bundled fixed definitions and individually read back before repository modifications.
- Publication: push/read back each owned commit before progression. Standard reporting; Minimal and Explicit profiles are available.
- Next boundary: execute the predefined loop through pass-6 DOCS-008, then stop before DOCS-009, whole-package QC, documentation integration or implementation.

## Scope sequence

1. **Playable classic baseline:** Falling tetrominoes, movement, rotation, gravity, line clearing, scoring, game over and restart. Keep the scope minimal; later additions stay in this record until their turn.
2. **Gameplay enhancements:** Hold, ghost, 7-bag, wall kicks and hard drop. Default lock delay is one full gravity interval from becoming grounded, including hard drop.
3. **Conditional ghost visibility:** Hide the projected ghost above the midline; show it in the lower half.
4. **Penetrator mode:** Hotkey spends one available bonus to activate the current piece until lock. Pass through occupied cells without destruction; lock entirely inside the board with no overlap. Hard drop and ghost use the lowest valid landing. Four-line clear awards one bonus, capped at three. Entirely white active penetrator; regular pieces never white. Side panel displays one symbol per bonus and refreshes on earning/spending.
5. **Session-only configuration:** Side panel controls ghost visibility (hidden/dynamic/shown), hard drop (off/on), next preview (off/on), hard-drop lock (general/immediate), general lock (failed down/full interval), hold (off/on). Add next preview. Defaults and runtime updates as proposed below; reset settings on reload, with no persistence in this scope.
6. **Configuration persistence:** Each of the six settings independently resolves explicit valid URL value, then valid cookie, then default. Changes save the setting cookie and update its URL parameter. Explicit valid URL values, including defaults, are saved to cookies; omitted parameters preserve saved cookies. Invalid inputs and unavailable persistence follow the decisions below.

## Per-pass decisions

The user accepted the initial PROJECT and these interaction proposals by replying "Approve" to published proposal 4956e55ca34db646224af4c647958cc4cc6d5d47. The choices retain their agent-proposed origin; approval covers their adoption at the listed scopes. Their originating pass is 1 (initial exploration); applicability identifies when they enter product documents. Later passes retain these summaries and record new decisions or supersession with reasons.

| Pass / decision | Resolution and rationale | Basis / source | Applicability / status |
| --- | --- | --- | --- |
| 1 / Platform | Single-player desktop keyboard browser game; static delivery without backend. TypeScript with Canvas board and semantic DOM controls is the recommended technical direction; architecture will choose tooling. This keeps deployment simple and game rules testable. | Browser target from user; remaining choices are agent proposals. | All scopes; accepted at initial checkpoint. |
| 1 / Minimal rules | 10×20 visible board, seven tetrominoes, fixed gravity, simple rotation with blocked rotations rejected, independent uniform piece draws, lock on failed down, points for line clears, game over on blocked spawn/top-out, clean restart. No speed levels are required. | Agent proposal to satisfy minimal baseline. | Pass 1; accepted at initial checkpoint. |
| 1 / Ghost midline | Use the topmost occupied ghost cell: show only if every cell lies in the lower half (row 10 or below on a 20-row board). A straddling ghost is hidden; exactly row 10 is visible. | Agent proposal: no ghost cells remain in the upper half. | Passes 3–6; accepted at initial checkpoint. |
| 1 / Lock timing | Start the interval when a piece first becomes grounded. Supported lateral motion/rotation does not reset it; leaving support cancels it and a later grounding starts a fresh interval. Successful descent clears old grounding. Repeated down/hard-drop input does not restart a running interval. Freeze game time on blur/hidden page to prevent background timing surprises. | Agent proposal to avoid infinite supported resets and stale timers. | Full-interval timing in passes 2–6; background suspension in baseline. Accepted at initial checkpoint. |
| 1 / Hard drop | Move to the ghost-equivalent landing. Default uses the remaining general grounded interval, starting one only if newly grounded; immediate setting locks at once at a valid landing. | User requires delayed default; agent proposes repeated-input semantics. | Passes 2–6; immediate option only from pass 5. Accepted at initial checkpoint. |
| 1 / Hold and activation | Hold is once per active-piece cycle, reset after lock, and disabled while penetrator is active. Activation is one-way until lock, spends exactly one bonus and is rejected without a bonus, outside a running game or when already active. Restart clears held piece and bonuses. | Agent proposal; consistent with the established penetrator/hold preference, presented for this repository's approval. | Hold from pass 2; penetrator interaction from pass 4. Accepted at initial checkpoint. |
| 1 / Penetrator safety | Use the deepest non-overlapping in-board pose at or below the current pose for the current column/orientation. Gravity can traverse occupied cells toward it; that destination defines grounding. Reject a move/rotation with no valid destination at or below it. Lock timers never write an overlapping pose. Ghost, gravity and hard drop share this destination. Activation recalculates grounding without renewing a still-valid timer. | Agent proposal to prevent overlap, trapped pieces or divergent drop previews. | Passes 4–6; accepted at initial checkpoint. |
| 1 / Bonus lifecycle | Four-line clear awards one bonus, capped at three, after the piece locks. Either ordinary or penetrator pieces can earn it. Restart clears bonuses; active/bonus visuals distinguish them. | User's award/cap requirements; lifecycle details accepted at initial checkpoint. | Passes 4–6; accepted at initial checkpoint. |
| 1 / Runtime settings | Ghost and preview changes apply on the next render. Hard-drop enablement, hold enablement and both locking policies take effect on the next spawned piece (including a piece supplied by Hold); snapshot mechanics for the current piece to avoid sudden locks. Disabling hold preserves its stored piece for re-enabling. Restart retains settings and applies all selected values. | Agent proposal: predictable mid-piece behavior with controls showing pending mechanics. | Passes 5–6; accepted at initial checkpoint. |
| 1 / Defaults | Dynamic ghost, hard drop on, next preview on, hard-drop lock follows general, general lock full interval, hold on. | Agent proposal; retains previously introduced gameplay behavior. | Passes 5–6; accepted at initial checkpoint. |
| 1 / Persistence fallback | Parse each setting independently with explicit allowlists. Invalid URL values fall through to cookie/default without overwriting a valid cookie; invalid cookies fall through to default. Use first occurrence for duplicate query keys. Persist valid explicit URL values even if default. Preserve unrelated URL parameters and hash; update via history replacement without navigation. Use namespaced cookies, root path, SameSite=Lax and one-year lifetime. Cookie/history errors keep session settings usable and display a concise persistence notice. | User defines precedence and explicit-value persistence; error, duplicate and transport policies accepted at initial checkpoint. | Pass 6; accepted at initial checkpoint. |
| 1 / Releases | Plan v0.1.0 for the first verified playable phase, then increase minor versions for capability phases; use patch versions for fixes and reserve v1.0.0 for an explicitly stabilized complete target. Publish a release after each implemented, verified and integrated phase using its corresponding tag and release notes. No tags/releases during documentation preparation. | User requires version management and releases after later authorized implementation; numbering accepted at initial checkpoint. | Delivery planning and later authorized implementation; accepted at initial checkpoint. |
| 2 / Current scope | Adopt inherited Hold/ghost/lock timing choices. Select horizontal kick offsets [0,-1,+1,-2,+2], no vertical kicks or Guideline SRS claim; split assisted supply/ghost and rotation/drop timing into bounded phases. Tooling is TypeScript/Vite/Vitest/Playwright, with versions locked at implementation. | Delegated-agent detail under accepted autodoc/autoloop; inherited initial choices retain human acceptance. | Scope 2 onward; active. |
| 3 / Current scope | Carry forward the accepted topmost-cell midline rule; no new product choice. Keep a narrow visibility phase because the policy has an independent visual acceptance boundary. | Delegated-agent detail under accepted autodoc/autoloop; inherited initial choices retain human acceptance. | Scope 3 onward; active. |
| 4 / Current scope | Carry forward accepted deepest-valid landing and Hold prohibition. Set white appearance on active and settled penetrator cells; reject moves with no safe landing at/below them, and suspend on impossible invalid-lock state rather than mutate settled cells. | Delegated-agent detail under accepted autodoc/autoloop; inherited initial choices retain human acceptance. | Scope 4 onward; active. |

## Cross-scope decisions

| Concern | Decision / applicable scopes | Reconsideration condition |
| --- | --- | --- |
| Scope separation | Minimal rules govern pass 1 only. Later cumulative scopes adopt the relevant per-pass decisions into their documents; never pre-load them into the baseline. | Explicit scope steering. |
| Delivery preservation | Strict mode protects each prior phase/task range. Add enhancements/configuration as later bounded increments. | Explicit flexible-multipass authorization or a reported conflict. |
| Drop consistency | Ghost midline, lock timing, hard-drop and penetrator safety decisions jointly govern passes 2–6. | New board geometry, rotation or penetrator behavior. |
| Hold/settings | Hold and activation plus runtime settings define passes 4–6 interaction; settings cannot revoke an active penetrator or reset its timer. | Explicit gameplay steering. |
| Input precedence | Persistence fallback applies independently to each of the six settings; pass 5 remains session-only. | New setting/source or changed precedence. |

## Decisions and document evidence

| Task | Current evidence / decision basis |
| --- | --- |
| DOCS-001 | All four root guidance files existed and were preserved byte for byte against c3042851137db6c467c591c9c65450f2f7fe6fc5. Task template copied from bundled 0.15.2 source with only DOCS-001 checked. Initialization includes this record and HANDOFF. Initialization commit e750fd9e849d7e35b400ec4291ddebbb46348f21 was pushed/read back exactly; issue #1 was closed as completed and individually read back with milestone #1 association. |
| DOCS-002 | Pass 4: PROJECT.md SHA-256 ca19ba84895c26c0256d0255d1236b90ab6fd55380ae9786e6cab9f3426f6d5b. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-003 | Pass 4: ARCHITECTURE.md SHA-256 2a377c37a55d6834491062486d7b636f22dfb3c5f7cce2408c8d3edfa24e7db5. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-004 | Pass 4: DECOMPOSITION.md SHA-256 47308c7ea7ba7d41311267c090b56967cf20d78233b75adeecca3956148ff835. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-005 | Pass 4: SPEC.md SHA-256 87e822bb79c7c7de42e0314804a9bc0b6bf31f97e590e71178ae462979b3b2f3; SPEC-REVIEW-REPORT.md SHA-256 90ed85adbbe6d95def5167a7e1c10de0f308f02ef105d3b816b586917817a10b. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-006 | Pass 4: PLAN.md SHA-256 f675ce063118ca8ea025b134accb6e0c4efef4085a1da0fb06ad02cdb4f79755; PLAN-REVIEW-REPORT.md SHA-256 c07ad6ffc191adc77b6dc63474036ccb9d2c8d85e2696e1d0a4b64ba1bce0786. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-007 | Pass 4: layout.md SHA-256 31282117af53ec44801fa4980fb4f2418bb98bbfe39a38f2c6525b027496df20; PLAN-REVIEW-REPORT.md SHA-256 af8d2f0fb7d1893ad7774d75a3c60271662e3a242998c778cc6571a38c60430f. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-008 | Pass 3: TASKS.md SHA-256 1351e216750402d67c5c62447a4a5cddc91a68c38d58b810897e970659310d4a; TASKS-REVIEW-REPORT.md SHA-256 d4cc385c40b9bc88689de0f1a4971f606a13640f84d740305a0383180697333d. Current-scope owner review and linked adjacent QC where required passed; unchanged retained inputs reviewed for current applicability. Scoped autodoc/autoloop preapproval from initial PROJECT acceptance; publication and issue closure follow this completion commit. |
| DOCS-009 | Unselected; remains pending at final autoloop stop. |

Material decisions: initial exploration choices above are accepted; later material details are delegated under autoloop. No product implementation is authorized.

## Initialization and current reset

- Root files retained: AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md and SKILL_DISCOVERY_PROTOCOL.md. None copied or altered. All-present case permits continuation to the PROJECT proposal without an initialization approval pause.
- Manual provenance: default enabled. Seed 943225c54c354cc4566c0c4c55f38933e9cd2b2a from main c3042851137db6c467c591c9c65450f2f7fe6fc5 contains the two byte-identical bundled scaffold files and necessary token exclusion. Explicit two-parent merge into main: bd2bfc52a4f8f923981d656ff048e4f8e3990e95. Both branch publications were read back as matching before design-docs/main creation. No transcript was recorded.
- Current reset: from scope 3 completed checkpoint 59d41e912b9274d8a75b549933f7e03b76919614 to scope 4; predefined autoloop authorization after initial PROJECT approval. DOCS-001 retained; DOCS-002–009 unchecked. Existing documents, decisions and phase/task ranges retained.
- Prior-pass evidence: scope 1 DOCS-008 checkpoint b1b773dfc0d643e8fd5e26bfc28189007f1579e7; later resets retain their own Git checkpoints and range summaries.

## Scope 1 delivery ranges and checks

Phase 1: T-001–T-007. Earlier established blocks remain byte-identical. All applicable initial cross-scope decisions were reviewed and carried forward; current owner QC is in the adjacent reports. No unresolved document blocker was retained. Required next effects: completion commit publication and issue #8 closure.

## Scope 2 delivery ranges and checks

Phase 1: T-001–T-007; Phase 2: T-008–T-013; Phase 3: T-014–T-018. Earlier established blocks remain byte-identical. All applicable initial cross-scope decisions were reviewed and carried forward; current owner QC is in the adjacent reports. No unresolved document blocker was retained. Required next effects: completion commit publication and issue #8 closure.

## Scope 3 delivery ranges and checks

Phase 1: T-001–T-007; Phase 2: T-008–T-013; Phase 3: T-014–T-018; Phase 4: T-019–T-021. Earlier established blocks remain byte-identical. All applicable initial cross-scope decisions were reviewed and carried forward; current owner QC is in the adjacent reports. No unresolved document blocker was retained. Required next effects: completion commit publication and issue #8 closure.

## Pending transitions

Publish/read back this pass-4 DOCS-007 completion, then close/read back issue #7. Recover actual later effects before retrying. Next eligible document: DOCS-008.
