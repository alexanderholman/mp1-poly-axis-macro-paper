# Tools Inventory

## Scope scanned

- `legacy_import/tools/`
- `legacy_full_investigate_strain/tools/`

Both locations currently expose the same top-level tool groups.

## Top-level inventory

- `artemis_utilities/` - project-owned workflow helpers
- `id_utilities/` - atom identification utilities for POSCAR/.vasp structures
- `task_utilities/` - task orchestration helpers
- `vasp_utilities/` - VASP setup/run/postprocess helpers
- `progload/` - program loading/runtime utility layer
- `C-QM/` - domain utility package (needs ownership check)
- `bader` - external compiled binary (Bader analysis)
- `bader_src/` - source/build materials for Bader binary
- `vtstscripts-1039/` - external VTST scripts bundle

## Classification

- Project-maintained candidates:
  - `artemis_utilities/`
  - `id_utilities/` (structure atom indexing/selection from POSCAR/.vasp)
  - `task_utilities/`
  - `vasp_utilities/`
  - `progload/`
- External/vendor candidates:
  - `bader`, `bader_src/`
  - `vtstscripts-1039/`
- Unknown ownership (needs decision):
  - `C-QM/`

## Immediate risks

- Duplication across `legacy_import` and `legacy_full_investigate_strain` can cause drift.
- External binaries/scripts may be version-stale and undocumented.
- Some scripts may rely on hard-coded legacy absolute paths.
