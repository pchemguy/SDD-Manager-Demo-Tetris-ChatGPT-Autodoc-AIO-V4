# Main documentation preparation record

## Current control

- Mode: autodoc/onepass, selected by the user’s project request.
- Scope: complete Tetris target in the original request; no later scope passes.
- Approval basis: PROJECT approval was granted for proposal commit `261504b2e484ea91aff459d1da1931142fef728a`; its gameplay and technical decisions are accepted. ARCHITECTURE through TASKS checkpoints are preapproved by autodoc selection. No implementation range is selected.
- Tracking: enabled for preparation and implementation by root AGENTS.md. Every owned commit must be pushed and read back before progression.
- Reporting: Standard, following Explicit bootstrap.
- Next boundary: complete the preapproved dependent documents through DOCS-008. Stop after DOCS-008 before DOCS-009 unless explicitly advanced.

## Scope sequence

One pass covers a playable classic browser Tetris baseline, Hold, ghost, 7-bag, wall kicks, hard drop, selectable locking, dynamic ghost visibility, penetrator bonuses, six configuration controls and per-setting URL/cookie persistence. Deliver the simplest playable baseline first, then bounded useful increments. Publish a versioned release after each verified and integrated implementation phase, as requested; preparation itself is not a game release.

## Decisions and document evidence

| Task | Current evidence / decision basis |
| --- | --- |
| DOCS-001 | All four existing root files retained unchanged; verification below. Default provenance scaffold integrated and remotely verified. Task list and HANDOFF established with this completion. |
| DOCS-002 | PROJECT proposed at Git blob `83e393675474b174e2d52019ef90b7ee5ec5d0c6`; human acceptance required. Scope, seed preservation, proposal provenance and document-content boundaries reviewed. Independent read-only builder review found no scope/persistence contradictions. Clarified lateral/rotational penetration, activation on support and airborne deadline consequences; removed a preparation-process sentence. Local links, heading spacing, proposal identity and DOCS checkbox counts verified. No browser/runtime checks performed or needed for this brief. No dependent design started. |
| DOCS-003–008 | Not started; scoped autodoc preapproval applies after prerequisites. |
| DOCS-009 | Not started; excluded by current autodoc stop. |

## Initialization and current reset

- Original root-file presence: all four existed; none copied or modified. Full presence permits continuation without an initialization approval pause.
- Preservation: root blobs match the initial repository commit `330b621edce22921b13158109f70943ca953c5df`; SHA-256 values below.
- Manual provenance: default enabled. The packaged two-file scaffold was copied byte for byte on `design-docs/ai-logs`, based on `330b621edce22921b13158109f70943ca953c5df`. Seed `a6c30fa11b8d1d61973d1b7141b7a3476b32713d` published/read back. Explicit two-parent merge `3754d3227d0d53adf412d15ac0a5905c1e160f91` published/read back on main after the user approved that exact publication. No transcript was recorded.
- Automatic approval review initially rejected the default-branch push; remote main was checked unchanged. Draft-PR fallback failed with HTTP 403 through the connector and supplied token. User then approved publication of the existing merge; supervised push/readback succeeded with confirmed cleanup.
- Current reset: none.

- `AI_DISCLOSURE.md`: SHA-256 `09411dc61f4966efabe8e821f2270c768baf5b96f4fd4587eb5c05233de7ffea`.
- `SDD-MANAGER.md`: SHA-256 `ab12d665c8148cbf4fb8e190f265ccda667c4d47e8aae2304deed0bcf3d5a5bf`.
- `AGENTS.md`: SHA-256 `7ff5e248253507a77a39ddaf3e4b267655951758152a13680209c30b712345ea`.
- `SKILL_DISCOVERY_PROTOCOL.md`: SHA-256 `ae6fd000ed174d13706689148ab9ab20cd26ed5826ead72829679905bd44f5ec`.

## Accepted decisions for PROJECT

The original request governs complete target scope. PROJECT’s named proposals cover a 10×20 board, the occupied-cell midline rule, a non-resetting first-grounding deadline, penetrator safe-landing rejection, disabled Hold while penetrator is active, ordinary settled colours, bonus reset/earning, live-setting timing, invalid-value fallback, defaults, static TypeScript/Canvas direction, SRS and exclusions. The human approved PROJECT and these decisions after the published proposal was presented. No unrelated-project approvals were imported. Exact scoring/control/encoding details remain for SPEC.

## Pending transitions

Initialization commit `fff34cd315a39166c208589c69390dcf71b8c9f3` was published/read back; issue #1 closed as completed and read back. PROJECT proposal was published/read back. The human approved it; record acceptance and close/read back issue #2 before architecture. Main preparation milestone #1 (`sdd-docs-main`) and issues #1–#9 were created from bundled fixed definitions and all associations/content read back before any preparation write. All were open at that gate. Later hosted effects must be checked before replay.

## DOCS-002 evidence

Human approved PROJECT and its gameplay/technical decisions in the latest message. Reviewed states: `docs/dev/PROJECT.md` blob `717d6204a510d249c84b464e0f0e20604690bf69`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-003 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/ARCHITECTURE.md` blob `dab4b7456d33c3a2cc298fd8fe661bf4f5923469`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-004 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/DECOMPOSITION.md` blob `f177558795d0ab9421fab4807cbaa307b07b6ef2`; `docs/dev/ARCHITECTURE.md` blob `e43684b16512d0d5b293a75ff6647bfbcf414d5e`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-005 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/SPEC.md` blob `8ed3b833d71fb7d45dcf9b6a8415452f3381f13a`; `docs/dev/spec/GAMEPLAY.md` blob `0b03edbf61cdf0215a7a62151c793e82778b6f72`; `docs/dev/spec/ROTATION.md` blob `36c8868c4c91ae4c5ae8cec6951e3fd4a3a68d53`; `docs/dev/spec/CONFIGURATION.md` blob `edb8e1a81b3dbcf30411c10ea07a27565262aafb`; `docs/dev/SPEC-REVIEW-REPORT.md` blob `ecaef7d3ec51e8f1559ba2605b9663f4d22f01c8`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.
