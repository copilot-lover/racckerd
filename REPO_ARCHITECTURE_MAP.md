# Repository Architecture Map

## Source list
Parsed from `links.md`.

## Inventory summary

### openwork (`repos/openwork`)
- Predominant languages: TypeScript, TSX, Markdown, some Rust.
- Key config signals: `package.json`, architecture/product markdown docs.
- Likely concerns: coding workflows, workspace/project context, orchestration helpers.
- Integration seam candidates:
  - coding execution adapter
  - project context adapter
  - optional Rust-native performance modules via process boundary

### open-design (`repos/open-design`)
- Predominant languages: TypeScript, HTML, CSS, UI assets.
- Key config signals: `package.json`, quickstart/contributing docs.
- Likely concerns: design tooling and collaborative design UX.
- Integration seam candidates:
  - design adapter interface
  - asset/prompt bridge for design tasks from chat

### nanobrowser (`repos/nanobrowser`)
- Predominant languages: TypeScript/TSX.
- Key config signals: `package.json`, environment templates.
- Likely concerns: browser automation and web task execution.
- Integration seam candidates:
  - browser action API (`navigate`, `extract`, `click`, `summarize`)
  - execution status stream back into unified chat UI

### open-webui (`repos/open-webui`)
- Predominant languages: Svelte (frontend), Python (backend), TS utilities.
- Key config signals: `pyproject.toml`, `package.json`, `.env.example`.
- Likely concerns: chat UX, provider support, memory/RAG foundations, user/session model.
- Integration seam candidates:
  - host shell for unified chat
  - extend tool-calls panel for external adapters
  - central auth/session + conversation persistence

## Recommended host strategy
Use **open-webui** as the primary host application for MVP integration due to:
1. Existing mature chat shell.
2. Existing backend/frontend split for routing and streaming.
3. Natural location for provider abstraction and memory integration.

## Adapter-first integration principle
Keep each external system independently upgradable:
- integrate through typed adapters and process/API boundaries.
- avoid direct code copy unless licensing/maintenance plan is explicit.
- maintain source separation under `repos/` for repeatable updates.
