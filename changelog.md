# Public Changelog

This changelog tracks public SOLAI Node progress without exposing private runtime
implementation details, provider integrations, billing internals, credentials, or
partner-specific logic.

## 2026-08-30

### Provider heartbeat capacity persistence added

Provider heartbeat capacity and active-job data is now retained in the provider
descriptor used by operational inspection.

Publicly shareable progress:

- Persists supplied capacity and active-job counts
- Rejects heartbeat data where active jobs exceed known capacity
- Returns the persisted fields through provider inspection
- Preserves provider status when a heartbeat only updates capacity data
- Coder sends only explicitly supplied heartbeat fields
- Coder rejects locally inconsistent capacity values before sending

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Capacity-aware provider routing added

Provider capacity reports now affect operational routing and assignment decisions.

Publicly shareable progress:

- Excludes a full provider from automatic routing
- Rejects explicit assignment to a provider at its reported capacity
- Selects another compatible provider when capacity is available
- Explains capacity exhaustion during route inspection

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Provider capacity metrics added

Runtime metrics now summarize the capacity information supplied by provider
heartbeats.

Publicly shareable progress:

- Reports total known provider capacity and active-job counts
- Reports routing-eligible available capacity slots
- Keeps raw provider topology and billing logic private

### Strict local runtime configuration added

SOLAI Node can now load its bind address and runtime data directory from a
strict local JSON configuration file.

Publicly shareable progress:

- Added `--config` and `SOLAI_NODE_CONFIG` support for `serve`
- Rejects unknown configuration fields at startup
- CLI and environment values override file settings
- Keeps API keys outside normal configuration files
- Validates the data directory before opening the HTTP listener
- Supports a bounded local queue-worker polling interval
- Allows CLI and environment overrides for the polling interval
- Exposes the effective polling interval in runtime status
- Rejects explicitly empty configured API keys at startup

This update does not expose credentials, provider addresses, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Native Coder operations expanded

SOLAI Coder can now inspect and control the essential operational state of a
running SOLAI Node from the main CLI.

Publicly shareable progress:

- Added Node version and readiness diagnostics
- Added provider, job, and metering counters
- Added runtime status and running/paused/draining mode controls
- Added bounded, filterable runtime event inspection
- Added bounded, filterable metering inspection
- Client-side limits match the Node maximum of 500 records
- Live acceptance confirmed the full Coder-to-Node-to-local-model operations path

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Native Coder provider control completed

SOLAI Coder can now inspect and operate the local-provider lifecycle from the
same CLI used for jobs and runtime controls.

Publicly shareable progress:

- Added bounded, filterable provider listing and individual provider inspection
- Added provider model-inventory refresh
- Added available, disabled, and unavailable state controls
- Added deletion with an explicit local confirmation flag
- Node continues to reject deletion while active jobs reference the provider
- Live acceptance confirmed control transitions against a local model provider

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Native Coder provider policy controls completed

SOLAI Coder can now maintain the operational policy data carried by a local
provider descriptor.

Publicly shareable progress:

- Added per-model positive-decimal price updates
- Added daily availability windows using 24-hour times and optional IANA timezones
- Added provider heartbeats for status, capacity, and active-job counts
- Live acceptance confirmed all three operations persist through a running Node

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Provider policy HTTP coverage added

The Node test suite now exercises provider-policy operations through the actual
HTTP router instead of only calling internal handlers.

Publicly shareable progress:

- Verifies protected price, schedule, and heartbeat routes
- Verifies changes are visible through a subsequent provider read
- Verifies bounded provider filters, availability transitions, and active-job
  deletion protection
- Keeps this coverage local and independent from external model-provider access

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Job lifecycle HTTP coverage added

The Node test suite now exercises the normal asynchronous job lifecycle through
the actual HTTP router.

Publicly shareable progress:

- Verifies creation, bounded filtered listing, detail, and route inspection
- Verifies cancellation and linked retry attempts
- Keeps the lifecycle coverage local and independent from external model access

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Runtime operations HTTP coverage added

The Node test suite now exercises the operational runtime endpoints through the
actual HTTP router.

Publicly shareable progress:

- Verifies public health diagnostics and API-key protection for operator endpoints
- Verifies metrics, runtime mode changes, persisted runtime status, and mode events
- Keeps the operational coverage local and independent from external model access

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Completed-job HTTP coverage added

The Node test suite now verifies the HTTP-visible records produced by the worker
after a job finishes.

Publicly shareable progress:

- Verifies completed job detail and output
- Verifies filtered metering and completion-event inspection
- Keeps the worker and HTTP coverage local and independent from external models

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### HTTP contract hardening round completed

Twenty additional local HTTP contract cases now protect the operational surface
used by SOLAI Coder and standalone Node operators.

Publicly shareable progress:

- Verifies public diagnostics, bearer authentication, and protected read routes
- Verifies invalid provider and job requests return structured HTTP errors
- Verifies constrained job-status transitions and terminal-job protections

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### Native Coder job control completed

SOLAI Coder can now inspect and control the normal lifecycle of asynchronous
Node jobs from the main CLI.

Publicly shareable progress:

- Added bounded, filterable job listing
- Added persisted job detail and route inspection
- Added assignment to an available provider
- Added explicit cancellation and retry commands
- Retry preserves history by creating a linked new attempt
- Live acceptance confirmed cancellation, retry, real model completion, and metering

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

## 2026-08-29

### First native SOLAI Coder client completed

SOLAI Coder can now talk directly to a running SOLAI Node from its main CLI.
The initial client covers runtime health, local-provider discovery, and a real
asynchronous chat job from submission through final model output.

Publicly shareable progress:

- Added `solai node health`, `solai node probe`, and `solai node chat`
- Added configurable Node URL and optional API-key forwarding
- Chat jobs poll the Node lifecycle and return assistant text or complete JSON
- Provider selection can be explicit or delegated to Node routing
- Focused CLI tests and compile validation added
- Live acceptance confirms the Coder-to-Node-to-local-model path

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

### First real local inference path completed

SOLAI Node has moved beyond the deterministic execution path for its first text
workload. A discovered local model provider can now receive an asynchronous chat
job, execute it, and return the model response through the normal Node lifecycle.

Publicly shareable progress:

- Provider discovery now records the provider protocol category
- First real chat workload adapter added
- Queue routing now selects the execution adapter from the provider category
- Successful jobs persist the model response, timing, and token counts
- Generated-token usage is recorded in the metering entry
- Connection, provider, input, and response failures use structured job errors
- Unit, formatting, and lint validation pass
- A live local-provider acceptance run confirmed probe, queue, execution, result,
  and metering behavior without simulated inference

This update does not expose provider addresses, credentials, private routing
policy, billing calculations, partner logic, or infrastructure topology.

## 2026-08-24

### Bounded metering inspection added

The private SOLAI Node runtime now supports bounded, filterable metering reads for
Coder-managed and standalone operator workflows.

Publicly shareable progress:

- Metering list responses now follow the bounded operational list pattern
- Metering records can be filtered by tenant, provider, job, workload, and model
- Metering responses are returned in stable recorded-time order
- Pagination support added for metering inspection
- Tests added for metering filtering, ordering, and pagination
- Runtime validation confirmed the full test suite passes after the metering update

This update does not expose private billing implementation details, pricing policy,
provider adapter internals, partner workload logic, credentials, or infrastructure
topology.

## 2026-08-20

### Runtime operations and failure handling hardened

The private SOLAI Node runtime now has operator-facing runtime modes and structured
failure handling for the execution lifecycle.

Publicly shareable progress:

- Runtime mode category added
- Operators can inspect runtime queue state
- Runtime can be switched between running, paused, and draining modes
- Queue worker only starts jobs while the runtime is in running mode
- Structured adapter failure path added
- Failed jobs now persist error details and execution timing
- Failed jobs emit operational events
- Tests added for paused runtime behavior and structured failure recording
- Runtime validation confirmed paused jobs remain queued, running mode resumes processing, and forced failures are recorded without metering

This update does not expose private provider adapter implementation, failure policy
internals, credential handling, billing internals, partner workload logic, or
infrastructure topology.

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
