# Tools Context Snapshot (2026-02-06)

This document captures the current understanding of the legacy tools stack so future sessions can resume quickly.

## What was analyzed

- Directory structure of:
  - `legacy_full_investigate_strain/tools/`
  - `legacy_import/tools/`
- Main entrypoints (`run.py`) and representative high-impact scripts.
- Template files (`*.tpl`) and path/runtime assumptions.

## Core architecture (current)

- `artemis_utilities`
  - Orchestrates setup/run/cleanup over `DINTERFACES/`
  - Copies and runs helper scripts, creates/submits SBATCH jobs
  - Heavy coupling to local Slurm/HPC environment

- `vasp_utilities`
  - Generates local VASP inputs from POSCAR context
  - Pipeline: `POTCAR` -> `NBANDS/NELECT` -> `INCAR` -> `KPOINTS`
  - Uses local `common/POTCARS/` tree

- `task_utilities`
  - Actual analysis/generation logic lives in `scripts/`
  - `run.py` is currently empty
  - Contains key energetics, Bader, DOS/PDOS/LDOS, and prep scripts

- `id_utilities`
  - Atom identification by layers/projections from POSCAR/.vasp
  - Produces per-axis image and JSON outputs for atom targeting workflows

- External/vendor or special stacks
  - `bader`, `bader_src/`
  - `vtstscripts-1039/`
  - `progload/` (own source/build system)
  - `C-QM/` (orbital-focused utility scripts)

## Important findings

- Tool trees in `legacy_full` and `legacy_import` are effectively the same.
  - Notable exception: embedded git metadata under `legacy_full.../tools/progload/.git`.

- Multiple scripts assume fixed working-directory layout:
  - root includes `DINTERFACES/`
  - run outputs under `DRUN_MLP_MACE/` and `DRUN_DFT_VASP/`

- Template mismatch risk exists:
  - SBATCH templates use `{name}`
  - setup scripts in Artemis currently format templates with `lm`/`um`
  - this likely needs reconciliation before operational use

- `task_utilities/scripts/analyse/energies.py` appears central:
  - reads VASP energies from `vasprun.xml`/`OUTCAR`
  - computes standardized energy metrics
  - records setup provenance hashes

## Dependencies observed in active scripts

- Python packages: `ase`, `pymatgen`, `numpy`, `matplotlib`
- Platform/runtime: `sbatch` (Slurm), `rsync`
- VASP-side assets: pseudopotentials in local POTCAR tree

## Suggested immediate next jobs

Follow `execution_checklist.md` job IDs:

1. `T01` lock canonical tools source (recommend `legacy_full_investigate_strain/tools/`)
2. `T03` assign ownership/status across top-level tool groups
3. `T04` formalize interface contracts (inputs/outputs/assumptions)
4. `T08` create path-assumption audit list from already observed hard couplings

## Open questions to resolve in upcoming sessions

- Is `C-QM` in MP1 scope or archival only?
- Is `progload` required in active MP execution path?
- Which external binaries/scripts are mandatory vs optional for MP1.1/MP1.2?
