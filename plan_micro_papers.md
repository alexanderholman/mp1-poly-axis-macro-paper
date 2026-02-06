# MP1 Plan: Poly-Axis Interface Analysis in Si

## Thesis claim

Single-axis interface models are useful controlled baselines but are not realistic for faceted grain-boundary networks because they cannot represent junction-induced strain and coupled multi-facet effects. Poly-axis models are required for realistic interface determination.

Final validation target: demonstrate that a dual-axis model can reproduce the interface structure observed by electron microscopy.

## Program structure

- `MP1` (this project) is the umbrella paper.
- The work is split into linked micro-papers that can each stand alone.
- Material system throughout: Si.
- Common methods stack across phases: DFT/VASP + MLIP (`mace-mpa-0`), strain, Bader, DOS/PDOS/LDOS, and defects where in scope.

## Model taxonomy used in MP1

- `Bi-axis (2D) step models`: `Box` and `Saw` are treated as the two step geometries.
- `Poly-axis capable models`: `Island` and `Checker` are treated as the model classes that naturally extend to 3D poly-axis networks.
- Naming convention in results should distinguish `bi-axis` from `poly-axis` explicitly.

## Locked protocols

- `Protocol L` (literature reproduction): use paper-matched settings for validation phases.
- `Protocol S` (Supers settings): use the team production settings for all comparative/final phases.

## Micro-paper roadmap

### MP1.1 - Sigma3 {112} reproduction

Goal
- Reproduce the reference Sigma3 {112} results with traceable setup parity.

Inputs
- Existing reference docs in `paper/library/`.
- Existing 1-axis/112 structures and run artifacts.

Deliverables
- Reproduction table: setup and convergence parity vs literature.
- Energetics comparison (reproduced vs reported).
- Relaxed structure snapshots for manuscript use.

Exit criteria
- Reproduced trends and key values are within predefined tolerance.

### MP1.2 - Sigma3 {111} reproduction

Goal
- Reproduce Sigma3 {111} literature baseline at the same rigor as MP1.1.

Deliverables
- Setup parity table.
- Energetics and structure comparison.

Exit criteria
- 111 baseline is validated and ready for transfer into Protocol S.

### MP1.3 - Protocol transfer (Supers settings)

Goal
- Freeze and document `Protocol S` as canonical settings for all forward comparisons.

Deliverables
- Versioned settings spec (INCAR/KPOINTS/POTCAR, relax strategy, tolerances).
- Rationale note on differences from `Protocol L`.

Exit criteria
- Protocol S is reproducible and used consistently in all remaining MPs.

### MP1.4 - Single-axis re-analysis under Protocol S

Goal
- Recompute single-axis 111 and 112 under Protocol S to create the controlled baseline.

Systems
- `1-axis/111`, `1-axis/112`.

Deliverables
- DFT and MACE energetics.
- Strain analysis outputs.
- Bader charge analysis.
- DOS, PDOS, LDOS outputs.

Exit criteria
- Complete and internally consistent single-axis baseline dataset.

### MP1.5 - Dual-axis core analysis (111|112)

Goal
- Demonstrate non-additive, junction-driven effects absent from single-axis models.

Model families
- Bi-axis step geometries: Box, Saw
- Poly-axis-capable geometries in 2-axis setting: Island, Checker

Deliverables
- Side-by-side single-axis vs dual-axis energetic comparison.
- Junction/line contribution analysis beyond planar interface terms.
- Strain localization comparison plots.
- Bader and DOS-family contrasts highlighting multi-axis effects.

Exit criteria
- Clear quantitative evidence that dual-axis behavior is not reducible to single-axis superposition.

### MP1.6 - Three-axis extension (110|111|112)

Goal
- Show how increased facet-network realism further changes energetics and response.

Scope note
- Prioritize `Island` and `Checker` for 3-axis/poly-axis extension.
- Treat `Box` and `Saw` as bi-axis reference geometries (not primary 3-axis candidates).

Deliverables
- 3-axis structural and energetic results under Protocol S.
- Strain/charge/electronic comparisons against 1-axis and 2-axis baselines.

Exit criteria
- 3-axis results reinforce the poly-axis necessity claim and remain method-consistent.

### MP1.7 - Defect campaign across axis complexity

Goal
- Map defect behavior across 1-axis, 2-axis, and 3-axis environments.

Defect classes
- Vacancy
- Substitutional: `H, He, Li, Be, B, C, N, O, F, Ne, Al, P, Fe, Ge, Sn`
- Interstitial: substitutional set plus `Si`

Deliverables
- Defect formation energies and preferred-site maps by model class.
- Bader/electronic signatures for representative defects.
- Comparative tables showing which conclusions change with axis complexity.

Exit criteria
- Defect trends can be tied to poly-axis structural/strain environment, not only local chemistry.

### MP1.8 - Synthesis and manuscript assembly

Goal
- Integrate all micro-paper outputs into one coherent MP1 manuscript.

Deliverables
- Final figure set and table set.
- Final methods and reproducibility notes.
- Argument-driven discussion and conclusion focused on realism gap of single-axis models.

Exit criteria
- Submission-ready manuscript with traceable provenance for every key result.

### MP1.9 - Electron microscopy structure validation

Goal
- Demonstrate that the dual-axis model reproduces the experimentally observed interface structure from electron microscopy.

Deliverables
- Side-by-side structural comparison: microscopy image features vs simulated dual-axis motif.
- Orientation and facet-index mapping used for direct comparison.
- Quantitative agreement metrics (for example: facet angles, segment lengths, junction geometry descriptors).
- Sensitivity note showing robustness across small setup/model perturbations.

Exit criteria
- Dual-axis model reproduces the defining microscopy-observed structural features with clear quantitative support.

## Figure and table checklist (MP1 final)

Figures
- F1: Conceptual schematic (single-axis vs poly-axis).
- F2: Literature reproductions ({112}, {111}).
- F3: Protocol S single-axis baseline results.
- F4: Dual-axis model family overview (island, step, box/saw, checker).
- F4: Dual-axis model family overview (bi-axis: box/saw; poly-axis-capable: island/checker).
- F5: Strain localization comparison (1-axis vs 2-axis vs 3-axis).
- F6: Energetic decomposition showing multi-axis excess term.
- F7: Charge and DOS/PDOS/LDOS contrasts.
- F8: Defect response summary across axis complexity.
- F9: Electron microscopy vs dual-axis structural overlay/comparison.

Tables
- T1: Method/protocol settings matrix (L vs S).
- T2: Energetic summary (DFT and MACE; normalized consistently).
- T3: Structural metrics and strain descriptors.
- T4: Defect formation energies and site preference summary.

## Data and reproducibility requirements

- Keep one normalized data schema for all energies and metadata.
- Use consistent normalization units (per atom, per area, and per junction length where applicable).
- Record provenance for each plotted value (source path, run type, protocol version).
- Keep analysis scripts deterministic and shared across all MPs.

## Milestones

- M1: MP1.1 + MP1.2 complete (literature calibration done).
- M2: MP1.3 + MP1.4 complete (Protocol S baseline fixed).
- M3: MP1.5 complete (core novelty demonstrated).
- M4: MP1.6 + MP1.7 complete (network realism + defect generality).
- M5: MP1.8 complete (integrated paper ready).
- M6: MP1.9 complete (experimental structure validation complete).

## Immediate next actions

- [ ] Confirm and pin the canonical `Protocol S` input set.
- [ ] Write a machine-readable experiment matrix for MP1.1 to MP1.8.
- [ ] Build one aggregation script in `src/` to collect energies/metadata into a single results table.
- [ ] Draft Figure F1 and F2 first to lock narrative before full computation expansion.
