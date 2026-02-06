# Interface Contracts (Detailed)

Date: 2026-02-06
Scope: active tool groups in canonical tree `legacy_full_investigate_strain/tools/`

## 1) `artemis_utilities`

- Entrypoint:
  - `legacy_full_investigate_strain/tools/artemis_utilities/run.py`
- Command surface:
  - Setup: `--setup-mlp-mace-jobs`, `--setup-dft-vasp-jobs`, `--setup-jobs`, `--setup-structure`, `--setup-all`
  - Run: `--run-concat`
  - Submit: `--submit-mlp-mace-jobs`, `--submit-dft-vasp-jobs`, `--submit-jobs`
  - Cleanup: `--cleanup-structure`, `--cleanup-mlp-mace-jobs`, `--cleanup-dft-vasp-jobs`, `--cleanup-jobs`, `--cleanup-all`
  - Aggregate: `--all` (current behavior does not submit; submit calls are commented)
- Required layout assumptions:
  - Run from root containing `DINTERFACES/`
  - Expects `artemis_utilities/common/` sibling files and templates
  - DFT setup expects `vasp_utilities/run.py` under same working root
- Inputs:
  - POSCAR directories under `DINTERFACES/`
  - `struc_dat.txt` in ancestor path chain
  - `shift_vals.txt` and `struc_dat.txt` at specific relative depths (DSHIFT/DSWAP)
- Outputs:
  - `SBATCH_MLP_MACE`, `run-mace.py`, `SBATCH_DFT_VASP` in POSCAR folders
  - `concat_artemis_data.py` and `poscar_data.json`
  - Timestamped run copies under `DRUN_MLP_MACE/` and `DRUN_DFT_VASP/`
- Runtime dependencies:
  - `python/python3`, `rsync`, `sbatch` (Slurm), module environment, `vasp_std`, MACE runtime
- Known contract risks:
  - SBATCH templates use `{name}` while setup scripts format with `lm`/`um`
  - DFT submit script includes one incorrect warning label (`SBATCH_MLP_MACE`)

## 2) `vasp_utilities`

- Entrypoint:
  - `legacy_full_investigate_strain/tools/vasp_utilities/run.py`
- Command surface:
  - `--generate-potcar`
  - `--calculate-nbands`
  - `--generate-incar`
  - `--generate-kpoints`
  - `--all` executes `potcar -> nbands -> incar -> kpoints`
- Required layout assumptions:
  - Execute inside calc directory containing `POSCAR`
  - POTCAR library expected in `vasp_utilities/common/POTCARS/`
- Inputs:
  - `POSCAR` (VASP5 species + counts assumptions)
  - `POTCAR` for NBANDS/NELECT stage
  - `INCAR.tpl` with placeholders `{NBANDS}` and `{NELECT}`
- Outputs:
  - `POTCAR`, `nbands.txt`, `nelect.txt`, `INCAR`, `KPOINTS`
- Runtime dependencies:
  - Python stdlib + `numpy`
- Known contract risks:
  - Potential POTCAR filename mismatch in library (`POTCAR` vs `PSCTR`) for non-Si species
  - `incar.py` silent default fallback (`48`) on missing/malformed `nbands.txt` or `nelect.txt`

## 3) `task_utilities`

- Entrypoints:
  - Intended manager: `legacy_full_investigate_strain/tools/task_utilities/run.py` (currently empty)
  - Actual script entrypoints in `task_utilities/scripts/`
- Functional contracts:
  - `scripts/analyse/energies.py`
    - Inputs: calc dirs/files (`vasprun.xml`, `OUTCAR`, `POSCAR/CONTCAR`, optionally INCAR/KPOINTS/POTCAR)
    - Output: structured JSON energy DB with setup hashes and setup_id
  - `scripts/analyse/bader*.py`
    - Inputs: POSCAR/CONTCAR + `ACF.dat`
    - Outputs: plots and transformed structures (`xyz`, `cif`)
  - `scripts/plot/*.py`
    - Inputs: VASP outputs (`vasprun.xml`, `DOSCAR`, `EIGENVAL`)
    - Outputs: DOS/PDOS/LDOS figures and data files
  - `scripts/prepare/calc/generate_band_kpoints.py`
    - Inputs: POSCAR + system type
    - Output: line-mode band `KPOINTS`
- Runtime dependencies:
  - `pymatgen`, `ase`, `numpy`, `matplotlib`, optional `mace`
- Known contract risks:
  - Missing unified CLI manager
  - Empty placeholder scripts in 2-axis/3-axis generate paths and prepare/calc relaxed/unrelaxed trees
  - Small script-level issues (argparse short-flag conflicts, brittle hardcoded scripts)

## 4) `id_utilities`

- Entrypoint:
  - `legacy_full_investigate_strain/tools/id_utilities/run.py`
- Contract:
  - Input: POSCAR-like structure file (`--input`)
  - Processing: layer assignment and per-axis projection labeling
  - Outputs: per-axis PNG + JSON layer exports and atom/layer console summary
- Runtime dependencies:
  - `ase`, `numpy`, `matplotlib`
