# Command Matrix

Date: 2026-02-06
Scope: canonical tool tree `legacy_full_investigate_strain/tools/`

Purpose: single-sheet operational reference for safe execution and troubleshooting.

## `artemis_utilities`

Entrypoint: `legacy_full_investigate_strain/tools/artemis_utilities/run.py`

| Command | Inputs | Outputs | Dependencies | Common failure modes |
|---|---|---|---|---|
| `--setup-mlp-mace-jobs` | `DINTERFACES/**/POSCAR`, `common/SBATCH_MLP_MACE.tpl`, `common/run-mace.py` | `SBATCH_MLP_MACE`, `run-mace.py` per POSCAR dir | Python, filesystem layout rooted at `DINTERFACES` | template placeholder mismatch (`{name}` vs formatter args), missing template files |
| `--setup-dft-vasp-jobs` | `DINTERFACES/**/POSCAR`, `common/SBATCH_DFT_VASP.tpl`, `vasp_utilities/run.py` | `SBATCH_DFT_VASP` + generated VASP inputs via `vasp_utilities` | Python, sibling `vasp_utilities`, POSCAR-ready folders | wrong cwd, missing `vasp_utilities/run.py`, POTCAR/INCAR generation failures |
| `--setup-structure` | `DINTERFACES/**/POSCAR`, `common/concat_artemis_data.py` | copied `concat_artemis_data.py` | Python | missing `DINTERFACES` tree |
| `--run-concat` | copied `concat_artemis_data.py`, `shift_vals.txt`, `struc_dat.txt` (relative paths) | `poscar_data.json` per POSCAR dir | Python3, strict relative path assumptions | DSHIFT/DSWAP depth mismatch, missing metadata files |
| `--submit-mlp-mace-jobs` | prepared `DINTERFACES` tree + SBATCH files | copied run tree `DRUN_MLP_MACE/<timestamp>/`, submitted jobs | `rsync`, `sbatch`, scheduler access | missing `sbatch`, stale outputs causing skipped submits |
| `--submit-dft-vasp-jobs` | prepared `DINTERFACES` tree + SBATCH files | copied run tree `DRUN_DFT_VASP/<timestamp>/`, submitted jobs | `rsync`, `sbatch`, scheduler access | same as above; one incorrect warning label in script |
| `--cleanup-*` | `DINTERFACES/**` generated files | removes setup/concat artifacts | Python | accidental cleanup from wrong cwd |
| `--all` | same as setup+run sequence | cleanup + setup + concat (submit currently commented) | same as above | behavior differs from help text (no submit) |

## `vasp_utilities`

Entrypoint: `legacy_full_investigate_strain/tools/vasp_utilities/run.py`

| Command | Inputs | Outputs | Dependencies | Common failure modes |
|---|---|---|---|---|
| `--generate-potcar` | `POSCAR`, `common/POTCARS/<species>/...` | `POTCAR` | Python, local POTCAR tree | species lookup mismatch (`POTCAR` vs `PSCTR` naming), POSCAR format assumptions |
| `--calculate-nbands` | `POSCAR`, `POTCAR` | `nbands.txt`, `nelect.txt` | Python | missing/invalid POTCAR ZVAL, malformed POSCAR counts |
| `--generate-incar` | `POSCAR`, `nbands.txt`, `nelect.txt`, `common/INCAR.tpl` | `INCAR` | Python | silent fallback values if band/electron files missing/malformed |
| `--generate-kpoints` | `POSCAR` | `KPOINTS` | Python, `numpy` | invalid cell vectors/scale parsing, wrong kspacing assumptions |
| `--all` | above in order | full local VASP setup files | same as above | first-stage POTCAR failures cascade to later stages |

## `task_utilities`

Entrypoint status: `legacy_full_investigate_strain/tools/task_utilities/run.py` is empty. Use script-level commands directly.

| Script command (direct) | Inputs | Outputs | Dependencies | Common failure modes |
|---|---|---|---|---|
| `scripts/analyse/energies.py ...` | calc files/dirs (`vasprun.xml`, `OUTCAR`, POSCAR/CONTCAR) | structured `energies.json` with setup fingerprints | `pymatgen`, Python | missing calc artifacts, mixed path layouts |
| `scripts/analyse/bader.py ...` | `ACF.dat` | histogram plot and summary | `numpy`, `matplotlib` | missing/invalid ACF format |
| `scripts/analyse/bader_to_xyz.py ...` | POSCAR + `ACF.dat` | charge-tagged XYZ | `numpy` | atom count mismatch POSCAR vs ACF |
| `scripts/analyse/bader_to_cif.py ...` | POSCAR + `ACF.dat` | charge-tagged CIF | `numpy` | non-orthogonal-cell simplification risk |
| `scripts/prepare/calc/generate_band_kpoints.py ...` | POSCAR + `--system-type` | line-mode `KPOINTS` | `pymatgen` | unsupported system type, missing POSCAR |
| `scripts/plot/pdos.py ...` | `vasprun.xml` or `DOSCAR` | PDOS plots + ASCII exports | `pymatgen`, `numpy`, `matplotlib` | parser/runtime dependency issues |

## `id_utilities`

Entrypoint: `legacy_full_investigate_strain/tools/id_utilities/run.py`

| Command | Inputs | Outputs | Dependencies | Common failure modes |
|---|---|---|---|---|
| `python run.py --input <POSCAR/.vasp> [options]` | structure file, optional range/plot args | `<stem>_layers/{a,b,c}` PNG + JSON exports | `ase`, `numpy`, `matplotlib` | missing input file, plotting backend issues |

## Execution guardrails

- Always confirm working directory expectations before running `artemis_utilities` commands.
- Prefer dry-run style checks (`ls`, file existence) before submit/cleanup commands.
- For `task_utilities`, treat script-level entrypoints as canonical until a unified `run.py` exists.
- Keep scheduler-dependent commands isolated from local-only analysis commands.
