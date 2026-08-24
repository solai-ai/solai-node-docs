# Public Architecture

SOLAI Node is the inference runtime for the SOLAI platform. It connects SOLAI Coder,
DApps across multiple market segments, partner applications, provider machines,
model providers, pricing, telemetry, and usage tracking.

The runtime implementation is private. This public document describes the product
boundary and the integration model.

## Repository model

- `solai-ai/solai-node`: private runtime implementation
- `solai-ai/solai-node-docs`: public roadmap and architecture updates
- `solai-ai/solai-coder`: public coding experience and Node administration surface

## Runtime modes

- **Embedded**: SOLAI Coder starts or administers a local SOLAI Node for the user
- **Standalone local**: SOLAI Node runs by itself on a local or provider machine
- **Standalone remote**: SOLAI Node runs as a service for DApps, applications, and partners

## What SOLAI Node owns

- inference jobs
- DApp and partner inference access
- provider registration and discovery
- provider health and model inventory
- pricing and availability metadata
- metering and usage records
- routing and fallback behavior
- runtime health, readiness, version reporting, and metrics
- job lifecycle policy and retry behavior
- runtime state compatibility policy
- bounded operational event history
- job detail and provider assignment policy
- queue execution lifecycle
- job result, error, execution timing, and metering records
- provider heartbeat category
- runtime mode controls for running, paused, and draining operation
- structured execution failure records

## What SOLAI Coder owns

- local-first coding workflow
- model selection UX
- local provider setup UX
- embedded Node administration
- user-facing status and metrics display

## Community visibility

Public updates should describe milestones, capabilities, endpoint categories, and
integration progress. They should not expose provider secrets, billing internals,
private routing logic, infrastructure topology, or partner-specific implementation.

## Current public endpoint categories

- health, version, and readiness diagnostics
- protected runtime metrics
- protected runtime metering
- protected runtime mode inspection and updates
- provider discovery and inspection
- provider enable, disable, heartbeat, unavailable, delete, price, schedule, and refresh controls
- job intake, lookup, detail, route inspection, listing, provider assignment, status updates, cancellation, and retry controls
- bounded runtime event inspection
- filtered operational list views
