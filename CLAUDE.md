# open-notebook-launcher

## Project Purpose

Launcher for [Open Notebook](https://github.com/lfnovo/open-notebook) — an open-source alternative to NotebookLM for managing AI-powered research notebooks. This repo provides the Docker Compose configuration and Bun scripts to run Open Notebook locally with a SurrealDB backend.

## Architecture

Two Docker services defined in `docker-compose.yml`:

- **surrealdb** — SurrealDB v2 database (port 8000, RocksDB storage)
- **open_notebook** — Open Notebook app (web UI port 8502, API port 5055)

## Common Commands

```bash
bun start   # Start Docker services + open browser
bun docker  # docker compose up -d
bun open    # Open http://localhost:8502 in browser
```

## Data Volumes

- `./notebook_data/` — app data (uploads, SQLite DB, tiktoken cache)
- `./surreal_data/` — SurrealDB persistence

## Key Files

- `docker-compose.yml` — service definitions, environment config, volume mounts
- `package.json` — Bun scripts

## Notes

- The encryption key in `docker-compose.yml` is for local development only; change it for any non-local deployment.
- SurrealDB credentials (root/password) are also dev-only defaults.
- `open_notebook` service uses `pull_policy: always` to stay on the latest image.
