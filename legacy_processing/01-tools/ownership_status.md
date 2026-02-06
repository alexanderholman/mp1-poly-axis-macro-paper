# Ownership and Status Map

Date: 2026-02-06
Scope: top-level groups under canonical tools tree

Status key:
- `active`: expected in current MP1 workflow
- `optional`: useful but not required on critical path
- `external-vendor`: third-party payload
- `unknown`: role/scope needs confirmation

| Tool Group | Proposed Owner | Status | MP1 Scope Note |
|---|---|---|---|
| `artemis_utilities/` | Workflow/automation owner | active | HPC orchestration over `DINTERFACES` and `DRUN_*` |
| `vasp_utilities/` | VASP setup owner | active | Generates core VASP inputs (`POTCAR/INCAR/KPOINTS/NBANDS`) |
| `task_utilities/` | Analysis pipeline owner | active | Energetics/Bader/DOS scripts; no unified `run.py` yet |
| `id_utilities/` | Structure indexing owner | active | Atom/layer identification from POSCAR/.vasp |
| `progload/` | Legacy tools owner | optional | Standalone package; active-path need not yet confirmed |
| `C-QM/` | Electronic/orbital methods owner | unknown | Orbital tooling; MP1 necessity to be confirmed |
| `bader`, `bader_src/` | External dependency owner | external-vendor | Needed for Bader-based analyses |
| `vtstscripts-1039/` | External dependency owner | external-vendor | Transition-state tools; likely out of baseline MP1 critical path |

## Immediate follow-ups

- Confirm named human owners for each active group.
- Decide `C-QM` scope for MP1 (active vs reference-only).
- Confirm whether `progload` is required for any MP1 milestone-critical pipeline.
