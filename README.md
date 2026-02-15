# open-notebook-launcher

Local launcher for [Open Notebook](https://github.com/lfnovo/open-notebook) — an open-source alternative to NotebookLM for AI-powered research notebooks.

## What is Open Notebook?

Open Notebook lets you create notebooks around topics, add sources (web pages, PDFs, text, YouTube videos), and interact with them via AI-powered chat and podcast generation — similar to Google's NotebookLM but self-hosted and open-source.

## Requirements

- [Docker](https://www.docker.com/) with Docker Compose
- [Bun](https://bun.sh/) (for launch scripts)

## Getting Started

```bash
bun start
```

This starts the Docker services and opens the web UI at `http://localhost:8502`.

### Individual commands

```bash
bun docker  # Start services in the background (docker compose up -d)
bun open    # Open the web UI in your browser
```

## Services

| Service | Port | Description |
|---------|------|-------------|
| Open Notebook UI | 8502 | Web interface |
| Open Notebook API | 5055 | REST API |
| SurrealDB | 8000 | Database backend |

## Data

All data is persisted locally:

- `./notebook_data/` — notebooks, uploads, and app data
- `./surreal_data/` — SurrealDB database

## Configuration

Environment variables for Open Notebook are set in `docker-compose.yml`:

| Variable | Default | Description |
|----------|---------|-------------|
| `OPEN_NOTEBOOK_ENCRYPTION_KEY` | `locally_running_safe_setup` | Key for credential encryption — **change for non-local use** |
| `SURREAL_URL` | `ws://surrealdb:8000/rpc` | SurrealDB connection URL |
| `SURREAL_USER` | `root` | SurrealDB username |
| `SURREAL_PASSWORD` | `password` | SurrealDB password — **change for non-local use** |
| `SURREAL_NAMESPACE` | `open_notebook` | SurrealDB namespace |
| `SURREAL_DATABASE` | `open_notebook` | SurrealDB database name |

## Stopping

```bash
docker compose down
```

To also remove persisted data:

```bash
docker compose down -v
rm -rf notebook_data surreal_data
```
