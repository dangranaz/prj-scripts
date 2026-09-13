# prj-scripts

**prj-scripts** are simple, user-facing scripts to run the published engines —
start and stop a server without needing to know the internals. Point them at a
model, get an OpenAI-compatible endpoint on your machine.

> [!IMPORTANT]
> These are convenience wrappers for **end users**. They auto-detect the
> Homebrew MLX prefixes, wait for the server to be healthy, and manage a PID
> file — so "start" and "stop" are one command each. For the engine itself see
> [engine-mlx](https://github.com/dangranaz/engine-mlx).

---

## Layout

```
prj-scripts/
└── engine-mlx/
    ├── start-server.sh    ← bring the engine-mlx server up on a model
    └── stop-server.sh     ← stop it
```

---

## Requirements

- **macOS on Apple Silicon**.
- The MLX C API: `brew install mlx-c`.
- Either a prebuilt `engine-mlx-serve` binary, or a clone of the
  [engine-mlx](https://github.com/dangranaz/engine-mlx) repo (the script can run
  it via `cargo`).

---

## Quick start (engine-mlx)

```sh
# 1. install the MLX C API
brew install mlx-c

# 2. start the server on a model directory (must contain config.json)
./engine-mlx/start-server.sh /path/to/Qwen3-1.7B-MLX-4bit
#    → serves http://127.0.0.1:11435
#      (/v1/chat/completions, /v1/models, /health)

# 3. stop it
./engine-mlx/stop-server.sh
```

If you don't have a prebuilt binary, point `ENGINE_MLX_DIR` at a clone of the
engine-mlx repo and the script runs it via `cargo` with the `mlx` feature.

---

## Configuration (env)

| Variable         | Default          | Meaning                                   |
|------------------|------------------|-------------------------------------------|
| `MODEL`          | (required)       | Model directory (contains `config.json`)  |
| `HOST`           | `127.0.0.1`      | Bind host                                 |
| `PORT`           | `11435`          | Bind port                                 |
| `ENGINE_MLX_BIN` | —                | Path to a prebuilt `engine-mlx-serve`     |
| `ENGINE_MLX_DIR` | `~/engine-mlx`   | Path to the engine-mlx repo (cargo run)   |
| `READY_TIMEOUT`  | `300`            | Seconds to wait for `/health`             |

---

## Related

- [engine-mlx](https://github.com/dangranaz/engine-mlx) — the inference engine.
- [prj-bench](https://github.com/dangranaz/prj-bench) — benchmark a running server.

## ⭐ Support the project

If these scripts make running engine-mlx easier for you, please **give the
repository a star** and share it. Feedback and suggestions are very welcome.

## License

MIT.
