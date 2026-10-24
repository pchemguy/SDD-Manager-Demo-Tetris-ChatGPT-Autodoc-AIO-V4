# SPEC review report

## Current gate

State: Ready for PLAN. Scope: SPEC and its three focused children, reviewed against accepted PROJECT/design. No whole-package QC, implementation, browser acceptance or installed-tool readiness is claimed. No unresolved confirmed findings; see resolved S-001 in Revision 1.

## Initial review

The specification owner compared every original requested capability and accepted brief decision with R1–R10, then checked design ownership, lifecycle, rejection/error behavior, timing, data formats and objective acceptance. Exact states:

- `PROJECT.md`: blob `717d6204a510d249c84b464e0f0e20604690bf69`.
- `ARCHITECTURE.md`: blob `e43684b16512d0d5b293a75ff6647bfbcf414d5e`.
- `DECOMPOSITION.md`: blob `f177558795d0ab9421fab4807cbaa307b07b6ef2`.
- `SPEC.md`: blob `8ed3b833d71fb7d45dcf9b6a8415452f3381f13a`.
- `spec/GAMEPLAY.md`: blob `0b03edbf61cdf0215a7a62151c793e82778b6f72`.
- `spec/ROTATION.md`: blob `36c8868c4c91ae4c5ae8cec6951e3fd4a3a68d53`.
- `spec/CONFIGURATION.md`: blob `edb8e1a81b3dbcf30411c10ea07a27565262aafb`.

| Coverage | Design / assessment |
| --- | --- |
| R1–R3 | C1/C3/C4 define spawn, movement, bounds, top-out, compaction, score and level; core ownership preserved. |
| R4 | C4/C5 compose chronological gravity/deadline events; explicit airborne, equal-time, pause, drop and invalid-time cases. |
| R5–R7 | C2/C3/C4/C9 share landing and source state; Hold restrictions, safe penetrator landing, reward/spend cap and white/settled distinction preserved. |
| R8–R9 | C6/C7 own exact codecs, independent precedence, explicit-default saving, omitted retention and recoverable per-port failure. |
| R10 | C8–C10 own input/focus, one loop, accessible controls, static delivery and both-browser application evidence. |

Manual conformance found no conflicting state owner or new product subsystem. Detailed scoring, controls, SRS candidates, time ordering and encodings fill precision explicitly left to SPEC by PROJECT. Classic-only behavior is identified for staged delivery without deleting the full target. End-state wording, local child links and Markdown spacing were checked. Acceptance specifies future evidence, not fabricated passing tests. Delivery counts do not apply to SPEC.

## Revision 1

S-001: R4 initially called the timer’s starting contact “valid grounding” and allowed expiry only at a visible-safe pose. An ordinary piece supported above the visible board could therefore wait forever instead of triggering R1 top-out. The specification owner clarified that first contact includes negative rows and a grounded negative-row deadline expiry ends the game without merging. This is the existing R1 failure behavior, not a change to the accepted first-grounding policy.

Revised `spec/GAMEPLAY.md` blob: `b40c9ad9380df9eb8f1856a8aa6abf481f9d8ce1`. Manual state-case review checked ordinary negative contact, ordinary visible contact, airborne expiry and penetrator transient overlap; only safe visible placements merge, ordinary top-out terminates, and penetration never locks while overlapping. Other reviewed inputs are unchanged. S-001 resolved; Ready for PLAN. No implementation test result is claimed.
