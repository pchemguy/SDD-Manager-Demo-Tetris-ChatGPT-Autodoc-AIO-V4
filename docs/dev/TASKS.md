# Executable implementation tasks

The [delivery plan](PLAN.md), [specification](SPEC.md) and [physical layout](layout.md) govern this single project-wide task hierarchy. All tasks are initially unchecked; planned acceptance is not observed implementation.

Each delivery task includes meaningful test-first checks, implementation, module/API/user documentation as affected, acceptance verification and blocker repair. Preserve unrelated work. Commit exactly one task’s verified result, evidence and initial checkbox together; push/read back before advancing, then close/read back its issue.

A final delivery task marked “Milestone exit” owns the whole-milestone review/testing/report and HANDOFF in that same completion commit. Only milestone 1.1 has a standalone review task. Dedicated phase-review tasks require prior delivery milestone closure; they do not wait for their own review milestone to close.

Phase integration/release lifecycle follows PLAN after the phase review: explicit complete-phase main merge, merged checks, push/readback, finalized notes as annotated-tag/GitHub-release body and release readback. A partial requested range stops without integrating an incomplete phase.

## Phase 1 — Playable classic

- [ ] Phase 1 — Playable classic
    - [ ] Milestone 1.1 — Falling game foundation
        - [ ] T-001 — Establish pinned tooling and isolated test environments
            Scope: package/lockfile, TypeScript/Vite/Vitest/Playwright configuration, ignore rules and docs/DEVELOPMENT.md.
            Depends on: none; requires accepted published preparation integration and verified phase-1 activation.
            Evidence: R10: clean dependency install, type-check/test/build smoke path and isolated Chromium/Firefox provisioning/launch probes. Diagnose each failed browser independently under root policy; record versions, finite deadlines and limits. No personal/system browser use.
        - [ ] T-002 — Implement board geometry and zero-offset rotation
            Scope: src/core/types.ts, pieces.ts, board.ts, rotation.ts and focused unit fixtures.
            Depends on: T-001.
            Evidence: R1/R2, C1/C2: seven shapes/orientations, active bounds, overlap, O invariance and zero-offset rotation acceptance/rejection pass. Preserve an unambiguous y-down transform.
        - [ ] T-003 — Implement active-piece spawning and the falling rules core
            Scope: src/core/random.ts, game.ts, timing.ts and core tests.
            Depends on: T-002.
            Evidence: R1/R4 classic subset, C3–C5: injected independent source, spawn rejection, downward movement, default gravity/first-grounding deadline and read-only snapshot work without browser imports. Verify negative-row top-out and no invalid merge.
        - [ ] T-004 — Integrate a controllable falling-piece application
            Scope: index.html, src/main.ts, app.ts, ui/board.ts, browser/input.ts, browser/loop.ts, styles and application smoke tests.
            Depends on: T-003.
            Evidence: R1/R2/R4/R10: actual app paints a piece and handles basic play-area movement/rotation with visible bounds/gravity. Execute actual application smoke/render/teardown on both managed browsers; startup errors stop one owned loop.
        - [ ] T-005 — Review, test and report the falling foundation
            Scope: whole milestone implementation and docs/dev/reports/phases/1/1.1.md.
            Depends on: T-001, T-002, T-003, T-004.
            Evidence: Whole-capability code review, core tests and actual Chromium/Firefox smoke evidence pass; repair blockers, retain environment limits and TODOs, and refresh HANDOFF. This is a standalone milestone review, not delivery work.
            Report: `docs/dev/reports/phases/1/1.1.md`; include HANDOFF and TODO section with this task completion.
    - [ ] Milestone 1.2 — Classic game rules
        - [ ] T-006 — Implement lock merging, simultaneous clearing and scoring
            Scope: src/core/board.ts, game.ts and clear/score fixtures.
            Depends on: T-005.
            Evidence: R1/R3: four-cell safe merge, simultaneous row removal, compaction, 100/300/500/800 scoring, cumulative lines and level/speed progression pass; no partial state exposed.
        - [ ] T-007 — Complete chronological gravity and deadline boundary coverage
            Scope: src/core/timing.ts, game.ts and timing integration tests.
            Depends on: T-006.
            Evidence: R4: first grounding, movement/airborne nonreset, same-time events, large-step/subdivision equivalence, pause exclusion and delayed negative-row top-out pass. Correct uncovered boundary defects within the accepted contracts.
        - [ ] T-008 — Complete classic session lifecycle and feedback
            Scope: src/core/game.ts, app.ts, ui/panel.ts and lifecycle integration tests.
            Depends on: T-006, T-007.
            Evidence: R1/R3/R10: ready/start, pause/resume, top-out/game-over and restart preserve final feedback and create one fresh session without duplicate loop/listeners. Demonstrate complete scoring play before milestone closure.
            Milestone exit: review the complete 1.2 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/1/1.2.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 1.3 — Classic delivery
        - [ ] T-009 — Implement deterministic repeat and focus-safe keyboard lifecycle
            Scope: src/browser/input.ts, loop.ts, app.ts and browser adapter/e2e tests.
            Depends on: T-008.
            Evidence: R2/R10: declared repeat cadence, opposite-key arbitration, one-shot controls, form-focus exclusion, scroll prevention, blur/visibility pause and held-key clearing pass through native events.
        - [ ] T-010 — Establish production build and continuous verification
            Scope: build configs, .github/workflows/verify.yml, static artifact exclusions and docs/DEVELOPMENT.md.
            Depends on: T-009.
            Evidence: R10: clean reproducible type-check/tests/build/static serve and isolated browser runner are documented; production output excludes fixtures/harnesses/tokens/workflow docs. Run CI when available and report actual versus unobserved CI evidence.
        - [ ] T-011 — Verify and document the classic release candidate
            Scope: tests/e2e/, README.md, docs/CONTROLS.md, DEVELOPMENT.md, package version and RELEASE-NOTES.md.
            Depends on: T-009, T-010.
            Evidence: Phase 1 exits: both-browser move/rotate/clear/score/level/pause/game-over/restart, board raster inspection, two-context lifecycle and baseline regressions pass. Prepare 0.1.0 version/notes describing classic scope only; no tag/release before phase integration.
            Milestone exit: review the complete 1.3 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/1/1.3.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 1.4 — Phase review
        - [ ] T-012 — Review, test and report phase 1
            Scope: docs/dev/reports/phases/1/PHASE-REPORT.md, HANDOFF and complete phase delta.
            Depends on: T-005, T-008, T-011.
            Evidence: After milestones 1.1–1.3 close, review cross-milestone code and classic R1–R4/R10 exits; repair blockers and rerun affected checks. Confirm version/notes and merged-state check plan; release v0.1.0 only after verified integration/publication.
            Phase gate: all task issues, reports and delivery milestones 1.1, 1.2, 1.3 must be complete/closed before this task; then close its own review milestone after its issue.
            Report: `docs/dev/reports/phases/1/PHASE-REPORT.md`; include HANDOFF and TODO section in this completion commit.

## Phase 2 — Modern play assists

- [ ] Phase 2 — Modern play assists
    - [ ] Milestone 2.1 — Piece management
        - [ ] T-013 — Implement seven-bag and observational queue
            Scope: src/core/random.ts, game.ts and source fixtures.
            Depends on: T-012.
            Evidence: R5, C3/C4: each bag is a permutation, seeded order is deterministic, cross-bag repeats are legal, peek consumes nothing and ordinary spawn consumes one kind.
        - [ ] T-014 — Implement once-per-lock Hold transitions
            Scope: src/core/game.ts and Hold/source integration tests.
            Depends on: T-013.
            Evidence: R5: empty Hold consumes one source piece, nonempty swap consumes none, incoming pose/timing reset, once-per-lock gate survives exchange and failed spawn ends game without corrupting state.
        - [ ] T-015 — Present Hold and next-piece state
            Scope: src/ui/panel.ts, app.ts, styles and presentation/native-input tests.
            Depends on: T-013, T-014.
            Evidence: R5/R10: show one next kind and held kind with accessible labels; C/Shift trigger one Hold with no repeat, queue and timer snapshots match the core. Preserve classic input/focus behavior.
            Milestone exit: review the complete 2.1 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/2/2.1.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 2.2 — Placement controls
        - [ ] T-016 — Implement ordered SRS wall-kick rotation
            Scope: src/core/rotation.ts, placement.ts and directed-transition fixtures.
            Depends on: T-015.
            Evidence: R2 and ROTATION: all eight transitions for both kick tables, y-up offset conversion, first-success order, floor/wall cases, O invariance and total rejection pass.
        - [ ] T-017 — Implement canonical normal landing and hard drop
            Scope: src/core/placement.ts, game.ts, browser/input.ts and placement/drop tests.
            Depends on: T-016.
            Evidence: R6/R3: stop at first normal obstruction, use one returned landing, award two per moved row and zero for zero distance; Space acts once and follows default lock policy.
        - [ ] T-018 — Verify delayed hard drop with active-piece timing
            Scope: src/core/timing.ts, game.ts and drop/time integration tests.
            Depends on: T-016, T-017.
            Evidence: R4/R6: drop preserves gravity accumulation, begins first contact if needed and never replenishes a prior deadline; repeated/zero-distance drop, airborne expiry and subsequent spawn remain deterministic.
            Milestone exit: review the complete 2.2 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/2/2.2.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 2.3 — Ghost and modern integration
        - [ ] T-019 — Render the canonical ordinary ghost
            Scope: src/ui/board.ts, core snapshot projection and raster tests.
            Depends on: T-018.
            Evidence: R6: always-shown ghost matches normal hard-drop landing cell for cell, clips at board bounds and remains distinct from active/settled blocks. It never mutates physics.
        - [ ] T-020 — Complete modern control and preview presentation
            Scope: src/ui/panel.ts, board.ts, styles, controls help and UI tests.
            Depends on: T-019, T-015.
            Evidence: R5/R6/R10: Hold/next/ghost state updates consistently, focus/labels remain usable at 800×600, regular colours exclude white and form-target keys cannot trigger gameplay.
        - [ ] T-021 — Verify and document the modern release candidate
            Scope: tests/e2e/, modern integration fixtures, README/controls, version and notes.
            Depends on: T-018, T-019, T-020.
            Evidence: Phase 2 exits: both-browser bag/Hold/preview/kicks/drop/ghost interactions and predecessor regressions pass. Prepare 0.2.0 notes/version without claiming penetration or configuration.
            Milestone exit: review the complete 2.3 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/2/2.3.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 2.4 — Phase review
        - [ ] T-022 — Review, test and report phase 2
            Scope: docs/dev/reports/phases/2/PHASE-REPORT.md, HANDOFF and phase delta.
            Depends on: T-015, T-018, T-021.
            Evidence: After milestones 2.1–2.3 close, cross-review modern state/input/landing interactions, run relevant complete ordinary-game regressions and repair blockers. Verify v0.2.0 readiness for post-integration release.
            Phase gate: all task issues, reports and delivery milestones 2.1, 2.2, 2.3 must be complete/closed before this task; then close its own review milestone after its issue.
            Report: `docs/dev/reports/phases/2/PHASE-REPORT.md`; include HANDOFF and TODO section in this completion commit.

## Phase 3 — Penetrator gameplay

- [ ] Phase 3 — Penetrator gameplay
    - [ ] Milestone 3.1 — Penetrator rules
        - [ ] T-023 — Implement deepest-safe penetrator placement
            Scope: src/core/placement.ts, rotation.ts and adversarial board fixtures.
            Depends on: T-022.
            Evidence: R7, C1/C2: ignore intervening occupancy, choose greatest safe y and reject stranded candidates; allow safe overlapping translations/rotations within bounds using the same kick order.
        - [ ] T-024 — Implement activation, rewards and Hold exclusion
            Scope: src/core/game.ts, types.ts and bonus/Hold tests.
            Depends on: T-023.
            Evidence: R7/R5: zero-start/cap-three, exactly one spend, repeated activation no-op, four-line-only rewards including penetrator clears, restart reset and disabled activated Hold pass without source/timer side effects.
        - [ ] T-025 — Integrate penetrator descent, projection and lock timing
            Scope: src/core/game.ts, timing.ts, placement projection and combined tests.
            Depends on: T-023, T-024.
            Evidence: R4/R6/R7: gravity traverses obstacles to deepest safe placement; drop/ghost share it; activation on support preserves deadline, no overlap/negative-row penetrator lock, and no settled-cell deletion except clears.
            Milestone exit: review the complete 3.1 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/3/3.1.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 3.2 — Penetrator experience
        - [ ] T-026 — Present white active pieces and exact bonus feedback
            Scope: src/ui/board.ts, panel.ts, app.ts and rendering/status tests.
            Depends on: T-025.
            Evidence: R7/R10: active penetrator entirely white, settled kind ordinary colour, exact 0–3 bolt symbols and accessible count update on spend/earn, disabled Hold feedback and B one-shot input verified.
        - [ ] T-027 — Verify hostile-board penetrator invariants
            Scope: tests/fixtures/, tests/unit/core/ and tests/integration/ with scoped core repairs.
            Depends on: T-026.
            Evidence: R7/R4–R6: cavities below blockers, overlapping intermediate states, floor stranding, lateral/rotation rejection, delayed and repeated drop, bonus cap and reward-after-spend conserve cells and agree on landing.
        - [ ] T-028 — Verify and document the penetrator release candidate
            Scope: tests/e2e/, controls/README, version and RELEASE-NOTES.md.
            Depends on: T-026, T-027.
            Evidence: Both-browser activated white/ghost/drop/bonus/Hold behavior and classic/modern regressions pass. Prepare 0.3.0 fixed-default penetrator release with precise controls and limitations.
            Milestone exit: review the complete 3.2 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/3/3.2.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 3.3 — Phase review
        - [ ] T-029 — Review, test and report phase 3
            Scope: docs/dev/reports/phases/3/PHASE-REPORT.md, HANDOFF and phase delta.
            Depends on: T-025, T-028.
            Evidence: After 3.1–3.2 close, review mode/resource/placement interactions, required browser/core evidence and predecessor preservation. Repair blockers and verify v0.3.0 post-integration release readiness.
            Phase gate: all task issues, reports and delivery milestones 3.1, 3.2 must be complete/closed before this task; then close its own review milestone after its issue.
            Report: `docs/dev/reports/phases/3/PHASE-REPORT.md`; include HANDOFF and TODO section in this completion commit.

## Phase 4 — Session configuration

- [ ] Phase 4 — Session configuration
    - [ ] Milestone 4.1 — Settings panel
        - [ ] T-030 — Define the typed six-setting schema and defaults
            Scope: src/config/schema.ts, core-facing policy types and config unit tests.
            Depends on: T-029.
            Evidence: R8: exact six keys/enum values/defaults have one owner; validate selections without browser ports or reverse core-to-config dependencies. No persistence adapter is introduced here.
        - [ ] T-031 — Build labelled session configuration controls
            Scope: src/ui/panel.ts, styles, app.ts and native control tests.
            Depends on: T-030.
            Evidence: R8/R10: all six selections are keyboard accessible, reflect session values in every lifecycle state and cannot leak gameplay keys from focused controls.
        - [ ] T-032 — Apply immediate settings and next-piece policy capture
            Scope: src/app.ts, core/game.ts, UI status and state/config integration tests.
            Depends on: T-030, T-031.
            Evidence: R8: live availability/visibility update immediately; Hold contents and queue survive hides/toggles; lock selections snapshot on next normal/Hold incoming piece with pending-status text. Restart retains session settings.
            Milestone exit: review the complete 4.1 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/4/4.1.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 4.2 — Configurable gameplay
        - [ ] T-033 — Implement dynamic midline ghost visibility
            Scope: src/ui/board.ts or pure projection visibility helper and boundary/raster tests.
            Depends on: T-032.
            Evidence: R6/R8: hide/show/dynamic modes; top occupied row 9 hides and row 10 shows, including straddling shapes/empty box rows and penetrator projections; no landing changes.
        - [ ] T-034 — Complete selectable lock-policy and action interaction checks
            Scope: src/core/game.ts, timing.ts, controller and policy matrix tests.
            Depends on: T-033.
            Evidence: R4/R8: failed-down versus interval with follow/immediate drop; ordinary/penetrator, zero-distance repeated drop, disabled hard drop/Hold and live policy changes follow captured semantics. Reject unsupported selections without mutation.
        - [ ] T-035 — Verify and document the session-settings release candidate
            Scope: tests/e2e/, README/controls, version and notes.
            Depends on: T-033, T-034.
            Evidence: All six controls and policy interactions work on both browsers with readable 800×600 layout; predecessor regressions pass. Prepare 0.4.0 version/notes explicitly describing session-only settings.
            Milestone exit: review the complete 4.2 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/4/4.2.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 4.3 — Phase review
        - [ ] T-036 — Review, test and report phase 4
            Scope: docs/dev/reports/phases/4/PHASE-REPORT.md, HANDOFF and phase delta.
            Depends on: T-032, T-035.
            Evidence: After 4.1–4.2 close, review schema/control/core ownership and dynamic ghost/policy boundaries. Repair blockers, run required regressions and verify v0.4.0 post-integration release readiness; do not claim persistence.
            Phase gate: all task issues, reports and delivery milestones 4.1, 4.2 must be complete/closed before this task; then close its own review milestone after its issue.
            Report: `docs/dev/reports/phases/4/PHASE-REPORT.md`; include HANDOFF and TODO section in this completion commit.

## Phase 5 — Persistent configuration

- [ ] Phase 5 — Persistent configuration
    - [ ] Milestone 5.1 — Source resolution and saves
        - [ ] T-037 — Implement per-setting codecs and source precedence
            Scope: src/config/schema.ts, resolve.ts and source/encoding fixtures.
            Depends on: T-036.
            Evidence: R9: independent valid URL/cookie/default resolution, first-URL-duplicate rule, malformed/duplicate-cookie handling, unknown values and origins pass; no invalid value is saved.
        - [ ] T-038 — Implement cookie restoration and explicit-URL synchronization
            Scope: src/config/persistence.ts cookie port, app startup and fake-port tests.
            Depends on: T-037.
            Evidence: R9: exact-name cookie read/write, specified attributes, HTTP/HTTPS Secure rule, save/readback and explicit default saving pass. Omitted/invalid URL preserves saved values and gameplay starts with resolved settings.
        - [ ] T-039 — Implement selected-setting URL updates
            Scope: src/config/persistence.ts history/location port and integration tests.
            Depends on: T-037, T-038.
            Evidence: R9: interactive change replaces its duplicates once via history replacement, preserves other values/unknown parameters/path/fragment, never navigates and does not add omitted keys on startup. Cookie/history attempts are independent.
            Milestone exit: review the complete 5.1 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/5/5.1.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 5.2 — Persistent application
        - [ ] T-040 — Handle unavailable persistence without interrupting play
            Scope: src/config/persistence.ts, app.ts, ui/panel.ts and failure-injection tests.
            Depends on: T-039.
            Evidence: R9/R10: cookie throw/readback failure, history throw, unreadable URL and both-port failure retain valid session settings, attempt unaffected port and show concise mechanism-specific status without raw exceptions.
        - [ ] T-041 — Verify actual browser reload and mixed-source behavior
            Scope: tests/e2e/, isolated cookie/context fixtures and scoped adapter repairs.
            Depends on: T-040.
            Evidence: All six controls reload correctly in Chromium/Firefox; explicit default overwrites conflicting cookie, omitted URL retains nondefault cookie, invalid/mixed/duplicate inputs resolve independently and query/fragment survives. Confirm failures remain playable through actual app path.
        - [ ] T-042 — Verify full static delivery and final user guidance
            Scope: production artifact checks, README/CONTROLS/DEVELOPMENT, package version and RELEASE-NOTES.md.
            Depends on: T-040, T-041.
            Evidence: Full R1–R10 application/core regressions, clean build/static serve and artifact exclusions pass. Document exact supported controls/config encodings/setup and observed browser limits; prepare 1.0.0 notes/version covering the complete accepted target.
            Milestone exit: review the complete 5.2 capability and relevant dependencies, run required tests/browser checks and repair blockers; commit `docs/dev/reports/phases/5/5.2.md` plus HANDOFF and TODO section with this delivery result and initial checkbox.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-043 — Review, test and report the complete target
            Scope: docs/dev/reports/phases/5/PHASE-REPORT.md, reports/IMPLEMENTATION-REPORT.md, HANDOFF and phase delta.
            Depends on: T-039, T-042.
            Evidence: After 5.1–5.2 close, review complete target and all predecessor interactions, run required R1–R10 acceptance, repair blockers and aggregate unresolved/deferred TODOs with evidence/options/owners. Verify v1.0.0 readiness for post-integration release; report actual tag/release outcomes separately.
            Phase gate: all task issues, reports and delivery milestones 5.1, 5.2 must be complete/closed before this task; then close its own review milestone after its issue.
            Report: `docs/dev/reports/phases/5/PHASE-REPORT.md`; include HANDOFF and TODO section in this completion commit.
            Final report: `docs/dev/reports/IMPLEMENTATION-REPORT.md`, aggregating all milestone/phase findings and TODO provenance.
