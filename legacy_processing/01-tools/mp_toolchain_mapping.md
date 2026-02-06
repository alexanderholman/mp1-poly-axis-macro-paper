# MP Toolchain Mapping

Date: 2026-02-06
Scope: required vs optional tool groups across MP1.1-MP1.9

Legend:
- Required: needed to execute/verify stage outputs
- Optional: useful extensions, not stage-blocking

## MP1.1 Sigma3 {112} reproduction

- Required:
  - `vasp_utilities`
  - `task_utilities` (`analyse/energies.py` minimum)
- Optional:
  - `id_utilities`
  - `task_utilities` plotting helpers
  - `bader` stack (if charge comparison included)

## MP1.2 Sigma3 {111} reproduction

- Required:
  - `vasp_utilities`
  - `task_utilities` (`analyse/energies.py` minimum)
- Optional:
  - `id_utilities`
  - Bader/DOS scripts as needed for extended comparison

## MP1.3 Protocol transfer (Supers settings)

- Required:
  - `vasp_utilities`
  - configuration/template governance docs
- Optional:
  - `artemis_utilities` orchestration wrappers

## MP1.4 Single-axis 111/112 under Protocol S

- Required:
  - `vasp_utilities`
  - `task_utilities` (`energies`, strain/electronic prep scripts)
- Optional:
  - `artemis_utilities` (if using legacy DINTERFACES orchestration)
  - `id_utilities`
  - `bader` stack and DOS plotting for extended outputs

## MP1.5 Dual-axis model comparison

- Required:
  - `vasp_utilities`
  - `task_utilities` (`energies`, selected generate/prepare scripts)
- Optional:
  - `id_utilities`
  - `artemis_utilities`
  - Bader/DOS stacks for deeper interpretation

## MP1.6 Three-axis extension

- Required:
  - `vasp_utilities`
  - `task_utilities`
- Optional:
  - `id_utilities`
  - `artemis_utilities`

## MP1.7 Defect campaign

- Required:
  - `vasp_utilities`
  - `task_utilities`
  - `bader` stack (for charge-analysis branch)
- Optional:
  - `id_utilities`
  - DOS/PDOS extensions depending on defect depth

## MP1.8 Synthesis/manuscript assembly

- Required:
  - analysis outputs and provenance contracts from prior MPs
- Optional:
  - additional plotting scripts for publication formatting

## MP1.9 Electron microscopy structure validation

- Required:
  - structure identification/indexing (`id_utilities`)
  - geometry/energetics evidence from prior MPs (`task_utilities` outputs)
- Optional:
  - additional visualization tooling

## Minimal reproducible stack

For MP1.1 + MP1.2 baseline:

- `vasp_utilities`
- `task_utilities/scripts/analyse/energies.py`
- optional local wrappers for plotting/reporting

For expanded MP1.5/1.6/1.7:

- add `id_utilities`
- add Bader runtime (`bader` + converters)
- add selected DOS/PDOS scripts
