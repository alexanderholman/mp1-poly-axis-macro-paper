# Tools Migration Plan

## Objective

Move from duplicated legacy tool trees to one documented, reproducible toolchain for MP1.

## Step 1 - Lock canonical source

- Choose one source tree as canonical (`legacy_full_investigate_strain/tools/` recommended).
- Freeze the non-canonical copy as read-only reference.
- Record this decision in `decisions.md`.

## Step 2 - Normalize tool categories

- Split tools into:
  - maintained project scripts
  - external/vendor dependencies
  - deprecated/unused scripts
- Create a simple ownership table (owner, purpose, status, replacement).

## Step 3 - External dependency policy

- For `bader` and `vtstscripts-1039`:
  - pin versions
  - document acquisition/build steps
  - define license and citation notes
- Prefer install scripts over committing opaque binaries when practical.

## Step 4 - Path and interface hardening

- Remove hard-coded absolute paths from maintained scripts.
- Standardize CLI entrypoints and config input conventions.
- Add minimal smoke tests for each maintained tool family.

## Step 5 - MP mapping

- Map required tool subsets to MPs:
  - MP1.1, MP1.2: reproduction-critical tools only
  - MP1.4, MP1.5, MP1.6: full energetics + structure pipeline tools
  - MP1.7: defect-focused extensions
  - MP1.9: geometry/comparison extraction helpers

## Step 6 - Migration completion criteria

- One canonical tool tree documented.
- External dependencies pinned and reproducible.
- All active MPs run without legacy-path assumptions.
- Deprecated tools marked and excluded from active workflows.

## First execution tasks

- [ ] Decide canonical tool source directory.
- [ ] Produce ownership/status table for each top-level tool group.
- [ ] Identify all scripts that reference absolute legacy paths.
- [ ] Draft install notes for Bader and VTST dependencies.
