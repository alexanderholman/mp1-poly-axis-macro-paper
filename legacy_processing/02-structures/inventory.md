# Structures Inventory

## Scope scanned

- `legacy_full_investigate_strain/data/structures/`

## Top-level structure groups

- `bulks/`
  - `Si8/`
- `surfaces/`
  - includes paired orientations (e.g., `110`, `-1-10`, `111`, `-1-1-1`, `112`, `-1-1-2`)
- `interfaces/`
  - `1-axis/` (`110`, `111`, `112`)
  - `2-axis/` (`110-111`, `110-112`, `111-112`, plus `__archive__`)
  - `3-axis/` (`110-111-112`)
- `surface-terminations/`
  - `terminations/` and `terminations_bak/` by Miller family (`110`, `111`, `112`)

## Legacy conventions observed

- Axis complexity is encoded in directory names (`1-axis`, `2-axis`, `3-axis`).
- Orientation/facet combinations are encoded in slug-like directory IDs (`111-112`, `110-111-112`).
- Calculation payloads commonly appear under `CALC/` subtrees.
- Variant/archive patterns exist (`__archive__`, `__variations__`, `__replications__`, `__config__`).

## Recreate-worthy structural pattern

The legacy directory pattern appears intentional and should be reproducible in the migrated system:

- Material group (`bulks`, `surfaces`, `interfaces`)
- Axis complexity group (`1-axis`, `2-axis`, `3-axis` for interfaces)
- Orientation/facet family (e.g., `111`, `111-112`, `110-111-112`)
- Structure metadata and variants (`__config__`, `__variations__`, `__archive__`)
- Calculation containers (`CALC/VASP`, `CALC/MACE` where applicable)

## Immediate risks

- Multiple “special” subtrees (`__archive__`, `terminations_bak`) may mix active and historical assets.
- Orientation naming conventions include negative-index string forms that need normalization rules.
- Some paths may be consumed by tooling assumptions; re-layout without mapping can break scripts.
