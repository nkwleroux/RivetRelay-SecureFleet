# SecureFleet Architecture

## Services

- **API:** operator-facing REST endpoints, authentication, authorization, and audit access.
- **Ingestion:** accepts device telemetry and health data.
- **Command service:** creates idempotent desired-state and command operations.
- **Deployment worker:** evaluates canary and percentage rollout policies.
- **Health evaluator:** pauses or rolls back releases when thresholds fail.
- **Artifact metadata service:** records firmware/image hashes, signatures, and compatibility.
- **Console:** real-time operational interface using REST plus SignalR/SSE.
- **Simulator:** deterministic virtual fleet for load and failure scenarios.

## Data boundaries

PostgreSQL is authoritative for identity, configuration, deployment, and audit records. Redis is optional for caches and transient coordination, never the only store of important state. Object storage can hold large firmware artifacts while PostgreSQL retains immutable metadata and hashes.

## Security boundaries

- Human operators authenticate through OIDC and receive role-based permissions.
- Devices use unique identities and mutually authenticated transport where practical.
- Release manifests are signed separately from transport security.
- Every configuration, command, and deployment transition produces an audit event.

## Deployment progression

Begin as a modular monolith with background workers. Split services only when scaling, isolation, or failure boundaries justify the operational cost.

