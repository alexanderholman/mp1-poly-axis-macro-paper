# Absolute Path Audit

Date: 2026-02-06
Scope: canonical tools tree `legacy_full_investigate_strain/tools/`

## Result summary

- No broad hard-coded local absolute paths found in active MP1 core scripts.
- One explicit absolute default path found in VTST helper stack.

## Findings

- `vtstscripts-1039/automagician.py`
  - `default_subfile_path_fri_halifax = "/home/kg33564/automagician-permanent/subfile-archive"`
  - Classification: external-vendor script path default; not baseline MP1 critical path.

- `vtstscripts-1039/kdbquery.py`
  - Comment-only mention of `/home/calculation` in explanatory text.
  - Classification: non-executable path reference.

## Related hard-couplings (non-absolute)

- Slurm templates hard-code account/email/module stack values.
- Many scripts are cwd-rooted (`Path.cwd()`, `os.getcwd()`) and layout-coupled.
- These are covered in `path_assumptions_audit.md`.

## Action

- Keep VTST out of baseline path unless explicitly enabled.
- If VTST is enabled, patch/remove absolute default path before production use.
