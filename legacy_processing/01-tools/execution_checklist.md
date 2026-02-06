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
- [ ] Decide canonical source: `legacy_full_investigate_strain/tools/` (recommended) or `legacy_import/tools/`.
- [ ] Record rationale and decision date.
- [ ] Mark non-canonical tree as reference-only in docs.

### Job T02 - Verify parity against reference tree
- [ ] Compare top-level directories in canonical vs reference tree.
- [ ] Record any mismatches (missing dirs/files, version differences).
- [ ] Decide whether mismatches are intentional or need reconciliation.

---

## 2) Ownership and status mapping

### Job T03 - Ownership table (top-level)
- [ ] Assign owner/status for each top-level tool group:
  - `artemis_utilities`
  - `vasp_utilities`
  - `task_utilities`
  - `id_utilities`
  - `progload`
  - `C-QM`
  - `bader` / `bader_src`
  - `vtstscripts-1039`
- [ ] Status values: active, optional, deprecated, external-vendor, unknown.

### Job T04 - Interface contract inventory
- [ ] For each active group, document entrypoints and expected inputs/outputs.
- [ ] Note required runtime dependencies (ASE, pymatgen, Slurm, rsync, etc.).
- [ ] Note required directory assumptions (e.g., `DINTERFACES/`).

---

## 3) External dependency policy

### Job T05 - Bader policy
- [ ] Record preferred installation route (binary vs build from `bader_src`).
- [ ] Record version pinning/checksum expectations.
- [ ] Record license/citation requirements.

### Job T06 - VTST policy
- [ ] Record expected VTST version and source.
- [ ] Record activation method (PATH/module/wrapper).
- [ ] Record scope for MP1 (which scripts are in-scope vs out-of-scope).

### Job T07 - Progload policy
- [ ] Decide whether Progload is required for MP1 active workflow.
- [ ] If required, document build and runtime procedure.
- [ ] If optional/deprecated, mark as reference-only.

---

## 4) Workflow hardening plan (documentation only in this phase)

### Job T08 - Path assumptions audit plan
- [ ] List scripts with hard-coded path assumptions.
- [ ] Define future normalization strategy (config/env/CLI arguments).
- [ ] Prioritize fixes by MP impact.

### Job T09 - CLI consistency plan
- [ ] Define target CLI style for managed utilities.
- [ ] Identify missing/empty CLI entrypoints (e.g., `task_utilities/run.py`).
- [ ] Define acceptance criteria for "ready" CLI wrappers.

### Job T10 - Data contract plan
- [ ] Define stable schema references for key outputs (`energies.json`, Bader exports, DOS outputs).
- [ ] Define provenance requirements (input hashes/setup IDs).
- [ ] Define where schema docs will live.

---

## 5) MP mapping and minimum viable toolchain

### Job T11 - MP critical path mapping
- [ ] Map exact required tools to each MP stage:
  - MP1.1
  - MP1.2
  - MP1.3
  - MP1.4
  - MP1.5
  - MP1.6
  - MP1.7
  - MP1.8
  - MP1.9
- [ ] Mark each dependency as required vs optional.

### Job T12 - Minimal reproducible stack definition
- [ ] Define smallest tool subset needed to execute MP1.1 and MP1.2 end-to-end.
- [ ] Define extension subset needed for MP1.5/MP1.6/MP1.7.
- [ ] Define acceptance checklist for "toolchain ready".

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
