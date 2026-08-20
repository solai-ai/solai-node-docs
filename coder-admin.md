# Administering SOLAI Node From SOLAI Coder

SOLAI Coder can act as a user-friendly administration layer for SOLAI Node.

This means users can manage local provider behavior from inside the Coder experience
while SOLAI Node remains an independent runtime that can also be installed and operated
separately.

## Planned admin surfaces

- Node health and availability
- provider status
- model inventory
- pricing controls
- availability schedules
- local metrics
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

## Example command surface

```bash
solai provider enable
solai provider status
solai provider price SOLAI-20B 4
solai provider schedule --from 22:00 --to 07:00
solai provider disable
```

## Product direction

Coder should make Node easy to operate. Node should remain the source of truth for
provider state, inference jobs, metering, and runtime policy.
