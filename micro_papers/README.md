# MP1 Micro-Papers Workspace

This directory tracks the execution units that feed the final MP1 macro paper.

## Scope

- Material: Si
- Core claim: poly-axis modeling is required for realistic faceted interface networks
- Baseline comparator: single-axis models

## Sequence

1. `mp1.1-sigma3-112-reproduction`
2. `mp1.2-sigma3-111-reproduction`
3. `mp1.3-protocol-transfer-supers-settings`
4. `mp1.4-single-axis-111-112-protocol-s`
5. `mp1.5-dual-axis-model-comparison`
6. `mp1.6-three-axis-extension-110-111-112`
7. `mp1.7-defect-campaign-across-axis-complexity`
8. `mp1.8-synthesis-manuscript-assembly`
9. `mp1.9-electron-microscopy-structure-validation`

## Model taxonomy

- Bi-axis (2D step): `box`, `saw`
- Poly-axis capable: `island`, `checker`

## Required analysis stack

- Energetics: DFT/VASP and MACE (`mace-mpa-0`)
- Strain analysis
- Bader charge analysis
- DOS/PDOS/LDOS
- Defects (where in scope)
