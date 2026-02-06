# Structures Migration Plan

## Objective

Create a reproducible MP1 structure layer while preserving the ability to recreate the legacy structure organization.

## Guiding principle

Preserve semantics first, optimize layout second.

## Step 1 - Freeze legacy schema

- Capture the current directory schema as the baseline reference.
- Define which subtrees are active vs archival.
- Record non-negotiable naming semantics (axis depth, facet IDs, orientation forms).

## Step 2 - Define canonical naming and mapping

- Define canonical naming rules for:
  - Miller index paths (including negative indices)
  - axis categories (`1-axis`, `2-axis`, `3-axis`)
  - facet-pair/triple slugs (`111-112`, `110-111-112`)
- Build a path mapping table:
  - legacy path -> canonical path
  - status: exact, transformed, archived

## Step 3 - Separate active from archival structures

- Mark active structure sources required for MP1.1-MP1.9.
- Mark archival/reference-only branches (`__archive__`, backup trees).
- Define retrieval policy for archived structures (on-demand only).

## Step 4 - Define structure metadata contract

- Specify required metadata for each structure unit:
  - structure type (bulk/surface/interface)
  - axis complexity and facet/orientation identifiers
  - provenance pointers to original legacy path
  - calculation readiness flags (VASP/MACE prepared)
- Define where metadata is stored and how it is versioned.

## Step 5 - Recreate template blueprint

- Publish a directory blueprint capable of recreating the legacy intent:
  - material category
  - axis complexity
  - orientation/facet ID
  - variants/configs
  - calc containers
- Include examples for:
  - single-axis (`1-axis/111`)
  - dual-axis (`2-axis/111-112`)
  - three-axis (`3-axis/110-111-112`)

## Step 6 - Tool compatibility planning

- Identify scripts that assume current structure paths.
- Define compatibility layer (path aliases or mapping resolver) before any restructure.
- Prioritize compatibility for MP1 critical path tools.

## Step 7 - Completion criteria

- Legacy schema documented and reproducible from blueprint.
- Active/archival split defined and reviewed.
- Mapping table complete for all in-scope structure paths.
- No planned structure change proceeds without documented tool-impact assessment.
