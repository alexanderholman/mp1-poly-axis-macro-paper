# WIP

## Active
- Tools migration program is active with Option 3 selected (pinned pip SHA + macro dev submodule).
- `mp1-tools` Phase 2 delivered (`mp1-vasp` added, namespace now `mlp_tools`, pins rolled out to macro + micro repos).
- Legacy local context to preserve: `legacy_full_investigate_strain` branch `file_sort` has local Artemis commit `294f4d0` and untracked local artifacts.

## Next
- Phase 3: migrate `artemis_utilities` into `mp1-tools` with `--dry-run` and safety guards.
- Separate follow-up: reconcile SBATCH template placeholder mismatch (`{name}` vs formatter fields).
- Decide handling for local untracked artifacts in `legacy_full_investigate_strain` (`__pycache__`, one DOS/process path).

## Done
- Macro + 9 micro-paper repos created from template and wired as submodules.
- Template placeholder/docs cleanup completed and pushed across all repos.
- Legacy processing planning scaffolds completed (`01-tools`, `02-structures`) with restart-safe checklists.
- `mp1-tools` created and integrated into macro repo (`vendor/mp1-tools`) with lock-based pinning.
- Lock naming standardized to `mlp_tools.lock` and pin updated to include `mlp_tools` namespace + `mp1-vasp`.
