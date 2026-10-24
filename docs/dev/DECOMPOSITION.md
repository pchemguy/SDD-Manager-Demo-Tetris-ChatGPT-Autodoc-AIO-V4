# Component decomposition

## Logical model

Components refine the blocks in [ARCHITECTURE](ARCHITECTURE.md). Their interfaces below describe design seams; SPEC owns exact public contracts and values. No component requires a separate runtime service or framework.

| Component | Owns / provides | Requires / does not own | Verification seam |
| --- | --- | --- | --- |
| C1 Geometry | Tetromino offsets by orientation; occupied-cell transforms, board bounds, overlap predicates and row compaction. | Piece definitions and board data; no lifecycle, randomness or rendering. | Small board fixtures, coordinate transforms and conservation checks. |
| C2 Placement and rotation | Normal candidate validation, ordered SRS kick evaluation, mode-dependent candidate safety and one canonical landing calculation. | C1 and active mode; no queue or bonus spending. | Same board/pose yields same ghost/drop destination; penetrator holes and obstruction fixtures. |
| C3 Piece source | Seedable/random-injected piece generation, 7-bag permutation and next queue. | Random-number function; no Hold or visibility state. | Seeded permutations, bag boundaries and queue-consumption counts. |
| C4 Game transitions | Authoritative board/active/hold/score/lines/level/bonus/session state and command processing; atomic merge/clear/spawn. | C1–C3 and C5; no DOM or persisted settings. | Command/state fixtures and failure/no-op transitions. |
| C5 Timing | Gravity accumulator, game-time clock and per-active-piece lock deadline/policy snapshot. | Elapsed unpaused duration and placement/grounding results from C4; no wall clock or animation ownership. | Injected elapsed steps around exact deadlines, pause and large-frame cases. |
| C6 Configuration schema | Six setting types/defaults, key/value codecs and per-setting validation/resolution. | Raw source values; no direct cookie/history calls. | Mixed-source, invalid-value and default-equivalence tables. |
| C7 Persistence coordinator | Initial load, explicit-URL cookie sync, selected-setting saves and independent failure statuses. | C6 and cookie/history ports; no game state. | Fake browser ports and real same-origin reload checks. |
| C8 Input and lifecycle adapters | Keyboard filtering/repeat, focus/blur/visibility events and finite loop lifecycle. | Event targets and controller command/time interfaces; no rule duplication. | Native keyboard/focus/visibility tests and teardown counts. |
| C9 Presentation | Canvas board/piece/ghost painting; native controls, previews, text status and bonus symbols. | Read-only snapshot, effective/pending settings and callbacks; no landing algorithm. | Raster inspection plus labelled control/status assertions. |
| C10 Application controller | Composition root, one session, adapter binding, command ordering, settings handoff and render scheduling. | C4, C7–C9; no geometry or persistence codec duplication. | Full application startup, action, pause, restart, reload and destroy flows. |

## State and interfaces

C4 exposes a game creation boundary, a command transition, elapsed-time advancement and a read-only snapshot. Internal state contains board cells by regular piece kind; active kind/orientation/position/penetrator flag; hold kind and per-turn availability; queued kinds; score/lines/level; bonus count; lifecycle state; and C5 timing state. A rejected command yields an unchanged state and a reason suitable for status where meaningful. Snapshots provide the landing projection computed through C2; C9 does not recompute it.

C2 accepts board, active pose, mode and action. It returns either a safe pose/landing or rejection. Normal placement requires non-overlap; penetrator transient overlap is permitted only with a future safe landing. Rotation returns the first accepted candidate in its fixed kick order. Shared occupied-cell transforms eliminate disagreement between bounds, collision, ghost and rendering.

C3 exposes take/peek and an injected random source. Peeking is observational. A Hold operation belongs to C4: it either consumes one queued kind for an empty slot or exchanges with the held kind. A held kind carries no penetrator flag, orientation or timer. C4 resets incoming pose and requests a new C5 policy snapshot; the hold-used gate survives the exchange until lock.

C5 receives ordered game-time changes. It evaluates gravity/contact/deadline events in game-time order; C4 decides whether a lock position is valid. Deadline expiry alone cannot merge an airborne or overlapping piece. When a lock changes active-piece identity, C5 resets that piece’s timer and gravity accumulator while remaining frame time can continue through the new state. Pause and game over consume no game time.

C6 maps raw URL/cookie entries into a complete typed settings object and per-field origins. C7 reads once during page initialization, then handles individual changes through C6 validation. It returns effective settings plus cookie/history failure flags. C10 passes current eligibility/visibility immediately and pending lock selections for the next spawn; C4 captures the lock pair only when an incoming piece becomes active.

C9 receives read-only data and callbacks for change/start/pause/restart. It renders setting controls even when an option is temporarily inapplicable, explaining pending lock-policy changes and disabled penetrator Hold. A presentation refresh cannot mutate a queue, spend a bonus or reset a clock. C10 disposes event listeners and the scheduled animation callback on teardown, and does not bind a second loop on restart.

## Critical collaborations

1. Startup: C7 resolves settings; C10 creates C4 with injected source/time and binds C8/C9. A user action starts play; no persistence operation blocks game creation.
2. Input: C8 filters the target and emits a command; C10 orders it with time events; C4 checks phase/settings/rules, consulting C2. C10 renders the resulting snapshot.
3. Lock: C5 identifies an eligible event; C4 verifies safe grounding, merges four cells, clears full rows simultaneously, scores/awards bonuses, advances level and spawns from C3. C10 renders only the completed transition.
4. Change setting: C9 emits one valid selection; C7 updates session state and independently attempts both saves; C10 updates current/pending behavior and displays any persistence limitation.

## Boundaries and failure handling

Invalid user actions are ordinary rejections, not exceptions. An impossible spawn ends the game cleanly. Browser storage/history errors are confined to C7 and visible status. Rendering or setup exceptions must stop the owned loop and display an actionable startup failure rather than continue a half-initialized session. No personal sessions, browser profiles or external services are part of this design.

Review: every mutable state has one owner; rule dependencies are acyclic; C4 orchestrates C5 instead of giving the timing helper an upward dependency. Each important interaction has either a pure seam or an application-level check. This document has no focused children.
