# Data Contract Plan

Date: 2026-02-06
Scope: tool outputs required for reproducible MP1 analysis

## 1) Priority outputs and contract anchors

- Energetics DB
  - Producer: `task_utilities/scripts/analyse/energies.py`
  - Contract anchor: JSON entries with calc path, energy metrics, and `vasp_setup` fingerprint fields
- Interface metadata aggregation
  - Producer: `artemis_utilities/common/concat_artemis_data.py`
  - Contract anchor: `poscar_data.json` with shift/structure metadata fields
- Bader post-processing outputs
  - Producers: `task_utilities/scripts/analyse/bader.py`, `bader_to_xyz.py`, `bader_to_cif.py`
  - Contract anchor: deterministic output naming and atom-count consistency checks
- Band/DOS artifacts
  - Producers: `task_utilities/scripts/prepare/calc/generate_band_kpoints.py`, `plot/*.py`
  - Contract anchor: explicit input file assumptions and output filename conventions

## 2) Provenance requirements

- Every analysis output should retain:
  - source calc path
  - source structure identifier (axis class + facet/orientation)
  - setup identity (hash/signature where available)
  - generation timestamp and tool version marker
- For energetics, preserve setup fingerprints (`INCAR`, `KPOINTS`, `POTCAR` hash lineage).

## 3) Normalization policy

- Use consistent unit labels in all output docs and tables.
- Avoid ad-hoc renamed output files; use declared naming conventions per script family.
- Ensure repeated runs with unchanged inputs produce stable schema shape.

## 4) Validation gates (planning)

- Schema gate: required keys present for each output class.
- Consistency gate: atom counts and structure IDs match between paired files.
- Provenance gate: calc path and setup identity present for publishable outputs.

## 5) Next implementation tasks

- [ ] Publish concrete JSON key schemas for `energies.json` and `poscar_data.json`.
- [ ] Define filename conventions for Bader and DOS output families.
- [ ] Add lightweight validators for schema/provenance checks.
