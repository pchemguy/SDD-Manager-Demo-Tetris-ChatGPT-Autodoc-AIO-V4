# Browser Tetris

## Purpose and users

Provide a responsive single-player browser Tetris game for keyboard players, with an immediately playable classic core and optional modern mechanics. The complete product includes the enhancements, penetrator ability and persistent configuration below. Deliver a useful classic baseline first and introduce the rest through bounded playable increments.

## Complete target scope

- Classic falling tetrominoes, horizontal movement, rotation, gravity, line clearing, scoring, increasing level/speed, game over and restart.
- Hold, ghost, 7-bag randomization, wall kicks and hard drop. The default general lock policy waits one full gravity interval from grounding. Hard drop follows that policy unless immediate hard-drop locking is selected.
- Three ghost visibility modes: always hidden, dynamically hidden above the board midline, and always visible.
- A hotkey activates penetrator mode for the current piece when a bonus is available. It passes through occupied cells without removing them, stays active until lock, and locks only fully inside the board without overlap. Hard drop and ghost share its lowest valid landing position.
- A four-line clear earns one activation bonus, capped at three. Active penetrators are entirely white; regular pieces never use white. The side panel shows one symbol per available bonus and updates after earnings/spending.
- Six side-panel settings: ghost visibility; hard drop enabled; next preview enabled; hard-drop lock follows general policy or is immediate; general lock on failed downward attempt or after a full gravity interval; Hold enabled.
- Per-setting persistence resolves valid explicit URL value, then valid saved cookie, then default. A setting change updates its cookie and URL parameter. Valid explicit URL values, even defaults, are saved to cookies. An omitted parameter preserves its cookie value. Session configuration may precede persistence as a delivered increment.

## Proposed gameplay decisions

These proposals resolve consequential gaps in the supplied scope and require confirmation with this brief. They are not claimed as prior user decisions.

| Concern | Proposed resolution and reason |
| --- | --- |
| Playfield | Ten columns and twenty visible rows, with spawn space above. Use the occupied ghost cells for visibility decisions, not empty cells in its shape box. |
| Ghost straddling the midline | Show the dynamic ghost only when every occupied ghost cell is in the lower half: its topmost cell is at or below row 10, counting visible rows from zero. Hide the entire ghost when any part is above the midline. |
| Grounding and lock delay | Start one deadline at the piece’s first grounding, using the gravity interval then in effect. Movement, rotation, repeated hard drops and penetrator activation do not restart it. It continues while airborne, but expiry can lock only at a valid grounded position; an expired piece locks on its next valid grounding. Pause suspends game time. This prevents grounded movement from extending the delay indefinitely. |
| Failed downward policy | A failed player or gravity downward attempt locks a valid grounded piece. A successful hard drop alone does not simulate an extra failed attempt; the immediate hard-drop option overrides this. |
| Penetrator landing safety | Choose the lowest fully in-board, non-overlapping placement at or below the candidate position, ignoring intervening occupied cells. While active, occupancy does not block downward or horizontal movement or rotation; board boundaries still apply. An action that leaves no such landing is rejected. Gravity can traverse overlaps, but locking cannot. At the deepest valid landing, stop descent and apply the selected lock policy. This avoids reaching an overlapping floor position with no safe landing left. |
| Activation and Hold | Activation spends one bonus once, cannot be toggled off and does not reset timers. Activation on support may open a deeper landing and make the piece ungrounded, retaining its original deadline. Repeated activation is a no-op. Hold is disabled while penetrator mode is active, preventing storage or transfer of the ability. A locked penetrator reverts to the ordinary settled-piece colour, preserving white for the active ability. |
| Bonus lifecycle | Start each game with zero bonuses; game restart clears bonuses and held piece. A four-line clear made by a penetrator also earns a bonus, subject to the same cap. Normal Hold is allowed once per piece until lock. |
| Live settings | Visibility, hard-drop availability and Hold availability change immediately; hiding next preview does not change the queue. Disabling Hold preserves its stored piece. Lock-policy selections apply to the next spawned or held-in piece so a setting change cannot retroactively lock the current piece. |
| Invalid configuration | Treat an invalid URL value as absent for that setting, falling back to its valid cookie then default. Never save invalid values. Invalid cookies fall back to default. Preserve unrelated URL parameters and the fragment. If persistence is unavailable, continue playable session settings and show a concise status. |
| Defaults | Ghost always shown; hard drop, next preview and Hold on; general lock after one full gravity interval; hard drop follows general lock. |

## Proposed technical direction and exclusions

Use TypeScript, Canvas for the board and native HTML controls for settings and status, with a static deployable build and no backend. This provides direct control over the board and keeps the configuration keyboard accessible. A DOM-rendered board is a viable alternative with easier cell inspection; a UI framework is also possible but adds machinery unnecessary for this scope. The recommended direction is a proposal, not a pre-existing repository stack.

Use SRS wall kicks for a defined, testable rotation system. Exact controls, scoring, speed curve, spawn rules, random injection seams and configuration encodings belong in the specification. Keep conventional keyboard controls and avoid consuming gameplay hotkeys while a form control has focus. Include pause and restart to support practical play.

Proposed exclusions are multiplayer, backend leaderboards/accounts, touch controls, audio and exact certification against a commercial Tetris guideline. Board and status should remain readable, with accessible control labels and visible focus. Chromium is primary and Firefox is included under the repository browser policy; use isolated managed test environments.

## Delivery and success

The first release is a playable classic baseline; later releases deliver modern controls/assists, penetrator gameplay, session settings and persistence in useful bounded increments. Start at version 0.1.0 for the verified classic release, advance minor versions for subsequent capability phases and reserve 1.0.0 for the complete accepted target. Publish each release only after its phase is verified and integrated.

Success means the classic game remains playable as enhancements arrive, ghost and hard drop agree on landing for both piece modes, occupied cells are never destroyed by penetration, lock behavior is deterministic, and every setting restores independently with the specified precedence. Verify deterministic game rules separately from browser interaction/rendering and real URL/cookie reload behavior.
