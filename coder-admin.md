# Administering SOLAI Node From SOLAI Coder

SOLAI Coder can act as a user-friendly administration layer for SOLAI Node.

This means users can manage local provider behavior from inside the Coder experience
while SOLAI Node remains an independent runtime that can also be installed and operated
separately.

## Planned admin surfaces

- Node health and availability
- Node version and readiness
- provider status
- model inventory
- pricing controls
- availability schedules
- local metrics
- provider unavailable and delete controls
- job status, cancellation, and retry controls
- job detail inspection
- job-to-provider assignment
- bounded runtime event inspection
- job route inspection
- runtime metering inspection
- runtime mode control
- embedded runtime lifecycle

## Initial runtime-backed admin categories

The private runtime has started exposing the provider administration categories that
SOLAI Coder can later use from the CLI/TUI:

- provider lookup
- provider enable
- provider disable
- provider pricing metadata
- provider availability schedule metadata
- structured missing-provider errors
- runtime metrics
- job lookup and cancellation
- job listing and status updates
- provider refresh
- optional runtime API key support
- public version and readiness diagnostics
- provider unavailable and delete controls
- job retry controls
- job detail controls
- job-to-provider assignment controls
- bounded runtime event inspection
- job route inspection
- runtime execution and metering display
- pause and drain controls for runtime maintenance
- filtered runtime lists
- stable ordered provider and job lists
- constrained job status transitions

## Example command surface

```bash
solai provider enable
solai provider status
solai provider price SOLAI-20B 4
solai provider schedule --from 22:00 --to 07:00
solai provider disable
solai provider unavailable
solai provider delete
solai node events
solai node metering
solai job detail
solai job route
solai job assign
solai job retry
```

## Product direction

Coder should make Node easy to operate. Node should remain the source of truth for
provider state, inference jobs, metering, and runtime policy.
