# Public Architecture

SOLAI Node is the inference runtime for the SOLAI platform. It connects SOLAI Coder,
partner applications, provider machines, model providers, pricing, telemetry, and
usage tracking.

The runtime implementation is private. This public document describes the product
boundary and the integration model.

## Repository model

- `solai-ai/solai-node`: private runtime implementation
- `solai-ai/solai-node-docs`: public roadmap and architecture updates
- `solai-ai/solai-coder`: public coding experience and Node administration surface

## Runtime modes

- **Embedded**: SOLAI Coder starts or administers a local SOLAI Node for the user
- **Standalone local**: SOLAI Node runs by itself on a local or provider machine
- **Standalone remote**: SOLAI Node runs as a service for applications and partners

## What SOLAI Node owns

- inference jobs
- provider registration and discovery
- provider health and model inventory
- pricing and availability metadata
- metering and usage records
- routing and fallback behavior
- runtime health and metrics

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

