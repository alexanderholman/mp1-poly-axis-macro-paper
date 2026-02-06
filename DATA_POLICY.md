# Data and Repository Policy

This repository (`mp1-poly-axis-macro-paper`) is the macro coordination repo.

## What belongs here

- Program-level planning and coordination documents.
- Micro-paper registry and submodule pointers.
- Lightweight metadata and reproducibility notes.

## What does not belong here

- Large legacy calculation trees.
- Imported historical workspaces.
- Bulk paper build artifacts and heavy intermediate files.

The following top-level directories are intentionally ignored in this macro repo:

- `legacy_full_investigate_strain/`
- `legacy_import/`
- `paper/`

## Source of truth for micro-paper work

Each micro-paper under `micro_papers/` is an independent git repository and is tracked here as a submodule.

## Rationale

- Keep macro history focused and fast.
- Avoid committing large, high-churn artifacts into the coordination repository.
- Preserve independent development cadence for each micro-paper.
