# Gameplay contracts

## R1 Board, pieces and session

Visible board coordinates are x=0…9 and y=0…19, increasing right/down. Settled cells exist only in that rectangle and store a piece kind. Spawn space allows active occupied cells at y=-4…-1. Active cells must remain within x bounds, y≥-4 and y≤19. Ordinary active cells cannot overlap settled cells. Negative active cells are clipped while drawing. A lock with any cell above y=0 causes game over without merging an invalid piece.

Use kinds I, J, L, O, S, T and Z with four occupied cells each and the orientations in [ROTATION](ROTATION.md). Spawn orientation is 0, local box origin (3,-2). Top-out occurs when the incoming spawn cells overlap settled cells or violate active bounds. All spawns, including Hold, use the same rule. A failed spawn produces game over with settled board and final score retained; it does not allow actions on an invalid active piece.

Lifecycle states are ready, running, paused and game-over. Initial page shows ready; Start creates/runs a game. Restart from any state starts a new running game with empty board, score/lines=0, level=1, zero bonuses, empty Hold, unused Hold permission and a fresh source. Preserve chosen settings. Gameplay commands in ready/paused/game-over are no-ops; start/restart/pause controls remain available where meaningful. Resume explicitly returns paused to running. No gravity or timer game time accrues outside running.

## R2 Movement and input

Left/right translates one column, soft drop attempts one row. A rejected candidate leaves active state/timing unchanged, except a failed downward attempt can lock under R4. Rotate clockwise/counterclockwise uses [ROTATION](ROTATION.md); unsuccessful rotation is a no-op. Baseline rotation tests only the zero-offset candidate; the modern rotation capability applies the full table.

Default controls: Left/Right arrows move, Down soft-drops, Up or X rotates clockwise, Z rotates counterclockwise, Space hard-drops, C or Shift holds, P/Escape pauses/resumes, B activates penetration, R restarts and Enter starts from ready. Display these mappings. Prevent default only when handling an eligible gameplay key with play-area focus; never hijack R or Space in a control/editable target. Activation/hold/rotation/drop/pause/restart act once per physical key press; ignore repeated keydown for these actions.

Movement repeat is game-time driven: immediate left/right step, first repeat after 150 ms, then every 50 ms while held; Down repeats every 50 ms after its initial attempt. Suppress native repeat events so OS settings do not change the rate. If both horizontal keys are held, the most recently pressed wins; releasing it resumes the other after a new delay. Pause/blur/visibility loss clears held keys. After a lock while Down remains held, repeat can affect the incoming piece on its next scheduled interval; it never repeats a hard drop or Hold onto that piece.

## R3 Clearing, score and level

After a valid lock, merge exactly four cells; clear all full rows simultaneously, shift remaining rows downward without changing horizontal contents, and insert empty rows at the top. Clearing alone removes settled cells. Award 100/300/500/800 × the pre-clear level for one/two/three/four rows. No combo, back-to-back or spin bonuses. Soft-drop successful player steps award one point per row; hard-drop successful distance awards two per row. Gravity and rejected drops award none. Zero-distance hard drop awards zero.

Total cleared lines accumulate; level is 1+floor(lines/10). Gravity interval is max(50, 1000−75×(level−1)) ms. Update score, lines, level and bonus count before spawning the next piece. A four-line clear awards one penetrator bonus under R7 even when the clearing piece was a penetrator; cap at three. No bonus for separate clears whose sum is four.

## R4 Gravity and lock timing

Each active piece captures the selected general and hard-drop lock policies on spawn, including Hold exchange; the initial default is interval/follow. Its gravity accumulator begins at zero. At each gravity interval attempt one downward row. Successful soft/hard drop does not reset the gravity accumulator. Level changes affect the next piece’s interval; the current piece’s captured grounding delay is never changed.

An ordinary piece is grounded when moving down one row is invalid. A penetrator is grounded only at its deepest safe landing (R7), not at an intervening occupied row. Record firstGroundedAt at the first valid grounding of that active piece, whether reached by movement, rotation, gravity, hard drop or spawn. Under interval policy, deadline=firstGroundedAt+the gravity interval at that contact. Never reset it for grounded movement, rotation, leaving support, rejected actions, repeated drops or activation. It continues through airborne game time. Expiry locks only when presently grounded at a valid non-overlapping visible placement; otherwise retain expired state and lock immediately upon the next valid grounding. Pause excludes duration from game time.

Under failed-down policy, only a failed downward attempt from a valid grounded position locks. Gravity while grounded counts as such an attempt; horizontal/rotation failures do not. Under interval policy a failed downward attempt before deadline leaves the piece active. Hard drop moves to the canonical landing, awards its distance score, and establishes grounding. With follow policy it does not synthesize an additional failed attempt or reset an existing deadline. With immediate policy it attempts lock in that transition. A visible-safe lock is still mandatory; ordinary negative-row top-out ends the game without invalid merge.

Advance finite nonnegative elapsed milliseconds in chronological order, processing all gravity/deadline events within the duration and carrying remaining time across locks/spawns. Reject negative/nonfinite time inputs without mutation. At equal timestamps evaluate an already-grounded expired deadline before gravity; a gravity step producing contact then evaluates that contact/deadline. Process elapsed time up to an input event before its command, so an already-due lock cannot be evaded by a late activation. No arbitrary frame clamp may change deterministic core results. Browser hiding/blur pauses rather than simulating hidden backlog.

## R5 Source, preview and Hold

With seven-bag enabled, shuffle one occurrence of each kind using injected random values in [0,1), consume the bag, then generate another. Each seven-item bag is a permutation; repeats may cross a bag boundary. Tests can supply a fixed kind sequence independent of production randomness. The classic baseline may use independent uniformly selected kinds instead; it must expose an injection seam and need not implement a bag early.

Next preview displays one queued kind in spawn orientation when enabled; hiding/showing it never consumes or regenerates the queue. On a normal spawn consume one kind. Hold is accepted only while running, enabled, unused since the last lock and not penetrator-active. Empty Hold stores the active kind and consumes one queued kind; nonempty Hold swaps kinds without consuming the source. Incoming pose/orientation/timing/lock-policy capture reset to spawn defaults. Mark Hold used for the incoming piece and reset permission only after a lock. Failed incoming spawn is game over. Disabled or penetrator Hold is a no-op with no source/bonus/timer side effects; disabling/re-enabling Hold preserves its contents.

## R6 Ghost and hard drop

Normal landing is the last pose reachable by successive downward steps before first obstruction; do not skip over normal blockers. Penetrator landing follows R7. Ghost and hard drop consume the same canonical result for the same board/pose/mode. Hard drop translates straight down without rotation; when disabled, its key is a no-op. A zero-distance drop still follows the selected locking policy. The same active piece can be hard-dropped repeatedly without replenishing time.

Always-hide draws no ghost. Always-show draws the projection, clipped to the visible board. Dynamic mode draws it only if the minimum occupied projected y is at least 10. A straddling piece or projection entirely above the midline is wholly hidden; empty shape-box cells do not affect visibility. No active piece means no ghost. A normal projection ending above the visible board can be clipped, but cannot make an unsafe lock valid. Ghost visibility affects no physics or score.

## R7 Penetrator and bonuses

B activates only while running with an ordinary active piece, at least one bonus and at least one fully visible, non-overlapping landing at/below its current origin y for its current x/orientation. Reject activation without these conditions and spend nothing. Accepting activation spends one bonus and sets the active flag until lock/game end; repeated B cannot toggle it or spend again. No queued/held/settled piece stores this flag. Existing gravity/deadline state remains, including when support is penetrated and the piece becomes airborne.

For penetrator landing, enumerate candidate origins at or below current y whose occupied cells fit in x=0…9, y=0…19 and do not overlap the board; select greatest y. Intervening occupied cells are irrelevant. Transient downward, horizontal and rotational poses may overlap settled cells, but active bounds and existence of such a safe future landing are mandatory. Reject any action that would strand the piece with none. Descend one row per successful gravity/soft-drop attempt until the selected deepest safe landing; at it, reject further descent and apply R4. Do not descend beyond the safe landing into an overlapping floor position. Rotation uses the first safe candidate in the same ordered kick table.

Hard drop selects that deepest safe placement directly; ghost previews it. Every lock revalidates the placement and never overwrites settled cells. Render the active penetrator entirely white. Its settled cells use the ordinary kind colour after locking. Hold is disabled throughout activation, even if the Hold setting is on. Show exactly bonusCount lightning symbols (0…3) in the side panel, with textual accessible count; update after each spend/award. Restart resets bonuses; a spend followed by a four-line clear can earn one back.
