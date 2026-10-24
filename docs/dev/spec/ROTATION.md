# Piece geometry and rotation data

This document owns the geometry and SRS candidate order consumed by R1/R2/R7 in [GAMEPLAY](GAMEPLAY.md). Coordinates below are local integer occupied cells. Orientation labels are 0, R, 2 and L. Clockwise transitions follow that cycle; counterclockwise reverses it. No 180-degree input is required.

## Spawn cells and pivots

| Kind | Orientation 0 occupied (x,y) cells | Rotation pivot |
| --- | --- | --- |
| I | (0,1), (1,1), (2,1), (3,1) | (1.5,1.5) |
| J | (0,0), (0,1), (1,1), (2,1) | (1,1) |
| L | (2,0), (0,1), (1,1), (2,1) | (1,1) |
| O | (1,0), (2,0), (1,1), (2,1) | invariant cells |
| S | (1,0), (2,0), (0,1), (1,1) | (1,1) |
| T | (1,0), (0,1), (1,1), (2,1) | (1,1) |
| Z | (0,0), (1,0), (1,1), (2,1) | (1,1) |

For y increasing down, clockwise rotation about (px,py) maps a cell to (px−(y−py), py+(x−px)); repeated rotation derives each orientation. All resulting occupied coordinates are integers. O preserves occupied cells and pose for rotation input. It may advance an internal orientation label but cannot translate or affect timing.

## Kick candidates

Each transition tests (0,0) first, followed by the four offsets in its row, stopping at the first accepted pose. Offset data uses x right and y **up**: apply (dx,dy) as origin (x+dx,y−dy) in board coordinates. Test normal bounds/non-overlap or penetrator safe-landing validation according to active mode. If all five fail, preserve the pose. Baseline zero-offset rotation uses only the first candidate.

| Transition | J/L/S/T/Z remaining candidates |
| --- | --- |
| 0→R | (-1,0), (-1,1), (0,-2), (-1,-2) |
| R→0 | (1,0), (1,-1), (0,2), (1,2) |
| R→2 | (1,0), (1,-1), (0,2), (1,2) |
| 2→R | (-1,0), (-1,1), (0,-2), (-1,-2) |
| 2→L | (1,0), (1,1), (0,-2), (1,-2) |
| L→2 | (-1,0), (-1,-1), (0,2), (-1,2) |
| L→0 | (-1,0), (-1,-1), (0,2), (-1,2) |
| 0→L | (1,0), (1,1), (0,-2), (1,-2) |

| Transition | I remaining candidates |
| --- | --- |
| 0→R | (-2,0), (1,0), (-2,-1), (1,2) |
| R→0 | (2,0), (-1,0), (2,1), (-1,-2) |
| R→2 | (-1,0), (2,0), (-1,2), (2,-1) |
| 2→R | (1,0), (-2,0), (1,-2), (-2,1) |
| 2→L | (2,0), (-1,0), (2,1), (-1,-2) |
| L→2 | (-2,0), (1,0), (-2,-1), (1,2) |
| L→0 | (1,0), (-2,0), (1,-2), (-2,1) |
| 0→L | (-1,0), (2,0), (-1,2), (2,-1) |

Verify all directed transitions for ordinary pieces, first-success ordering, I versus J/L/S/T/Z differences, O invariance and all-candidate rejection. Penetrator fixtures must check the same ordering using its safe-future-landing predicate. These explicit tables govern the product; no undocumented guideline mechanics are implied.
