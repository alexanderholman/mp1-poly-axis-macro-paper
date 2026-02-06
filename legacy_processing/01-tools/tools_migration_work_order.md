# Tools Migration Work Order (Commit-Sized)

Mode: build
Date: 2026-02-06

This is an execution checklist where each numbered block is intended to land as its own commit (or small PR) to keep progress restartable.

## 0) Pre-flight

0.1 Decide names/paths
- [ ] Confirm tools repo name: `alexanderholman/mp1-tools`
- [ ] Confirm macro dev submodule path: `vendor/mp1-tools`
- [ ] Confirm per-repo lock file name: `mp1_tools.lock`

0.2 Guardrails
- [ ] Confirm we will not vendor: POTCAR libraries, Bader binary, VTST bundle

## 1) Create `mp1-tools` repository

1.1 Repo bootstrap
- [ ] Create `alexanderholman/mp1-tools` from `alexanderholman/template`
- [ ] Clone locally under a convenient workspace path

1.2 Add Python packaging skeleton
- [ ] Add `pyproject.toml` with `src/` layout
- [ ] Create `src/mp1_tools/__init__.py`
- [ ] Add minimal shared helpers in `src/mp1_tools/_shared/` (config + exit codes)

1.3 Add entrypoints
- [ ] Add console scripts: `mp1-id`, `mp1-energies` (stubbed OK)

## 2) Migrate `id_utilities` (Phase 1)

2.1 Copy code
- [ ] Copy legacy implementation into `src/mp1_tools/id/`
- [ ] Keep CLI surface compatible (input/output options)

2.2 Add docs
- [ ] Add `docs/id.md` describing inputs/outputs and examples

2.3 Add tests
- [ ] Add `tests/test_id_smoke.py` (imports + `--help`)
- [ ] Add minimal fixture POSCAR and test that outputs land in temp dir

## 3) Migrate energetics extraction (Phase 1)

3.1 Copy code
- [ ] Copy `task_utilities/scripts/analyse/energies.py` into `src/mp1_tools/energies/`
- [ ] Keep CLI behavior stable initially

3.2 Freeze schema contract
- [ ] Write `docs/energies_schema.md` capturing JSON keys and provenance requirements

3.3 Add tests
- [ ] Add smoke test (`--help`) and schema validation test (even without heavy VASP fixtures)

## 4) Add macro repo dev submodule (Option 3)

4.1 Add submodule
- [ ] Add `mp1-tools` as submodule at `vendor/mp1-tools`
- [ ] Document dev workflow in macro `INSTALL.md` or a dedicated `docs/tools_dev.md`

4.2 Add macro repo lock file
- [ ] Add `mp1_tools.lock` recording pinned SHA + install command

## 5) Wire micro-paper repos to pinned SHA install (Option 3)

5.1 Add lock file to each micro-paper repo
- [ ] Add `mp1_tools.lock` to `mp1-1` .. `mp1-9` repos
- [ ] Add short install stanza to each `INSTALL.md`

5.2 Record toolchain pinning rule
- [ ] Explicitly state: no floating `@main`; always pin SHA

## 6) Phase 2: `vasp_utilities` migration (licensing-safe)

6.1 Copy code with potcar-dir config
- [ ] Add `mp1-vasp` entrypoint
- [ ] Replace implicit POTCAR tree with required `--potcar-dir` / `VASP_POTCAR_DIR`

6.2 Add tests
- [ ] Add POSCAR parsing tests and failure-mode tests for missing POTCAR

## 7) Phase 3: `artemis_utilities` migration

7.1 Copy code
- [ ] Add `mp1-artemis` entrypoint
- [ ] Include root/path overrides and safety guards

7.2 Add dry-run mode
- [ ] `--dry-run` for setup/cleanup/submit operations

7.3 Separate sprint: template placeholder reconciliation
- [ ] Fix `{name}` vs `{lm}/{um}` mismatch
- [ ] Add regression test for template rendering

## 8) External dependency enablement (opt-in)

8.1 Bader
- [ ] Provide `docs/bader.md` install + citation checklist
- [ ] Add runtime detection and clear error hints (no vendored binary)

8.2 VTST
- [ ] Provide `docs/vtst.md` gating + license verification checklist
- [ ] Keep disabled by default

## 9) Completion criteria

- [ ] MP1.1 and MP1.2 can run end-to-end using `mp1-id` + `mp1-energies` installed from pinned SHA.
- [ ] Macro repo and micro-paper repos record toolchain pin in `mp1_tools.lock`.
- [ ] Tooling repo has smoke tests and documented contracts.
