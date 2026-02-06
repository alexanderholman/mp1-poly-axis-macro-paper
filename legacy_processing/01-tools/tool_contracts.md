# Tool Contracts (Draft)

Status: draft baseline for context restoration and migration planning.

## artemis_utilities

- Primary entrypoint: `legacy_full_investigate_strain/tools/artemis_utilities/run.py`
- Current role:
  - setup jobs (`--setup-*`)
  - run concat scripts (`--run-concat`)
  - submit jobs (`--submit-*`)
  - cleanup generated helpers (`--cleanup-*`)
- Required layout assumptions:
  - run from a root containing `DINTERFACES/`
  - templates available under `artemis_utilities/common/`
- External runtime dependencies:
  - `rsync`
  - `sbatch` (Slurm)
- Main outputs:
  - SBATCH files in POSCAR folders
  - `run-mace.py` in POSCAR folders
  - `poscar_data.json` via concat workflow
  - copied run trees under `DRUN_*` for submission scripts

## vasp_utilities

- Primary entrypoint: `legacy_full_investigate_strain/tools/vasp_utilities/run.py`
- Current role:
  - generate `POTCAR` from POSCAR species
  - compute/write `nbands.txt`, `nelect.txt`
  - render `INCAR` from template
  - generate mesh `KPOINTS`
- Required layout assumptions:
  - run inside target calc directory containing POSCAR
  - pseudopotentials available in `vasp_utilities/common/POTCARS/`
- External runtime dependencies:
  - Python stdlib + `numpy`
- Main outputs:
  - `POTCAR`, `INCAR`, `KPOINTS`, `nbands.txt`, `nelect.txt`

## task_utilities

- Entrypoint status:
  - `legacy_full_investigate_strain/tools/task_utilities/run.py` is currently empty
  - scripts are invoked directly from `task_utilities/scripts/`
- High-value scripts:
  - `scripts/analyse/energies.py` (energy extraction + provenance setup hash)
  - `scripts/analyse/bader*.py`
  - `scripts/plot/dos.py`, `scripts/plot/pdos.py`, `scripts/plot/ldos.py`
  - `scripts/prepare/calc/generate_band_kpoints.py`
- External runtime dependencies:
  - `pymatgen`, `ase`, `numpy`, `matplotlib`
- Current limitations:
  - no unified CLI manager
  - uneven script maturity (some placeholders like `generate/interface/2-axis.py`)

## id_utilities

- Primary entrypoint: `legacy_full_investigate_strain/tools/id_utilities/run.py`
- Current role:
  - assign atom IDs and layer grouping from POSCAR/.vasp
  - generate layer plots and JSON exports along axes a/b/c
- Inputs:
  - POSCAR-like structure file (`--input`)
- Outputs:
  - `<input_stem>_layers/{a,b,c}/*.png`
  - `<input_stem>_layers/{a,b,c}/*.json`
  - console atom/layer summaries

## C-QM

- Entrypoints:
  - `C-QM/c_atomic_orbitals_PENB.py`
  - `C-QM/c_orbital_tool.py`
  - `C-QM/load_orbital.py`
- Current role:
  - orbital dataset generation/inspection/export (npz-driven)
- Scope status:
  - ownership and MP1 relevance not yet finalized

## progload

- Location: `legacy_full_investigate_strain/tools/progload/`
- Characteristics:
  - standalone Fortran/shell package with own source/build layout
  - embedded `.git/` metadata in legacy_full copy
- Scope status:
  - required-vs-optional for MP1 remains to be decided

## bader / bader_src

- Current role:
  - binary + source for Bader charge analysis
- Integration:
  - consumed by analysis helpers in `task_utilities/scripts/analyse/`
- Migration status:
  - versioning/licensing/install policy still required

## vtstscripts-1039

- Current role:
  - VTST bundle (NEB/dimer/related utilities)
- Scope status:
  - likely optional for core MP1 baseline unless transition-state workflows are activated
