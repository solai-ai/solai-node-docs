# Public Changelog

This changelog tracks public SOLAI Node progress without exposing private runtime
implementation details, provider integrations, billing internals, credentials, or
partner-specific logic.

## 2026-08-20

### Execution and metering lifecycle started

The private SOLAI Node runtime now has the first end-to-end execution lifecycle for
jobs, from queue intake through runtime result and metering records.

Publicly shareable progress:

- Internal queue worker category started
- Initial deterministic adapter path added for lifecycle validation
- Job execution state now records timing and adapter category
- Job result and structured error fields added to runtime state
- Metering record category added
- Runtime metering inspection endpoint category added
- Provider heartbeat category added
- Job routing inspection category added
- Runtime metrics now include metering record count
- Worker emits job started, job completed, and metering recorded events
- Tests added for routing and worker-driven completion
- Runtime validation confirmed schema generation, automatic job completion, result recording, execution timing, metering output, and operational events

This update does not expose private provider adapter implementation, routing
policy internals, billing internals, partner workload logic, credentials, or
infrastructure topology.

### Runtime state and audit surface expanded

The private SOLAI Node runtime now has stronger state handling and operational
inspection for local, Coder-managed, and standalone deployments.

Publicly shareable progress:

- Runtime state advanced to the next schema generation
- Existing local state can migrate forward from the previous job format
- Job detail inspection category added
- Job retry now preserves original job payload metadata at the runtime level
- Job attempt tracking and parent-job linkage added
- Optional provider assignment category added for jobs
- Bounded runtime event inspection category added
- Provider, job, and event list filtering started
- Default response limits added for operational list endpoints
- Provider deletion is guarded when active jobs still reference the provider
- Additional validation added for job payload size and identifier lengths
- CLI support added for runtime events, job detail, and job assignment
- Tests added for migration, filtering, event trimming, payload limits, and retry payload preservation
- Runtime validation confirmed protected events, job detail, filtered list responses, cancellation, retry, and event records

This update does not expose private payload contents, provider adapters, routing
logic, execution internals, billing internals, tenant policy, credentials, or
partner-specific implementation.

### Runtime control surface expanded

The private SOLAI Node runtime now has a broader production control surface for
Coder-managed and standalone deployments.

Publicly shareable progress:

- Public version endpoint added for local automation and diagnostics
- Public readiness endpoint added for runtime orchestration
- Provider unavailable state endpoint added
- Provider deletion endpoint added
- Job retry endpoint added for failed or cancelled jobs
- Provider and job list responses are now stable ordered
- Job creation validation rejects empty model values
- Job status transitions are now constrained
- Runtime state loading rejects unsupported future schema versions
- CLI support added for version, readiness, provider unavailable, provider delete, and job retry
- Tests added for schema compatibility, stable ordering, job validation, and status transitions
- Runtime validation confirmed public diagnostics, protected endpoints, cancellation, invalid-transition conflict, and retry behavior

This update does not expose private routing logic, execution internals, payload
handling, billing internals, tenant policy, provider integrations, credentials,
or partner-specific implementation.

### Runtime operations hardened

The private SOLAI Node runtime now has stronger operational controls for local and
Coder-managed deployments.

Publicly shareable progress:

- Optional runtime API key support added
- Health remains available for local probes
- Operational endpoints can now require authenticated requests
- CLI requests can use the same runtime API key from the environment
- Provider refresh endpoint added
- Job listing endpoint added
- Job status update endpoint added
- Local state now includes an explicit schema version
- Provider price validation added
- Provider schedule validation added
- Tests added for authentication, validation, status parsing, metrics, and persistence
- Runtime validation confirmed protected endpoints reject unauthenticated calls

This update does not expose private auth policy evolution, key management internals,
provider execution details, routing logic, tenant policy, infrastructure topology,
or partner-specific implementation.

### Operational metrics and job cancellation started

The private SOLAI Node runtime now has the first operational metrics surface and
basic job cancellation.

Publicly shareable progress:

- Runtime metrics endpoint added
- Provider counts by status added
- Job counts by status added
- Job cancellation endpoint added
- CLI support started for runtime metrics
- CLI support started for job lookup and job cancellation
- Cancelled jobs persist to local runtime state
- Tests added for provider and job metrics
- Runtime validation confirmed metrics update after job cancellation

Current operational endpoint categories:

```text
GET  /v1/metrics
POST /v1/jobs/{job_id}/cancel
```

This update does not expose private scheduling internals, routing logic, provider
execution details, billing internals, tenant policy, or partner-specific implementation.

### Local runtime persistence started

The private SOLAI Node runtime now persists local runtime state across restarts.

Publicly shareable progress:

- Runtime data directory support added
- Environment-based data directory configuration added
- Provider and job state persistence started
- Atomic state-file writes added
- Missing state file now loads as an empty runtime state
- Tests added for state loading and round-trip persistence
- Runtime validation confirmed state is written after job intake

This update does not expose private state schema evolution plans, provider secrets,
tenant policy, billing calculation internals, infrastructure topology, or
partner-specific implementation.

### Provider administration surface started

The private SOLAI Node runtime now includes the first provider administration
surface needed for Coder-managed Node operation.

Publicly shareable progress:

- Provider lookup endpoint added
- Provider enable endpoint added
- Provider disable endpoint added
- Provider price endpoint added
- Provider schedule endpoint added
- CLI commands started for provider administration
- Provider state now includes status, pricing metadata, schedule metadata, and update timestamps
- Runtime returns structured errors for missing providers

Current provider administration endpoint categories:

```text
GET  /v1/providers/{provider_id}
POST /v1/providers/{provider_id}/enable
POST /v1/providers/{provider_id}/disable
POST /v1/providers/{provider_id}/price
POST /v1/providers/{provider_id}/schedule
```

This update does not expose private provider integrations, routing rules, billing
calculation internals, tenant policy, infrastructure topology, or partner-specific
implementation.

### Initial private runtime foundation

The private SOLAI Node repository now has an initial executable runtime foundation.

Publicly shareable progress:

- Initial Rust workspace created for the private runtime
- Versioned contract layer started
- Provider discovery layer started
- Standalone runtime and CLI entrypoint started
- Health endpoint added
- Provider list endpoint added
- Provider probe endpoint added
- Job creation and job lookup endpoints started
- Basic provider probing follows the existing SOLAI Coder local-provider behavior
- Initial tests added around provider address normalization and model-name handling

Current initial endpoint categories:

```text
GET  /v1/health
GET  /v1/providers
POST /v1/providers/probe
POST /v1/jobs
GET  /v1/jobs/{job_id}
```

This update does not expose private providers, routing logic, billing internals,
tenant policy, infrastructure topology, or partner-specific implementation.
