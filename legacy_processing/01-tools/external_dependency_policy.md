# External Dependency Policy

Date: 2026-02-06
Scope: `bader` / `bader_src`, `vtstscripts-1039`

## 1) Bader (`bader`, `bader_src`)

- Status: external-vendor, active dependency for MP1 charge-analysis workflows.
- Version pinning policy:
  - Pin exact source snapshot and record source checksum.
  - Record binary checksum for the executable used in production runs.
- Installation policy:
  - Preferred: reproducible build from `bader_src` in controlled environment.
  - Allowed: prebuilt `bader` binary only when checksum-verified and architecture-matched.
- Licensing and citation:
  - Treat as GPL-derived external dependency; retain license attribution in docs.
  - Include Bader method citation in manuscript methods/checklist.
- MP1 scope:
  - In-scope for Bader analysis scripts under `task_utilities/scripts/analyse/bader*.py`.

## 2) VTST (`vtstscripts-1039`)

- Status: external-vendor, optional by default for MP1 baseline.
- Version pinning policy:
  - Pin bundled snapshot identity and maintain a manifest checksum for active scripts.
- Installation/activation policy:
  - Do not assume globally active PATH.
  - Activate through wrapper/module only for workflows that explicitly require VTST tools.
- Licensing and citation:
  - Verify upstream license terms before redistribution packaging.
  - Add citation requirements when VTST-enabled results enter manuscript outputs.
- MP1 scope:
  - Out of baseline critical path.
  - Enable only for transition-state/NEB-specific work.

## 3) Implementation checklist

- [ ] Record canonical Bader source + binary checksums in a version manifest.
- [ ] Document reproducible Bader build recipe.
- [ ] Add Bader citation requirement to paper release checklist.
- [ ] Record VTST snapshot manifest checksum.
- [ ] Document VTST activation method (wrapper/module) for opt-in usage.
- [ ] Verify and document VTST license terms before publication packaging.
