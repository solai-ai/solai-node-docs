# Public Changelog

This changelog tracks public SOLAI Node progress without exposing private runtime
implementation details, provider integrations, billing internals, credentials, or
partner-specific logic.

## 2026-08-20

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

