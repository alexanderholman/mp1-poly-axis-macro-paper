# MP1 Tools Migration Plan (Option 3)

Mode: build
Date: 2026-02-06

Option 3 = pip install from pinned SHA + dev submodule in macro repo.

## Goal

Extract maintainable, MP1-owned tooling from legacy trees using copy-based migration, while preserving:

- reproducibility for HPC execution (pip install pinned SHA)
- fast local iteration (submodule checkout)
- legacy as reference (no destructive moves)

## Architecture

- New public repo: `alexanderholman/mp1-tools` (based on `alexanderholman/template`)
- Installation strategy:
  - Macro repo + each micro-paper repo: `pip install git+...@<SHA>` (no floating branch refs)
  - Macro repo only: `vendor/mp1-tools` git submodule for development

## Non-negotiables (public repo hygiene)

- Do not vendor VASP POTCAR libraries (e.g. `common/POTCARS/`).
- Do not vendor opaque binaries by default (e.g. `bader`).
- Do not vendor VTST bundles by default.
- External dependencies must be opt-in and configured via PATH/env/config.

## Proposed `mp1-tools` repo layout

- `pyproject.toml`
- `src/mp1_tools/`
  - `id/` (from `id_utilities`)
  - `energies/` (from `task_utilities/scripts/analyse/energies.py`)
  - `vasp/` (from `vasp_utilities`, with `--potcar-dir` / env var)
  - `artemis/` (from `artemis_utilities`, including root/path decoupling)
  - `_shared/` (config loader, path utils, error codes)
- `tests/`
- `docs/`

Initial console commands:

- `mp1-id`
- `mp1-energies`

Later:

- `mp1-vasp`
- `mp1-artemis`

## Migration order (copy-based)

Phase 1 (low coupling, high value)

1. `id_utilities`
2. `task_utilities/scripts/analyse/energies.py`

Phase 2 (setup pipeline)

3. `vasp_utilities` (remove in-repo POTCAR coupling)

Phase 3 (orchestration)

4. `artemis_utilities` (add `--dry-run`; fix SBATCH placeholder mismatch as separate sprint)

## Integration policy

- Each consumer repo maintains a tiny lock file recording the pinned tools SHA:
  - `mp1_tools.lock`
- Micro-paper repos do not add tools submodules.
- Macro repo may carry `vendor/mp1-tools` submodule for dev only.

## Acceptance criteria

Phase 1 done when:

- `mp1-id` and `mp1-energies` install from pinned SHA and pass smoke tests.
- Output contracts are documented (I/O + schema keys).

Phase 2 done when:

- `mp1-vasp` matches legacy outputs given same inputs and explicit potcar config.
- Missing required inputs fail loudly (no silent defaults).

Phase 3 done when:

- `mp1-artemis` supports `--root` and path overrides from any cwd.
- Cleanup and submit have safety guards and a `--dry-run` mode.
- Template placeholder mismatch is resolved with regression coverage.
