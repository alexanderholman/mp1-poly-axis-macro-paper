# Legacy Tools Processing

This phase defines how legacy tooling is stabilized and mapped into MP1 micro-paper workflows.

## Goals

- Identify which tools are still required.
- Separate external binaries from project-owned scripts.
- Define a minimal maintained toolchain for MP1 execution.

## Outputs for this phase

- `inventory.md`: current tool inventory and classification.
- `migration_plan.md`: stepwise migration and validation plan.
- `execution_checklist.md`: session-safe checklist for job-by-job progress and handoff.
- `context_snapshot_YYYY-MM-DD.md`: dated analysis snapshots for fast session restore.
- `tool_contracts.md`: draft interfaces for each top-level tool group.
- `canonical_source_decision.md`: canonical tools-tree decision and rationale.
- `ownership_status.md`: current owner/scope/status map for each top-level tool group.
- `interface_contracts_detailed.md`: command-level contracts for active tool groups.
- `path_assumptions_audit.md`: hard-coupled path assumptions and normalization priorities.
- `absolute_path_audit.md`: hard-coded absolute-path findings.
- `external_dependency_policy.md`: policy/checklist for Bader and VTST external dependencies.
- `cli_consistency_plan.md`: standard CLI target and staged wrapper rollout plan.
- `progload_scope_decision.md`: MP1 scope and activation criteria for Progload.
- `data_contract_plan.md`: schema/provenance contract for key analysis outputs.
- `mp_toolchain_mapping.md`: required vs optional tool map across MP1.1-MP1.9.
