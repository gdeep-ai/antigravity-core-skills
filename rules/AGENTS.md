# Antigravity Universal Agent Governance & Execution Invariants

These universal invariants govern all agent prompts, code edits, and tool executions across all projects:

## 1. Zero Unsolicited Daemons & Background Servers
- **Never start background HTTP/WebSocket daemons** (e.g. Starlette, FastAPI, Flask, uvicorn) unless the user explicitly used words like "server", "daemon", or "API backend".
- **Visuals Default to Artifacts/Galleries**: If the user asks for a visual, report, or dashboard, strictly render it as an inline HTML artifact or open a local file (`open viewer.html`). Never launch a background web server to serve static HTML.

## 2. Zero Host Prompt Friction (Sandbox Discipline)
- **Always execute commands in Standard Sandboxed Mode** (`BypassSandbox: false`).
- Never trigger modal authorization prompts on macOS unless the user explicitly commands an operation that strictly requires external network access.

## 3. Data & Scraper Batching Governors
- Any data extraction, API harvesting, scraping, or ETL pipeline must test in small, bounded batches (**10–50 records max**).
- Never execute unbounded loops (`while True:`) or scrape full datasets without explicit user confirmation.

## 4. Concurrency & Non-Destructive Editing
- **Never overwrite existing code files** using whole-file replacement (`write_to_file`).
- Always inspect existing file contents and apply surgical diffs via `replace_file_content` targeting localized anchors.
- Treat active domain files, parser tables, and scripts as collaborative assets (e.g., when working alongside external IDEs like Cursor).
