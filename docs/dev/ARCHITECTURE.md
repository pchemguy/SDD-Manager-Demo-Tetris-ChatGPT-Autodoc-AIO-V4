# System architecture

## Context and direction

The [project brief](PROJECT.md) defines a static single-player browser game. A TypeScript rules core owns gameplay without depending on the DOM, Canvas, cookies, URLs or wall-clock time. Browser adapters deliver commands and elapsed game time, expose configuration and render snapshots. No server or framework runtime is required. Build tooling runs during development and emits static assets.

## Major blocks

| Block | Responsibility and state | Dependencies |
| --- | --- | --- |
| Rules core | Board, active and held pieces, queue, score, level, bonuses, lifecycle and timing. Produces a read-only view and transition result. | Geometry, placement/landing, rotation and random source supplied through explicit seams. |
| Application controller | Serializes input, elapsed-time updates, settings and rendering; owns the browser session and adapter lifetimes. | Rules core and browser adapters. |
| Presentation | Draws the board, active/ghost pieces and previews; updates score, bonus symbols, settings and status. Owns no game rules. | Snapshot and validated setting values. |
| Configuration | One typed six-setting schema and codecs; independent source precedence, cookie/URL reconciliation and persistence status. | Injected cookie and location/history adapters; no game mutation. |
| Browser boundary | Keyboard/focus events, animation scheduling, document visibility, Canvas/DOM and browser persistence. | Web platform only; calls controller-facing interfaces. |

Dependency direction is browser/controller → core; presentation consumes projections. Configuration emits validated values to the controller. The core never calls an adapter. Geometry/landing has no dependency on lifecycle; lifecycle composes it. Keep one application process and one active game loop per page.

## Gameplay ownership and collaboration

A single game state is authoritative. Commands and elapsed-time updates are processed sequentially, never concurrently with rendering. The transition boundary owns lock → merge → simultaneous clear → score/bonus update → next spawn as one transaction. A renderer cannot observe a partially cleared board. Spawn failure produces game over rather than a partial active piece.

Both ghost and hard drop call one landing service against the same immutable board and active-piece mode. Normal landing stops before the first obstruction. Penetrator landing searches for the deepest valid placement while ignoring intervening occupancy; candidate moves must preserve a safe landing. Contact and lock eligibility are mode-dependent but the lock-timer owner is shared. A penetrator flag belongs only to the active piece; it never enters the hold slot, queue or settled board.

Time enters as elapsed unpaused game time. The core owns gravity accumulation and the first-grounding deadline; the controller converts animation timestamps and excludes paused/hidden duration. Capture both lock policies at each spawn, including a Hold exchange. Other settings affect current presentation/command eligibility. The core validates commands again even when the UI disables an action.

## Persistence boundary

The configuration schema is the sole owner of defaults, names, accepted values and decoding. Initialization reads every setting independently: valid explicit URL → valid cookie → default. It then saves valid explicit URL values to the corresponding cookies. Interactive changes update session state first and attempt cookie/history writes independently. Browser failures leave the session usable with visible status. No full-board or saved-game persistence is included.

Only the selected setting’s parameter and cookie may change during an interactive update; unknown URL parameters and fragment survive. Storage adapters report failures as results; they never throw through the game loop. Cookie blocking does not disable URL configuration, and history failure does not disable cookies.

## Structural choices and tradeoffs

A pure core makes placement/timing/bonus behavior reproducible with injected time and randomness; it adds a small explicit adapter boundary instead of coupling rules to animation events. Canvas keeps board painting compact; native HTML keeps settings and textual status accessible. A DOM board or UI framework remains unnecessary for this product’s selected interaction model. No generic plugin, event bus, dependency-injection container or asynchronous worker architecture is needed.

Use Vite for development/static bundling, Vitest for deterministic core/adapter tests and Playwright for Chromium and Firefox application checks. Pin actual compatible versions and a lockfile when tooling is implemented; do not infer installed versions or browser readiness from this design. Browser setup follows root BROWSER_DEV_POLICY.md, including isolation and finite diagnostics. Windows execution follows WINDOWS_SHELL_POLICY.md.

## Invariants and verification seams

- Only the core writes game state; published snapshots cannot mutate it.
- Every lock is in bounds and disjoint from occupied cells. Penetration never deletes cells; line clearing alone removes completed rows.
- Ghost and hard drop use the same landing result. Presentation changes neither queue consumption nor timing.
- Input adapters cannot route gameplay keys from editable/select/button controls into the core. Pause and visibility transitions cannot add hidden elapsed time.
- Geometry, random source, clock, input, cookie and history boundaries can be replaced independently in tests. Real-browser tests still verify native input, Canvas output and persistence reloads.

## Detailed model

DECOMPOSITION refines logical responsibilities and interfaces when established. Behavioral acceptance belongs to SPEC; file ownership belongs to layout. This architecture has no focused child documents.
