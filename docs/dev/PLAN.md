# Delivery plan

## Strategy and release boundaries

Deliver five useful functionality increments from the [complete specification](SPEC.md). Each phase preserves its predecessor’s playable behavior and has its own verification/integration/release boundary. A phase’s first milestone is not a substitute for its integrated phase exit. Infrastructure work is bounded enabling work within the classic phase, not a product release.

| Phase | Integrated outcome / version | Included scope and honest deferrals |
| --- | --- | --- |
| 1 — Playable classic | v0.1.0: keyboard game with movement, zero-offset rotation, gravity, full-interval lock delay, clearing/scoring/level, pause/restart and game over. | R1–R4/R10 classic subset; injected independent random source. Defer seven-bag, Hold, preview, kicks, ghost, hard drop, penetration and configuration. |
| 2 — Modern play assists | v0.2.0: seven-bag, Hold and next preview, SRS kicks, hard drop following delay, always-visible ghost. | R2/R4/R5/R6 ordinary modern subset; fixed defaults. Defer dynamic/hide visibility selection, alternate lock selections and all configuration to phase 4; penetration to phase 3. |
| 3 — Penetrator gameplay | v0.3.0: earn/spend up to three bonuses, activate safely, penetrate through occupied cells and preview/drop to deepest safe landing. | R7 plus R4/R5/R6 interactions; white active piece, ordinary settled colour and bonus symbols. Fixed default settings remain. |
| 4 — Session configuration | v0.4.0: all six controls, three ghost modes and both lock-policy selections, effective in the current page session. | R8 and remaining R4/R6 choices, including dynamic midline; deliberately no cookie/URL restore/save claims. |
| 5 — Persistent configuration | v1.0.0: independent URL/cookie/default restoration and live saves, failure status and complete target acceptance. | R9 with R1–R10 full regression; no remaining target-scope deferrals. |

Only a complete verified phase integrates into main. Preparation integration precedes the first phase branch. Activate only the eligible phase’s label, all milestones and task issues; future phases stay unprojected until their predecessors and authorization are established. Hosted tracking and release publication do not replace local acceptance evidence.

## Phase 1 — Playable classic

Predecessor: accepted design/specification and a verified integrated preparation baseline. The classic game requires no modern feature to be useful. Keep only interfaces needed for injected time/randomness and static presentation; avoid implementing a universal settings system or penetrator abstractions early.

| Milestone | Outcome / scope | Depends on | Exit evidence |
| --- | --- | --- | --- |
| 1.1 — Falling game foundation | Pinned tool/test environment, geometry and independent source, active-piece spawning/gravity/default lock, Canvas/controller with basic keyboard play. | Preparation baseline | A controllable falling piece obeys bounds/rotation/gravity; deterministic core checks and a representative real application run on both browsers establish the path. Setup failures resolved before dependent browser work. |
| 1.2 — Classic game rules | Simultaneous clear, score/level progression, chronological lock/timing boundaries, top-out/pause/restart lifecycle. | 1.1 | Seeded line-clear/score/level and timing/top-out cases pass; pause consumes no game time; restart uses one fresh session. |
| 1.3 — Classic delivery | Keyboard repeat/focus/visibility, static build/CI, integrated classic browser checks, player/developer guidance and release preparation. | 1.2 | Both-browser playable loop and visible board verified; isolated teardown, static serving and clean reproducible commands documented; release version/notes prepared. |
| 1.4 — Phase review | Cross-milestone code review, classic regressions, report and release readiness. | Closure of 1.1–1.3 | All included classic R1–R4/R10 outcomes and reports pass; no modern capability is claimed. |

## Phase 2 — Modern play assists

Predecessor: phase 1 integrated and released. Bag/Hold/preview form one piece-management increment; SRS/drop/ghost form a coherent placement-assistance increment. Deliver them together as a bounded modern-play release, keeping the independent penetrator mechanic and settings UI out.

| Milestone | Outcome / scope | Depends on | Exit evidence |
| --- | --- | --- | --- |
| 2.1 — Piece management | Seven-bag/queue, Hold lifecycle and native/canvas Hold-next presentation. | Phase 1 | Bag permutations/boundaries, queue observational peek, empty/swap Hold and once-per-lock permission verified. |
| 2.2 — Placement controls | SRS rotation, canonical normal landing/hard drop and retained delay under repeated drop. | 2.1 | All directed kick transitions, rejection order, normal blockers and hard-drop deadline behavior verified. |
| 2.3 — Ghost and modern integration | Always-shown ordinary ghost, status/focus for added widgets and integrated modern browser/release readiness. | 2.2 | Ghost matches drop; Hold/preview/drop/rotation coexist without baseline regressions on both browsers. |
| 2.4 — Phase review | Code review, complete modern regression and release evidence. | Closure of 2.1–2.3 | Ordinary modern R2/R4/R5/R6 outcomes pass with classic preservation. |

## Phase 3 — Penetrator gameplay

Predecessor: phase 2 integrated and released. Retain two delivery milestones: safe physics/resource state and its presentation/application acceptance. A third independent milestone would fragment one tightly coupled mechanic without another usable outcome. Both milestones remain bounded rather than absorbing configuration or persistence.

| Milestone | Outcome / scope | Depends on | Exit evidence |
| --- | --- | --- | --- |
| 3.1 — Penetrator rules | Deepest-safe landing and candidate safety, activation/bonuses/Hold exclusion, gravity/drop/lock integration. | Phase 2 | Intervening occupancy is traversed without deletion; no stranded/overlapping lock; spend/earn/cap/reset and inherited deadlines pass. |
| 3.2 — Penetrator experience | White active/ordinary settled pieces, ghost/bonus feedback, hostile-board regressions and browser/release readiness. | 3.1 | Same ghost/drop destination in cavities; stranding actions rejected; exact symbol counts and disabled Hold verified on both browsers. |
| 3.3 — Phase review | Code review, full penetrator/modern/classic regressions and report. | Closure of 3.1–3.2 | R7 and its R4–R6 interactions pass; release remains fixed-default. |

## Phase 4 — Session configuration

Predecessor: phase 3 integrated and released. Retain two delivery milestones separating schema/panel/state handoff from behavioral integration. This is a useful configurable game independently of persistence. Avoid cookie/history coupling until the session settings behavior is sound.

| Milestone | Outcome / scope | Depends on | Exit evidence |
| --- | --- | --- | --- |
| 4.1 — Settings panel | Shared typed six-setting schema/defaults, labelled controls and current-versus-next-piece application. | Phase 3 | Every control affects its declared field; focus safety and captured lock policies survive live edits and Hold exchanges. |
| 4.2 — Configurable gameplay | Dynamic ghost, disabled actions/retained Hold/preview queue invariants, both-lock-policy interaction matrix and browser/release readiness. | 4.1 | All R8 choices and remaining R4/R6 behavior pass for ordinary and penetrator pieces; settings survive restart within the page. |
| 4.3 — Phase review | Code review, session-configuration regressions and report. | Closure of 4.1–4.2 | All R8 behavior and predecessor guarantees pass; no persistence claim. |

## Phase 5 — Persistent configuration

Predecessor: phase 4 integrated and released. Retain two delivery milestones: deterministic source resolution and actual browser persistence/failure integration. Persistence is a distinct useful completion step with no additional gameplay scope.

| Milestone | Outcome / scope | Depends on | Exit evidence |
| --- | --- | --- | --- |
| 5.1 — Source resolution and saves | Exact codecs, independent precedence, URL-explicit cookie sync, cookie saves and selected-parameter history replacement. | Phase 4 | R9 mixed/invalid/default/omitted/duplicate cases, exact cookie names and unrelated URL/fragment preservation verified. |
| 5.2 — Persistent application | Independent port-failure status, real reload matrix, complete static delivery/user documentation and release preparation. | 5.1 | All six settings restore on both browsers; blocked persistence leaves gameplay usable; complete target and clean build pass. |
| 5.3 — Phase review | Final code review, R1–R10 acceptance, final report/TODO aggregation and release readiness. | Closure of 5.1–5.2 | Complete target passes; every unresolved/deferred issue has provenance, rationale and owner; no contract violation is deferred. |

## Common milestone and phase exits

Every delivery milestone requires whole-capability code review, appropriate deterministic/application tests, blocker repair, a committed milestone report and HANDOFF. TASKS gives a standalone review task only when that milestone has at least four delivery tasks and the phase has at least two delivery milestones; otherwise these obligations belong to its final delivery task. The dedicated final phase-review milestone always contains exactly one phase review/testing/report task and is excluded from delivery counts.

A delivery milestone closes only after its task issues, assigned review outcome and exits are verified. Phase review waits for all delivery milestones to close, then checks cross-milestone interactions, relevant predecessor regressions and release readiness. Reports retain Findings/Blockers and a TODO section; only noncritical code issues consistent with contracts may be deferred. The final phase review also aggregates final implementation evidence/TODOs. Task completion records and reports remain part of the implementation result, not a documentation-only substitute.

After phase review: verify the complete phase, explicitly merge into the recorded main parent, check the merged build/tests and included browser flows, publish/read back, then publish the phase’s version tag and GitHub release. Root RELEASE-NOTES.md supplies the exact finalized Markdown body for the annotated tag and GitHub release. Set package version consistently; verify notes cover actual delivered changes and limitations. Do not tag an unintegrated phase tip. Each published phase release must be read back before treating its release boundary as complete. A failed release/publication remains pending; do not invent success or force-push.

## Verification approach and coverage

| Layer | Required evidence |
| --- | --- |
| Pure core | Seeded commands/elapsed time, geometry/rotation fixtures, state invariants, timing boundaries, source consumption and penetrator conservation. |
| Adapter integration | Focus/repeat/visibility filtering, lifecycle teardown, schema/codec matrices and independently failing cookie/history ports. |
| Real application | Isolated Chromium and Firefox interactions, actual Canvas/preview/ghost/bonus inspection, pause/restart and phase-specific settings/reload flows. |
| Delivery | Type check, deterministic tests, production build, clean static serving, pinned lockfile/setup/CI and version/notes/tag/release readback. |

The first milestone establishes representative browser execution through the actual application path, following the repository’s diagnostic/fallback policy if provisioning fails. Browser-independent work can continue only where task dependencies allow; required browser evidence remains a blocker for its assigned exit. No benchmark or performance claim is inferred from these planned checks. Physical allocation belongs to layout; executable task IDs/progress belong to TASKS.
