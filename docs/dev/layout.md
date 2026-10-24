# Repository layout

## Ownership and status

This map allocates the [logical components](DECOMPOSITION.md) to physical homes consistent with [ARCHITECTURE](ARCHITECTURE.md) and [PLAN](PLAN.md). Root policies, bundled plugin and the development documents exist. Product source, tests, build configuration and reports listed below are intended locations; their listing does not claim implementation.

| Physical home | Logical owner / contents | Corresponding checks |
| --- | --- | --- |
| `src/core/types.ts` | C4 domain value/state/command/snapshot types, shared by pure core consumers. No browser imports. | Type checking and focused state/invariant tests. |
| `src/core/pieces.ts`, `src/core/board.ts` | C1 occupied transforms, bounds/overlap and row operations. | `tests/unit/core/` geometry/board fixtures. |
| `src/core/placement.ts`, `src/core/rotation.ts` | C2 canonical normal/penetrator landing, candidate safety and rotation/kick tables. | `tests/unit/core/` placement/rotation tests; shared board fixtures. |
| `src/core/random.ts` | C3 independent source, injected sequence seam, bag/queue. | `tests/unit/core/` source/consumption tests. |
| `src/core/game.ts` | C4 state transition orchestration, Hold/bonus/scoring/lifecycle. | `tests/unit/core/` transitions plus `tests/integration/` combined sessions. |
| `src/core/timing.ts` | C5 game-time event scheduling, gravity/deadline state helpers. | `tests/unit/core/` boundary/subdivision tests; integration with game transitions. |
| `src/config/schema.ts`, `src/config/resolve.ts` | C6 setting types/defaults/keys/codecs and pure source resolution. | `tests/unit/config/` complete value/source matrix. |
| `src/config/persistence.ts` | C7 cookie/history ports and coordination, explicit-URL sync and independent failures. | `tests/unit/config/` fake-port failures; `tests/e2e/` reload and cookie cases. |
| `src/browser/input.ts`, `src/browser/loop.ts` | C8 event filtering/repeat/focus/visibility and owned animation scheduling. | `tests/unit/browser/` adapter tests; native event/lifecycle e2e tests. |
| `src/ui/board.ts`, `src/ui/panel.ts`, `src/styles.css` | C9 Canvas painting, native controls/status/bonus/preview and desktop presentation. | Rendering assertions/screenshots under `tests/e2e/`; focused presentation tests where useful. |
| `src/app.ts`, `src/main.ts`, `index.html` | C10 controller/composition, initialization/error status and document entry. | `tests/integration/`, actual built application e2e path and static serving checks. |
| `tests/fixtures/` | Test-owned board/sequence/command/config fixtures. | Consumers load shared data; no duplicate production placement algorithm. |
| `package.json`, `package-lock.json`, `tsconfig.json`, `vite.config.ts`, `vitest.config.ts`, `playwright.config.ts` | Project tooling owner; versions/scripts, strict compilation, static bundling and runner/browser matrix. | Clean install/type-check/unit/integration/build/e2e commands established during implementation. |
| `.github/workflows/verify.yml` | CI verification owner; runs the same declared checks and isolated browser provisioning. | Actual workflow runs when available; local success alone does not prove CI. |

Keep imports within the pure core independent of `config`, `browser`, `ui` and Web APIs. `types.ts` may define the core-facing lock-policy value types; configuration maps to those types rather than creating a reverse core→config dependency. The controller composes settings and adapters. Production modules carry concise module/API documentation and own relevant failure semantics; do not create a generic utilities dumping ground.

## Tests and application fixtures

`tests/unit/` follows ownership areas rather than requiring one test file for each implementation file. `tests/integration/` exercises composed core/controller/config flows; `tests/e2e/` owns real application interaction, rendering and reload checks for Chromium and Firefox. Inject clock, random sequence and browser ports through declared construction seams. A test-only application harness may prepare deterministic board fixtures but must be excluded from the production build; do not add public debug URL mutation controls to the shipped game.

Use a project-owned absolute browser installation directory and isolated profiles/caches as required by root browser policy. Runner and installation share the same selected path. Keep binaries, traces, profiles and temporary downloads out of production assets and Git. Provision actual versions only after dependencies are pinned; never claim a planned path establishes a working browser.

## Documentation, reports and releases

| Home | Owner / role |
| --- | --- |
| `docs/dev/PROJECT.md`, `ARCHITECTURE.md`, `DECOMPOSITION.md` | Purpose and structural design. |
| `docs/dev/SPEC.md`, `docs/dev/spec/` | Canonical behavioral contracts and focused children. |
| `docs/dev/PLAN.md`, `layout.md`, `TASKS.md` | Delivery strategy, physical allocation and the single executable hierarchy. |
| `docs/dev/SPEC-REVIEW-REPORT.md`, `PLAN-REVIEW-REPORT.md`, `TASKS-REVIEW-REPORT.md` | Adjacent preparation QC; each covers its root/children. |
| `docs/dev/DOCS_TASKS.md`, `DOCS_PREPARATION.md`, `HANDOFF.md` | Preparation checklist, control/evidence and continuity snapshot. |
| `docs/dev/reports/phases/<phase-id>/<milestone-id>.md` | Delivery milestone code-review/testing/exit report, persisted by its assigned boundary task. |
| `docs/dev/reports/phases/<phase-id>/PHASE-REPORT.md` | Dedicated phase review/report task evidence and integration/release readiness. |
| `docs/dev/reports/IMPLEMENTATION-REPORT.md` | Final phase review’s complete target and TODO aggregation. |
| `README.md`, `docs/CONTROLS.md`, `docs/DEVELOPMENT.md` | Current delivered capabilities, player controls/settings and reproducible developer/setup/browser commands with evidence limits. |
| `RELEASE-NOTES.md` | Current finalized release body and annotated-tag message. Historical release bodies remain available through Git/tags/GitHub releases. |
| `docs/ai-logs/` | Existing manual provenance scaffold/records; not governing product requirements or routine review inputs. |
| `.agents/plugins/sdd-manager/` | Bundled workflow package, preserved as a dependency rather than a product module. |

## Generated and protected inputs

Exclude `node_modules/`, `dist/`, `coverage/`, `playwright-report/`, `test-results/` and project-local browser/runtime temporary state from tracking. Browser installations and caches belong to the test environment; distributable archives belong in an ignored `artifacts/` area before authorized release upload. Add actual ignore rules with the owning implementation setup. Root `*.tkn` exclusion is already established; never include tokens in source, reports, URL values, fixtures, archives or CI artifacts.

The production artifact is the static `dist/` output, without test harnesses, development docs, bundled workflow package or credentials. Report screenshots/traces may be attached as test evidence only after excluding user sessions and sensitive configuration. No personal browser data is required.

All C1–C10 responsibilities have a source/check home; each source area has one logical owner. Milestones can evolve a small set of related modules with their tests; integration tasks may span controller/presentation boundaries. No unresolved placement choice blocks task derivation. This document has no focused children.
