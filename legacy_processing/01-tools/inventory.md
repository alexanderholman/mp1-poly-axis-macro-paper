# Tools Inventory

## Scope scanned

- `legacy_import/tools/`
- `legacy_full_investigate_strain/tools/`

Parity check result:

- Trees are functionally equivalent at top and file level.
- Observed difference: `legacy_full_investigate_strain/tools/progload/.git` exists (embedded git metadata).

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

## Entry-point overview

- `artemis_utilities/run.py`
  - Role: orchestration manager for setup/run/cleanup jobs across `DINTERFACES/`
  - Dependencies: `rsync`, `sbatch` (Slurm), template files in `artemis_utilities/common/`

- `vasp_utilities/run.py`
  - Role: local VASP input generation pipeline (`POTCAR`, `NBANDS/NELECT`, `INCAR`, `KPOINTS`)
  - Dependencies: local pseudopotential tree `vasp_utilities/common/POTCARS/`

- `task_utilities/run.py`
  - Role: intended manager entrypoint
  - Current state: empty; actual functionality is split under `task_utilities/scripts/`

- `id_utilities/run.py`
  - Role: layer-wise atom indexing/visualization from POSCAR/.vasp files
  - Outputs: per-axis PNG and JSON exports + printed atom ID/layer summaries

## High-value scripts already identified

- `task_utilities/scripts/analyse/energies.py`
  - Provenance-aware energy extraction (`vasprun.xml`/`OUTCAR`) with setup hashing
  - Likely source for existing `energies.json` artifacts in legacy calc trees

- `task_utilities/scripts/prepare/calc/generate_band_kpoints.py`
  - Band-structure KPOINTS generation for bulk/surface/interface classes

- `artemis_utilities/common/concat_artemis_data.py`
  - Interface metadata collation (`shift_vals.txt`, `struc_dat.txt`) into `poscar_data.json`

## Structural coupling observations

- Several tools assume execution from a root containing `DINTERFACES/`.
- Slurm submission scripts assume local scheduler availability and account/project settings.
- Job templates include `{name}` placeholders while setup scripts currently format with `{lm}`/`{um}`.


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
