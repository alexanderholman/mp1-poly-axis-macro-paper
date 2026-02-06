# Tools Migration Execution Checklist

Purpose: track tools migration in small, restart-safe jobs so work can pause/resume cleanly.

Rule: this file is planning/tracking only. No code changes are required to complete checklist updates.

---

## 0) Session control (do this every session)

- [ ] Confirm canonical working repo path.
- [ ] Confirm current objective (which job ID below is active).
- [ ] Record any blockers discovered since last session.
- [ ] End session by updating status for active job and next job.

---

## 1) Canonical source lock

### Job T01 - Choose canonical tools tree
- [x] Decide canonical source: `legacy_full_investigate_strain/tools/` (recommended) or `legacy_import/tools/`.
- [x] Record rationale and decision date.
- [x] Mark non-canonical tree as reference-only in docs.

### Job T02 - Verify parity against reference tree
- [x] Compare top-level directories in canonical vs reference tree.
- [x] Record any mismatches (missing dirs/files, version differences).
- [x] Decide whether mismatches are intentional or need reconciliation.

---

## 2) Ownership and status mapping

### Job T03 - Ownership table (top-level)
- [x] Assign owner/status for each top-level tool group:
  - `artemis_utilities`
  - `vasp_utilities`
  - `task_utilities`
  - `id_utilities`
  - `progload`
  - `C-QM`
  - `bader` / `bader_src`
  - `vtstscripts-1039`
- [x] Status values: active, optional, deprecated, external-vendor, unknown.

### Job T04 - Interface contract inventory
- [x] For each active group, document entrypoints and expected inputs/outputs.
- [x] Note required runtime dependencies (ASE, pymatgen, Slurm, rsync, etc.).
- [x] Note required directory assumptions (e.g., `DINTERFACES/`).

---

## 3) External dependency policy

### Job T05 - Bader policy
- [x] Record preferred installation route (binary vs build from `bader_src`).
- [x] Record version pinning/checksum expectations.
- [x] Record license/citation requirements.

### Job T06 - VTST policy
- [x] Record expected VTST version and source.
- [x] Record activation method (PATH/module/wrapper).
- [x] Record scope for MP1 (which scripts are in-scope vs out-of-scope).

### Job T07 - Progload policy
- [x] Decide whether Progload is required for MP1 active workflow.
- [x] If required, document build and runtime procedure.
- [x] If optional/deprecated, mark as reference-only.

---

## 4) Workflow hardening plan (documentation only in this phase)

### Job T08 - Path assumptions audit plan
- [x] List scripts with hard-coded path assumptions.
- [x] Define future normalization strategy (config/env/CLI arguments).
- [x] Prioritize fixes by MP impact.

### Job T09 - CLI consistency plan
- [x] Define target CLI style for managed utilities.
- [x] Identify missing/empty CLI entrypoints (e.g., `task_utilities/run.py`).
- [x] Define acceptance criteria for "ready" CLI wrappers.

### Job T10 - Data contract plan
- [x] Define stable schema references for key outputs (`energies.json`, Bader exports, DOS outputs).
- [x] Define provenance requirements (input hashes/setup IDs).
- [x] Define where schema docs will live.

---

## 5) MP mapping and minimum viable toolchain

### Job T11 - MP critical path mapping
- [x] Map exact required tools to each MP stage:
  - MP1.1
  - MP1.2
  - MP1.3
  - MP1.4
  - MP1.5
  - MP1.6
  - MP1.7
  - MP1.8
  - MP1.9
- [x] Mark each dependency as required vs optional.

### Job T12 - Minimal reproducible stack definition
- [x] Define smallest tool subset needed to execute MP1.1 and MP1.2 end-to-end.
- [x] Define extension subset needed for MP1.5/MP1.6/MP1.7.
- [x] Define acceptance checklist for "toolchain ready".

---

## 6) Risks and issue handling

### Known risks to track
- [ ] Template/format placeholder mismatches in job scripts and templates.
- [ ] HPC scheduler/account assumptions embedded in SBATCH templates.
- [ ] Public-repo licensing constraints for POTCAR/binaries.
- [ ] Drift risk from duplicated legacy trees.

### Blocker log
- [ ] None currently.

Use this format for new blockers:
- [ ] `BLOCKER-ID`: short title
  - Impact:
  - Detected in:
  - Temporary workaround:
  - Resolution owner:

---

## 7) Handoff template (copy/paste at end of a session)

Session date:

Completed jobs:
- 

In-progress job:
- 

Next job:
- 

Blockers:
- 

Notes:
- 

---

## Progress log

### 2026-02-06

- Completed documentation-only analysis pass over tool structure and key entry scripts.
- Added `context_snapshot_2026-02-06.md` for fast session restore.
- Verified near-parity between `legacy_full.../tools/` and `legacy_import.../tools/`.
- Flagged immediate follow-up priorities: `T01` canonical lock and template placeholder reconciliation.

### 2026-02-06 (processing start)

- Completed `T01`: canonical source locked to `legacy_full_investigate_strain/tools/`.
- Completed `T02`: parity verified with metadata-level exception in `progload/.git`.
- Completed `T03` baseline: ownership/status map created in `ownership_status.md`.

### 2026-02-06 (delegated analysis pass)

- Completed `T04` using delegated module-by-module analysis and documented details in `interface_contracts_detailed.md`.
- Completed `T08` with `path_assumptions_audit.md` (assumptions, normalization strategy, priority queue).
- Added consolidated contract/risk updates to `inventory.md` and retained restore context in dated snapshot files.

### 2026-02-06 (policy + mapping pass)

- Completed `T05` and `T06` with `external_dependency_policy.md`.
- Completed `T07` with `progload_scope_decision.md`.
- Completed `T09` with `cli_consistency_plan.md`.
- Completed `T10` with `data_contract_plan.md`.
- Completed `T11` and `T12` with `mp_toolchain_mapping.md`.

### 2026-02-06 (absolute path verification)

- Completed migration-plan absolute-path audit item with `absolute_path_audit.md`.
- Confirmed only one executable hard-coded absolute path in optional VTST stack.

### 2026-02-06 (operational reference)

- Added `command_matrix.md` as an execution-safe command matrix for active tool groups.
- Captured command-level inputs/outputs/dependencies/failure modes for faster recovery in future sessions.

### 2026-02-06 (first implementation target defined)

- Defined first concrete fix target in `first_fix_target_artemis_root_decoupling.md`.
- Locked Sprint-1 scope to root/path decoupling with explicit acceptance and verification checklist.

### 2026-02-06 (Sprint 1 implementation)

- Implemented Artemis root/path decoupling in `legacy_full_investigate_strain/tools/artemis_utilities/`.
- Added shared resolver: `scripts/pathing.py`.
- Added manager-level path options (`--root`, `--interfaces-dir`, `--run-root-mlp`, `--run-root-dft`) and propagated to setup/run/cleanup flows.
- Added safety guards for cleanup/operations against missing interfaces paths and filesystem-root target.
- Added resolved-path logging before mutation/submission actions.
- Performed syntax validation (`python -m py_compile`) and basic runtime checks for new CLI/help/guards.

### 2026-02-06 (tools migration kickoff, Option 3)

- Created `alexanderholman/mp1-tools` from template.
- Implemented Phase 1 package scaffold with `mp1-id` and `mp1-energies` CLIs.
- Added macro repo dev submodule at `vendor/mp1-tools` and pinned lock file `mlp_tools.lock`.
