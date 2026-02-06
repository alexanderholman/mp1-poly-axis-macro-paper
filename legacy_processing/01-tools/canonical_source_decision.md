# Canonical Source Decision

Date: 2026-02-06
Decision ID: TOOLS-T01

## Decision

- Canonical source for active tools processing is:
  - `legacy_full_investigate_strain/tools/`
- Reference-only mirror is:
  - `legacy_import/tools/`

## Rationale

- Functional parity is effectively present between both trees.
- `legacy_full_investigate_strain` aligns with the currently active structure/calc data context used in MP1 work.
- Using one canonical source avoids dual-edit drift and simplifies future migration tasks.

## Validation notes

- A recursive parity check found no substantive file-level differences in tool content.
- Noted exception: embedded git metadata at `legacy_full_investigate_strain/tools/progload/.git`.
- Therefore, parity is treated as "content equivalent with metadata divergence".

## Operational rule

- All future tool analysis and migration jobs use canonical paths from `legacy_full_investigate_strain/tools/`.
- `legacy_import/tools/` is used only for spot verification and historical reference.
