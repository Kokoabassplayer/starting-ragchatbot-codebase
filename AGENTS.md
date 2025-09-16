# Repository Guidelines

## Project Structure & Module Organization
- `backend/` FastAPI RAG services: `app.py`, `rag_system.py`, `vector_store.py`, `document_processor.py`, `ai_generator.py`, `search_tools.py`, `session_manager.py`.
- `frontend/` static UI: `index.html`, `script.js`, `style.css` (served by FastAPI root).
- `docs/` course transcripts auto‑ingested on startup.
- Root: `pyproject.toml` (managed by `uv`), `.env.example`, `run.sh`, `README.md`. Create `tests/` for new tests.

## Build, Test, and Development Commands
- `uv sync` — install dependencies and create a virtual env from the lockfile.
- `chmod +x run.sh && ./run.sh` — start backend with auto‑reload; on Windows use Git Bash.
- `cd backend && uv run uvicorn app:app --reload --port 8000` — manual run.
- `uv run python -m pytest -q` — run tests (after adding `pytest`).

## Tooling Rules
- Use `uv` instead of `pip` for all installs and dependency changes (e.g., `uv sync`, `uv add <package>`).
- Use `uv run` to execute Python files and tools; do not call `python` directly (e.g., `uv run python backend/util.py`, `uv run pytest`).

## Coding Style & Naming Conventions
- Python: PEP 8, 4‑space indentation, add type hints where helpful.
- Names: modules `snake_case.py`, classes `PascalCase`, functions/vars `snake_case`, constants `UPPER_SNAKE_CASE`.
- Keep `app.py` endpoints thin; delegate logic to services (e.g., `rag_system.py`) and pass configuration via `config.py`.

## Testing Guidelines
- Framework: `pytest`. Place tests under `tests/` mirroring modules (e.g., `tests/test_rag_system.py`).
- Use fakes/mocks: stub Anthropic and Chroma calls; avoid network and real API keys.
- Focus coverage on chunking/parsing in `document_processor.py` and filtering/search in `vector_store.py`.

## Commit & Pull Request Guidelines
- Commits: imperative, scoped, present tense (e.g., `Add lesson filter to search`).
- PRs: clear description, linked issues, verification steps (`uv sync`, `./run.sh`), screenshots for UI changes, and notes on new files in `docs/` or config changes.

## Security & Configuration Tips
- Copy `.env.example` to `.env`; set `ANTHROPIC_API_KEY`. Never commit secrets.
- Keep sensitive or large data out of `docs/`. Ensure `.gitignore` covers local ChromaDB paths (`CHROMA_PATH`).
