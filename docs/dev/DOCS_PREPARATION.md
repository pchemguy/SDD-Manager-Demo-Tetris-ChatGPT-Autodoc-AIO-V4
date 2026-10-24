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
| DOCS-001 | Complete; published initialization and verified closed issue #1; retained four-file/provenance evidence below. |
| DOCS-002 | Human accepted proposal `261504b2e484ea91aff459d1da1931142fef728a`; settled brief published in `159eee3513de13c6a9eb9659bba9d671e792f55b`; issue #2 closed/read back. |
| DOCS-003 | Complete under autodoc preapproval; published architecture and issue #3 closed/read back. Later navigation-only link update travelled with DOCS-004. |
| DOCS-004 | Complete under autodoc preapproval; decomposition published and issue #4 closed/read back. |
| DOCS-005 | Complete under autodoc preapproval; SPEC/design QC and S-001 correction/recheck published; issue #5 closed/read back. See SPEC-REVIEW-REPORT Revision 1. |
| DOCS-006 | Complete under autodoc preapproval; strategy QC published and issue #6 closed/read back. |
| DOCS-007 | Complete under autodoc preapproval; layout/combined PLAN QC published and issue #7 closed/read back. See PLAN-REVIEW-REPORT Revision 1. |
| DOCS-008 | Scoped preapproval applies; TASKS conformance checks passed. Submit list/report, this evidence, HANDOFF and initial checkbox together, then publish/read back and close/read back issue #8. |
| DOCS-009 | Unchecked and unstarted; issue #9 and milestone #1 remain open at the autodoc stop. |

Exact per-document identities are retained in the task-qualified evidence below and adjacent reports. TASKS contains 43 unchecked product tasks across 5 phases and 17 milestones; 37 delivery tasks, 1 standalone milestone review and 5 phase reviews. No implementation phase is activated.

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

The original request governs complete target scope. PROJECT’s accepted decisions cover a 10×20 board, the occupied-cell midline rule, a non-resetting first-grounding deadline, penetrator safe-landing rejection, disabled Hold while penetrator is active, ordinary settled colours, bonus reset/earning, live-setting timing, invalid-value fallback, defaults, static TypeScript/Canvas direction, SRS and exclusions. The human approved PROJECT and these decisions after the published proposal was presented. No unrelated-project approvals were imported. Exact scoring/control/encoding contracts are owned by SPEC and its children.

## Pending transitions

DOCS-001–007 commits and issue closures are verified. DOCS-008 commit publication and issue #8 closure must be confirmed after this checkpoint; any failed/unknown effect blocks claiming the stop is settled. After successful readback, pause before DOCS-009. Do not perform package QC, merge preparation, close milestone #1, activate phase 1 or start implementation. Explicit advance can select the existing package-QC stage; it does not select an implementation range.

Preparation milestone #1 (`sdd-docs-main`) and all nine fixed-definition issues were created/verified before preparation writes. Product tracking projection remains unstarted. No game release is published; PLAN maps phase versions to 0.1.0, 0.2.0, 0.3.0, 0.4.0 and 1.0.0.

## DOCS-002 evidence

Human approved PROJECT and its gameplay/technical decisions in the latest message. Reviewed states: `docs/dev/PROJECT.md` blob `717d6204a510d249c84b464e0f0e20604690bf69`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-003 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/ARCHITECTURE.md` blob `dab4b7456d33c3a2cc298fd8fe661bf4f5923469`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-004 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/DECOMPOSITION.md` blob `f177558795d0ab9421fab4807cbaa307b07b6ef2`; `docs/dev/ARCHITECTURE.md` blob `e43684b16512d0d5b293a75ff6647bfbcf414d5e`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-005 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/SPEC.md` blob `8ed3b833d71fb7d45dcf9b6a8415452f3381f13a`; `docs/dev/spec/GAMEPLAY.md` blob `0b03edbf61cdf0215a7a62151c793e82778b6f72`; `docs/dev/spec/ROTATION.md` blob `36c8868c4c91ae4c5ae8cec6951e3fd4a3a68d53`; `docs/dev/spec/CONFIGURATION.md` blob `edb8e1a81b3dbcf30411c10ea07a27565262aafb`; `docs/dev/SPEC-REVIEW-REPORT.md` blob `ecaef7d3ec51e8f1559ba2605b9663f4d22f01c8`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## SPEC correction evidence

Before PLAN, review identified and resolved S-001 in SPEC-REVIEW-REPORT Revision 1: interval-policy top-out must terminate at expiry even when the grounded ordinary piece has negative rows. Updated GAMEPLAY blob `b40c9ad9380df9eb8f1856a8aa6abf481f9d8ce1`; accepted scope and DOCS-005 completion retained. This bounded correction is published before dependent planning.

## DOCS-006 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/PLAN.md` blob `9834156264b9bc85d492b7bce333316d5c7ea8da`; `docs/dev/PLAN-REVIEW-REPORT.md` blob `f9991ea056b06ea4e1c98d66905da77ac0ef39a7`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-007 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/layout.md` blob `432075c046a914f720866e17c1e0a3506d58aeed`; `docs/dev/PLAN-REVIEW-REPORT.md` blob `e8c51c97789135fd3444b73823e5850d2660ad85`; `AGENTS.md` blob `15717585b3eae2ec4740eb7f3a959850199238b3`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.

## DOCS-008 evidence

Scoped autodoc preapproval; upstream completion, publication and issue closure established. Reviewed states: `docs/dev/TASKS.md` blob `b4d3369cb2ecb3896f5e36bb3dc7835e1615d1c4`; `docs/dev/TASKS-REVIEW-REPORT.md` blob `d23182bf37c9950cc62008a735688c14e37c94bf`; `docs/dev/HANDOFF.md` blob `53d44019591de6a3cdfaa776ba2692672c35ffd7`; `README.md` blob `b15d546e2a78d17136ec9493c16f055e651e000b`; `AGENTS.md` blob `5d114bd2b2e5cf9078b97d13f681ba15c35c1539`. Local links, heading spacing, diff whitespace and content-boundary checks passed. Required technical QC is retained in the adjacent report when applicable. Publication and issue closure are confirmed by Git/provider readback after this commit.
