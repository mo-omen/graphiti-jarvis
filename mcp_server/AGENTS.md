# Repository Guidelines

## Project Structure & Module Organization
Source code lives in `src/`, with configuration models in `src/config/`, request and domain models in `src/models/`, service integrations in `src/services/`, and shared helpers in `src/utils/`. The entrypoint is `main.py`. Tests live in `tests/`, with shared fixtures in `tests/conftest.py`. Operational docs are in `docs/`, local config examples belong in `config/`, and Docker assets for FalkorDB and Neo4j are under `docker/`.

## Build, Test, and Development Commands
Use `uv` for local development.

- `uv sync --extra dev`: install runtime and development dependencies.
- `uv run pytest`: run the full test suite.
- `uv run pytest tests/test_<feature>.py`: run a focused test module.
- `uv run ruff check src tests`: run lint checks.
- `uv run ruff format src tests`: apply formatting.
- `uv run pyright`: run static type checks.
- `docker compose up`: start the default local stack.
- `docker compose -f docker/docker-compose-neo4j.yml up`: run against Neo4j instead of FalkorDB.

## Coding Style & Naming Conventions
Target Python 3.10+ with 4-space indentation and a 100-character line limit. `ruff format` enforces single quotes and spacing. Use `snake_case` for modules, functions, and variables; use `PascalCase` for classes and Pydantic models. Keep orchestration logic in `src/services/` and push reusable helpers into `src/utils/`.

## Testing Guidelines
Tests use `pytest`, `pytest-asyncio`, and shared fixtures from `tests/conftest.py`. Name files `test_<feature>.py` and test functions `test_<behavior>`. Add regression tests for bug fixes and prefer targeted runs while iterating, for example `uv run pytest -k search`. Run the full suite before opening a PR.

## Commit & Pull Request Guidelines
Follow the existing history: concise imperative commit subjects such as `Harden search filters against Cypher injection (#1312)`. Keep commits focused and avoid mixing refactors with behavior changes. PRs should include a clear description, linked issue or context, configuration or API impact notes, and logs or screenshots when behavior changes are visible to users.

## Configuration & Security Tips
Do not commit secrets or local API keys. Keep runtime settings in local config files or environment variables, and verify database and model provider settings before running integration flows.
