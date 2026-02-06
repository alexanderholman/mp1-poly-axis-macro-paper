# Structures Migration Execution Checklist

Purpose: migrate structure assets in small, restart-safe jobs while preserving the ability to recreate legacy structure layout.

Rule: planning/tracking only. No restructuring work is required to complete checklist updates.

---

## 0) Session control (every session)

- [ ] Confirm active repo path and branch.
- [ ] Confirm active job ID below.
- [ ] Record blockers from last session.
- [ ] End session with completed/in-progress/next job notes.

---

## 1) Legacy schema capture

### Job S01 - Snapshot structure hierarchy
- [ ] Capture and store canonical tree snapshot for `data/structures/`.
- [ ] Confirm inclusion of bulks, surfaces, interfaces, and terminations.
- [ ] Record date/version for snapshot.

### Job S02 - Classify active vs archival branches
- [ ] Tag active branches used by MP1 execution.
- [ ] Tag archival branches (`__archive__`, backup trees, etc.).
- [ ] Record uncertain branches needing user decision.

---

## 2) Naming and mapping

### Job S03 - Naming convention lock
- [ ] Define rules for Miller index naming (including negative index forms).
- [ ] Define rules for facet pair/triple naming.
- [ ] Define rules for axis labels and future extensions.

### Job S04 - Path mapping table
- [ ] Build table: legacy path -> canonical path.
- [ ] Add mapping status: exact, transformed, archived.
- [ ] Add notes for any lossy/non-trivial transformations.

---

## 3) Recreate blueprint

### Job S05 - Directory blueprint draft
- [ ] Draft recreate blueprint for bulk/surface/interface families.
- [ ] Include axis-depth and facet examples.
- [ ] Include config/variation/archive placement rules.

### Job S06 - Recreate validation checklist
- [ ] Define checks proving a recreated tree matches legacy intent.
- [ ] Define minimum required files/subdirs per structure node.
- [ ] Define acceptance criteria for "recreate complete".

---

## 4) Metadata contract planning

### Job S07 - Required metadata fields
- [ ] Define mandatory metadata for each structure unit.
- [ ] Define provenance fields back to legacy paths.
- [ ] Define readiness flags for VASP and MACE pipelines.

### Job S08 - Metadata storage plan
- [ ] Decide metadata file format and placement.
- [ ] Define update policy (manual/generated/hybrid).
- [ ] Define review/validation workflow for metadata changes.

---

## 5) Tool compatibility and risk control

### Job S09 - Path-coupled tool audit plan
- [ ] Identify tooling that assumes current structure path shapes.
- [ ] Rank by criticality for MP1.1-MP1.9.
- [ ] Define compatibility strategy before any move/rename.

### Job S10 - Risk register update
- [ ] Track risks from structural rename/move operations.
- [ ] Track risk of archive/active confusion.
- [ ] Track risk of broken provenance links.

---

## 6) MP alignment

### Job S11 - MP dependency mapping
- [ ] Map required structure subsets to each MP stage.
- [ ] Mark required vs optional structure families.
- [ ] Flag missing structure assets per MP.

### Job S12 - Minimal structure set definition
- [ ] Define minimal structure set for MP1.1 + MP1.2.
- [ ] Define incremental adds for MP1.5/MP1.6/MP1.7.
- [ ] Define completion criteria for structure readiness by milestone.

---

## 7) Blockers and handoff

### Blocker log
- [ ] None currently.

Use this format for new blockers:
- [ ] `BLOCKER-ID`: short title
  - Impact:
  - Detected in:
  - Workaround:
  - Resolution owner:

### Handoff template

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
