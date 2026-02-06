# Path Assumptions Audit

Date: 2026-02-06
Scope: canonical tools tree `legacy_full_investigate_strain/tools/`

## Summary

Most active scripts are tightly coupled to working-directory layout and fixed names (`DINTERFACES`, `DRUN_*`, POSCAR-family filenames). This is manageable for legacy execution but fragile for migration and reuse.

## A) High-impact assumptions (MP-critical)

### A1) `DINTERFACES/` rooted execution

- Found in:
  - `artemis_utilities/scripts/setup/*.py`
  - `artemis_utilities/scripts/run/*.py`
  - `artemis_utilities/scripts/cleanup/*.py`
- Pattern:
  - `base_dir = Path.cwd(); interface_dir = base_dir / "DINTERFACES"`
- Risk:
  - Running from alternate root breaks discovery of POSCAR jobs.

### A2) `DRUN_MLP_MACE/` and `DRUN_DFT_VASP/` output roots

- Found in:
  - `artemis_utilities/scripts/run/submit_mlp_mace_jobs.py`
  - `artemis_utilities/scripts/run/submit_dft_vasp_jobs.py`
- Pattern:
  - timestamped run trees copied from `DINTERFACES` before submission
- Risk:
  - hard-coded run roots complicate alternative run-management strategies.

### A3) Relative metadata paths (`shift_vals.txt`, `struc_dat.txt`)

- Found in:
  - `artemis_utilities/common/concat_artemis_data.py`
- Pattern:
  - DSHIFT/DSWAP-specific relative-depth traversal
- Risk:
  - path depth changes invalidate metadata collation.

### A4) VASP file naming assumptions in current directory

- Found in:
  - `vasp_utilities/scripts/generate/*.py`
  - `task_utilities/scripts/analyse/energies.py`
  - `task_utilities/scripts/plot/*.py`
- Pattern:
  - expects `POSCAR`, `POTCAR`, `INCAR`, `KPOINTS`, `vasprun.xml`, `OUTCAR`, etc.
- Risk:
  - non-standard naming or split calc layouts require wrappers/manual prep.

## B) Medium-impact assumptions

### B1) Tool sibling path coupling

- Found in:
  - `artemis_utilities/scripts/setup/jobs_dft_vasp.py`
- Pattern:
  - expects `<cwd>/vasp_utilities/run.py`
- Risk:
  - breaks if utilities are moved/packaged separately.

### B2) Pseudopotential tree placement

- Found in:
  - `vasp_utilities/scripts/generate/potcar.py`
- Pattern:
  - fixed path under `vasp_utilities/common/POTCARS/`
- Risk:
  - portability and licensing constraints for public or clean installs.

## C) Normalization strategy (planning)

1. Introduce explicit root/config argument for orchestration scripts.
2. Introduce resolver utility for structure metadata discovery (replace hard-coded relative depth rules).
3. Add consistent input-path arguments for scripts currently tied to `Path.cwd()`.
4. Externalize environment-specific values (Slurm account/partition/email/module stack).
5. Add a pseudopotential locator config instead of fixed in-tree assumptions.

## D) Priority queue (T08)

Priority 1 (do first):
- `artemis_utilities` root/path hard-coupling (`DINTERFACES`, `DRUN_*`)
- `concat_artemis_data.py` relative-depth assumptions

Priority 2:
- `jobs_dft_vasp.py` sibling utility path coupling
- `vasp_utilities` POTCAR source path coupling

Priority 3:
- script-by-script standardization of cwd-only assumptions in plotting/analysis helpers
