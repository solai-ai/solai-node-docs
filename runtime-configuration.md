# Runtime Configuration

SOLAI Node supports a small strict JSON configuration file for local operator
settings. It is passed through `solai-node serve --config PATH` or the
`SOLAI_NODE_CONFIG` environment variable.

```json
{
  "bind": "127.0.0.1:9876",
  "data_dir": "/var/lib/solai-node"
}
```

The file accepts only `bind` and `data_dir`; unknown fields are rejected. CLI
flags and environment settings take precedence over file values. API keys are
not stored in this file—use `SOLAI_NODE_API_KEY` or `--api-key`.
