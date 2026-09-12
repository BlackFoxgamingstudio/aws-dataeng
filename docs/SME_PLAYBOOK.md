# SME Playbook & Interview Defense: Sovereign Aws Dataeng

## Role Alignment
Target Roles: Staff Software Engineer, Principal Systems Architect, Director of Engineering.

## 60-Second Elevator Pitch
"Proves Senior Cloud Data Engineer mastery: AWS lakehouse design, distributed Spark ETL, Athena partitioned queries, and infrastructure cost optimization."

## Key Technical Decisions
1. **Zero-Dependency Architecture**: Prevents dependency drift and keeps embedded/edge environments lean.
2. **Deterministic Idempotency**: Generates SHA-256 tokens from action and payload for guaranteed exactly-once processing in n8n workflows.
3. **Dual-Mode Testing**: Test suite uses `unittest` to guarantee execution in minimal standard environments while remaining 100% compatible with `pytest`.
