# First Fix Target: Artemis Root/Path Decoupling

Date: 2026-02-06
Target ID: `TOOLS-IMPL-01`

## Why this first

- Highest-impact path coupling is in `artemis_utilities` (`DINTERFACES`, `DRUN_*`, cwd assumptions).
- Fixing root resolution early reduces breakage risk for all job setup/run/cleanup workflows.
- This can be done as a non-destructive compatibility upgrade.

## Current pain points

- Scripts assume `Path.cwd()` is the orchestration root.
- `DINTERFACES/` and run roots are hard-coded.
- Wrong cwd can cause no-op scans, missed files, or destructive cleanup in unintended paths.

## Scope (Sprint 1)

In scope:
- Introduce explicit root argument for Artemis orchestration entrypoints.
- Centralize directory resolution (`root`, `interfaces_dir`, `run_dir_mace`, `run_dir_vasp`).
- Preserve current defaults when no explicit root is passed.

Out of scope:
- Changing scientific logic or file formats.
- Template placeholder repair (`{name}` mismatch) in this same sprint.
- Scheduler/account abstraction changes.

## Proposed interface change

- Add optional argument(s) to Artemis manager and worker scripts:
  - `--root <path>` default: `.` (current behavior)
  - `--interfaces-dir <path>` optional override; default `<root>/DINTERFACES`
  - `--run-root-mlp <path>` optional override; default `<root>/DRUN_MLP_MACE`
  - `--run-root-dft <path>` optional override; default `<root>/DRUN_DFT_VASP`

Compatibility rule:
- Existing invocations without these arguments continue to work exactly as before.

## Acceptance criteria

Functional:
- Running from repository root with no new arguments yields unchanged behavior.
- Running from outside repository with `--root <repo-root>` works for setup/run/cleanup command families.
- Submit commands place timestamped run trees under resolved run roots, not forced cwd defaults.

Safety:
- Cleanup commands refuse to operate if resolved interfaces dir is missing or points to filesystem root.
- Scripts print resolved paths before mutation/submission actions.

Quality:
- One shared path-resolver helper is used across Artemis scripts.
- No direct `Path.cwd()/os.getcwd()` root assumptions remain in Artemis setup/run/cleanup scripts except controlled defaults.

Verification checklist

- [ ] Baseline test: old invocation from expected cwd still works.
- [ ] Root-override test: run setup from unrelated cwd with `--root` and verify correct files are touched.
- [ ] Submit dry check: verify destination run tree path resolution.
- [ ] Cleanup guard test: invalid/missing interfaces path aborts safely.
- [ ] Regression check: command help includes new options and examples.

## Implementation notes for next session

- Start with manager `artemis_utilities/run.py`, then flow arguments into worker scripts.
- Create small shared helper module for path resolution to avoid divergence.
- Land this as one focused PR/commit before template placeholder fixes.
