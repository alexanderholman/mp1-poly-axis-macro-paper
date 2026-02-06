# Progload Scope Decision

Date: 2026-02-06
Decision ID: TOOLS-T07

## Decision

- `progload` is classified as **optional** for MP1 baseline execution.
- It remains available as an on-demand legacy tool, not a default dependency.

## Rationale

- MP1 critical path is currently centered on:
  - VASP setup and execution
  - Energetics extraction/provenance
  - Strain/Bader/DOS analyses
- These workflows are covered by `vasp_utilities`, `task_utilities`, `id_utilities`, and selected external dependencies.
- `progload` adds capability but is not required for baseline MP1 milestones.

## Promotion triggers (optional -> required)

- A milestone requires an analysis/output only available in Progload tools.
- Existing active pipeline cannot reproduce required outputs with acceptable confidence.
- A reproducibility audit flags Progload as part of historical reference outputs that must be regenerated.

## Fallback policy

- Keep a lightweight usage manifest if Progload is activated (tool version, build env, command invoked, output artifacts).
- Activate only per-task via explicit workflow note; do not add global runtime assumptions.
