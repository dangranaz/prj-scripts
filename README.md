# prj-scripts

Simple, user-facing operational scripts for running the published engines —
start/stop a server without needing to know the internals.

## Layout

```
prj-scripts/
└── engine-mlx/
    ├── start-server.sh    ← bring the engine-mlx server up on a model
    └── stop-server.sh     ← stop it
```

## engine-mlx

```bash
# 1. install the MLX C API
brew install mlx-c

# 2. start the server on a model directory (contains config.json)
./engine-mlx/start-server.sh /path/to/Qwen3-1.7B-MLX-4bit
#    → serves http://127.0.0.1:11435 (/v1/chat/completions, /v1/models, /health)

# 3. stop it
./engine-mlx/stop-server.sh
```

If you don't have a prebuilt binary, point `ENGINE_MLX_DIR` at a clone of the
[`engine-mlx`](https://github.com/dangranaz/engine-mlx) repo and the script runs
it via `cargo` with the `mlx` feature.

Config via env: `MODEL`, `HOST` (default `127.0.0.1`), `PORT` (default `11435`),
`ENGINE_MLX_BIN` (prebuilt binary), `ENGINE_MLX_DIR` (engine-mlx repo).
