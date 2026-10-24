# Behavioral specification

## Scope and ownership

The complete static browser game follows [PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and components C1–C10 in [DECOMPOSITION](DECOMPOSITION.md). Gameplay rules are independent of browser APIs. Requirements describe intended behavior; implementation and browser acceptance must supply their own observed evidence.

| Contract | Canonical owner / detail | Structural participants |
| --- | --- | --- |
| R1 Board, pieces and session | [Gameplay](spec/GAMEPLAY.md#r1-board-pieces-and-session) | C1, C3–C5, C10 |
| R2 Movement, rotation and input | [Gameplay](spec/GAMEPLAY.md#r2-movement-and-input), [rotation data](spec/ROTATION.md) | C1, C2, C4, C8 |
| R3 Clearing, score and level | [Gameplay](spec/GAMEPLAY.md#r3-clearing-score-and-level) | C1, C4, C9 |
| R4 Gravity and lock timing | [Gameplay](spec/GAMEPLAY.md#r4-gravity-and-lock-timing) | C2, C4, C5, C8 |
| R5 Source, preview and Hold | [Gameplay](spec/GAMEPLAY.md#r5-source-preview-and-hold) | C3, C4, C9 |
| R6 Ghost and hard drop | [Gameplay](spec/GAMEPLAY.md#r6-ghost-and-hard-drop) | C2, C4, C9 |
| R7 Penetrator and bonuses | [Gameplay](spec/GAMEPLAY.md#r7-penetrator-and-bonuses) | C1, C2, C4, C9 |
| R8 Six settings and live effects | [Configuration](spec/CONFIGURATION.md#r8-schema-and-live-effects) | C4, C6, C9, C10 |
| R9 Cookie and URL persistence | [Configuration](spec/CONFIGURATION.md#r9-resolution-and-persistence) | C6, C7, C10 |
| R10 Browser interaction, quality and delivery | Below | C8–C10 |

## R10 Browser interaction, quality and delivery

Serve a static build over HTTP(S), without a backend, accounts or network gameplay services. No game-state restore, multiplayer, mobile-touch controls, audio or commercial-guideline certification is required. TypeScript source must type-check; production build and deterministic tests must pass using pinned dependencies/lockfile. Windows hosts use the repository’s [shell policy](../../WINDOWS_SHELL_POLICY.md).

Chromium is primary and Firefox is included in application coverage using compatible isolated managed builds under [browser policy](../../BROWSER_DEV_POLICY.md). Verify real application launch, native keyboard actions, pause/restart, at least two isolated contexts, visible board/ghost/bonus rendering, configuration changes and reload persistence on each browser. Provisioning alone is not application acceptance. Finite whole-process/action deadlines and owned teardown are required; missing browser evidence blocks the affected phase exit rather than silently removing a browser.

Use Canvas for board rendering and native labelled inputs/selects/buttons for configuration. Show score, lines, level, lifecycle status and available bonuses as text/symbols, with accessible names and visible keyboard focus. Each of the seven ordinary kinds has a distinct non-white colour. Active penetrator blocks use white fill; after lock they use their kind’s ordinary colour. Ghost uses a translucent/outlined projection visually distinct from both active and settled blocks. The complete visible board and side panel must be usable without overlap at desktop viewports from 800×600 upward. No screen-reader interpretation of every Canvas cell is required; controls and status must remain accessible.

Game actions must not fire while a form control, editable region or button has focus. Capture/prevent scrolling only for accepted gameplay keys while the board/play area has focus. Provide readable controls help. Blur or document hiding pauses a running session and clears held input; focus/visibility return does not automatically resume it. A paused session retains board, active pose, timer and score. Restart creates one fresh game without duplicating event listeners or the animation loop; configuration remains selected. Teardown cancels the owned scheduled frame and removes listeners.

Use game time rather than rendered frame count. Deterministic tests inject elapsed time and random values. In a foreground running session, the next rendered frame after processing an action must reflect its resulting state; avoid a fixed FPS acceptance threshold dependent on unspecified hardware. Unexpected startup/render failures stop the loop and expose an actionable message. Storage/history failures use R9’s recoverable status. No expected rejected gameplay action throws an uncaught exception.

## End-to-end acceptance

- A fresh session can start, move/rotate/drop pieces, clear lines, increase score/level, pause/resume, reach game over and restart; occupied cells stay within the board and every lock contributes exactly four cells before clearing.
- The same injected source and timed command sequence produces the same core state. One long time step and equivalent subdivisions produce the same state where command order is unchanged.
- Ordinary wall/floor collisions reject movement; rotation follows the declared kick order. Hold, preview and seven-bag consumption obey R5.
- Ghost/drop landing agrees for ordinary and penetrator modes. Dynamic ghost hides the whole projection when any occupied cell is above row 10 and returns when all are at/below row 10.
- Delayed locks occur at the captured first-grounding deadline only in valid grounding. Airborne expiry, repeated hard drop, pause, activation and both policy selections follow R4. Immediate hard drop is the sole drop-specific override.
- A seeded four-line-clear fixture increments bonuses up to three; activation spends exactly one, prevents Hold, traverses occupied rows safely and never deletes settled cells except through completed-line removal.
- All six configuration controls affect their declared behavior; cross-source and reload fixtures prove independent URL/cookie/default resolution, explicit default saving, omitted-value retention and unrelated URL preservation. Failure injection proves a playable session when either persistence port fails.

These outcomes apply when their capability is included in the delivered phase. Earlier phase exits preserve their included behavior without claiming completion of later contracts. Exact phase allocation belongs to PLAN.
