# SOLAI Node Roadmap

SOLAI Node is planned as the private inference runtime for the SOLAI platform.
It is the bridge between applications, compute providers, model providers, pricing,
telemetry, and partner workloads.

The implementation details and provider integrations are private platform work.
This public roadmap exists so the community can follow the direction without exposing
security-sensitive code, partner integrations, or infrastructure internals.

## Product role

SOLAI Coder is the public local-first coding experience.

SOLAI Node is the inference layer that powers provider discovery, workload routing,
usage tracking, SOLAI Coder, and DApps across multiple market segments.

The Coder can use a local embedded Node for a simple user experience. Partners and
larger deployments can use SOLAI Node as a standalone service when they need
authenticated inference access without the full Coder experience.

## Public milestones

### Phase 1: Foundation

- Define the boundary between SOLAI Coder and SOLAI Node
- Document embedded, standalone local, and standalone remote deployment modes
- Keep the public Coder workflow stable while Node work moves behind a private runtime

### Phase 2: Contracts

- Define versioned job contracts
- Define provider capability contracts
- Define health, metrics, heartbeat, and usage event contracts
- Keep the contracts stable enough for Coder and partner integrations

### Phase 3: Runtime

- Add the standalone Node runtime
- Add local configuration and secure credential loading
- Add health checks, metrics, logs, and job status endpoints
- Support local and remote operation

### Phase 4: Provider network

- Add provider registration and discovery
- Add model inventory reporting
- Add pricing per model and workload class
- Add availability scheduling for provider machines
- Add fallback behavior for unavailable providers

### Phase 5: Partner workloads

- Define the DApp integration model for external applications across multiple segments
- Keep SOLAI Coder as the first embedded client while supporting non-Coder inference clients
- Support image, video, text, audio, and other inference workloads through provider adapters
- Track tenant usage and metering
- Add DApp and partner-facing API documentation
- Add operational controls for quotas, rate limits, and billing records

## Public progress format

Progress should be shared publicly as high-level updates:

- architecture notes
- protocol milestones
- endpoint categories
- integration status
- provider capability categories
- community-facing changelog entries

The public repository should not expose:

- provider secrets
- billing implementation details
- private partner logic
- infrastructure topology
- private model routing logic
- signing keys or credential flows

## Current status

The SOLAI Node repository has been created as a private runtime repository.
The initial private runtime foundation is now in place, including versioned contract
types, provider discovery, a standalone runtime entrypoint, health checks, provider
listing, provider probing, initial job intake, provider administration, local runtime
state persistence, operational metrics, basic job cancellation, optional runtime API
key protection, job listing, job status updates, provider refresh, public version
and readiness diagnostics, provider unavailable/delete controls, job retry controls,
stable ordered list responses, stricter job validation, constrained job status
transitions, runtime state schema compatibility checks, forward migration from the
previous local job format, job detail inspection, job attempt tracking, parent-job
linkage, job-to-provider assignment, bounded runtime event inspection, filtered
operational list views, safer default response limits, internal queue execution,
job result/error state, execution timing, provider heartbeat category, routing
inspection, initial metering records, bounded metering inspection, runtime mode
controls, queue pause/drain controls, structured execution failure records, the
provider adapter boundary, provider protocol classification, and the first real
local chat inference path with persisted results, token usage, and metering. The
real path has been validated end to end against a live local model provider.
SOLAI Coder now also has its first native Node client commands for health,
provider discovery, asynchronous chat execution, readiness and metrics, runtime
mode control, bounded event inspection, bounded metering inspection, job list and
detail inspection, routing inspection, assignment, cancellation, and retry.
Provider administration now includes bounded list and detail inspection, inventory
refresh, availability state control, guarded deletion, pricing, availability
scheduling, and heartbeat updates. The first protected provider-policy routes now
also have in-process HTTP coverage, including bounded filtering, state changes,
and active-job deletion protection.
The core job lifecycle now has matching HTTP coverage for creation, inspection,
routing, cancellation, and retry.
Runtime diagnostics, metrics, mode changes, status, and mode events now also
have local HTTP coverage with authorization checks.

This public docs repository tracks roadmap and community-facing progress.

Current public docs:

- [Public Architecture](architecture.md)
- [Administering SOLAI Node From SOLAI Coder](coder-admin.md)
- [Public Changelog](changelog.md)
