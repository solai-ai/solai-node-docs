# Public Changelog

This changelog tracks public SOLAI Node progress without exposing private runtime
implementation details, provider integrations, billing internals, credentials, or
partner-specific logic.

## 2026-08-20

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
