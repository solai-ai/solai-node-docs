# Runtime Configuration

SOLAI Node supports a small strict JSON configuration file for local operator
settings. It is passed through `solai-node serve --config PATH` or the
`SOLAI_NODE_CONFIG` environment variable.

```json
{
  "bind": "127.0.0.1:9876",
  "data_dir": "/var/lib/solai-node",
  "worker_tick_ms": 1000
}
```

The file accepts only `bind`, `data_dir`, and `worker_tick_ms`; unknown fields are rejected. CLI
flags and environment settings—including `--worker-tick-ms` and
`SOLAI_NODE_WORKER_TICK_MS`—take precedence over file values. API keys are not
stored in this file—use `SOLAI_NODE_API_KEY` or `--api-key`.

When configured, an API key must not be blank. Node rejects an explicitly empty
key at startup instead of silently running without authentication.

`worker_tick_ms` configures local queue polling. It must be between 10 and
60,000 milliseconds; the default is 1,000 milliseconds.

Node creates a missing data directory at startup. If the configured path exists
but is a file rather than a directory, startup fails before opening the listener.
