# CLI Consistency Plan

Date: 2026-02-06
Scope: `artemis_utilities`, `vasp_utilities`, `task_utilities`, `id_utilities`

## Target standard

- Command shape:
  - One executable per utility family with verb-first subcommands.
  - Kebab-case long options and consistent global flags.
- Required global flags:
  - `--help`, `--version`, `--verbose`, `--quiet`, `--format {text,json}`
- Error handling standard:
  - `0` success
  - `2` usage/validation error
  - `3` not-found
  - `4` external runtime dependency failure
  - `1` unexpected internal error
- Output discipline:
  - stdout for results, stderr for diagnostics/progress
  - stable JSON envelope in json mode

## Wrapper readiness criteria

- Command parity for in-scope MP1 operations.
- Standardized exit codes and error formatting.
- Consistent global flag support.
- Deterministic output in text/json mode.
- Compatibility path for legacy invocations (deprecation warnings allowed).
- Smoke tests for representative commands and one JSON golden output path.

## Staged rollout

1. Pilot wrapper conventions on `task_utilities` (currently lacks usable `run.py`).
2. Apply standard to `id_utilities` (small, focused interface).
3. Apply to `vasp_utilities` (core setup pipeline).
4. Apply to `artemis_utilities` (highest orchestration/path coupling).

## Immediate planning tasks

- [ ] Define shared CLI helper skeleton and error code enum.
- [ ] Build old->new command parity matrix for each utility.
- [ ] Select top 5 high-frequency commands per utility for smoke tests.
- [ ] Define deprecation window for legacy direct-script invocations.
