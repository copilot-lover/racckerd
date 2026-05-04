# Unified Platform Integration Plan (MVP)

## Phase A — Repository Acquisition
All repositories listed in `links.md` were downloaded into `repos/`:
- `repos/openwork`
- `repos/open-design`
- `repos/nanobrowser`
- `repos/open-webui`

## Phase B — Architecture Map

### 1) openwork
- **Language/Framework:** TypeScript-heavy monorepo with React/Next-style frontend packages and Rust components.
- **Likely role:** coding agent + project workspace + orchestration patterns.
- **Entrypoints:** `package.json` scripts at repo root; architecture docs exist (`ARCHITECTURE.md`).
- **Integration seam:** adapter for coding agent execution + project-level state.

### 2) open-design
- **Language/Framework:** TypeScript + React + HTML/CSS assets; design-oriented app structure.
- **Likely role:** design tool integration and UI pattern source.
- **Entrypoints:** `package.json` scripts; quickstart docs.
- **Integration seam:** design adapter + reusable UI primitives.

### 3) nanobrowser
- **Language/Framework:** TypeScript/TSX browser automation app.
- **Likely role:** browser automation adapter and execution runtime.
- **Entrypoints:** `package.json` scripts.
- **Integration seam:** tool adapter for browser tasks with structured action/result API.

### 4) open-webui
- **Language/Framework:** Python backend + Svelte frontend.
- **Likely role:** base unified chat runtime (streaming, session history, providers).
- **Entrypoints:** Python app and frontend build scripts in root `package.json` and backend config.
- **Integration seam:** core chat shell, provider abstraction extension points, memory/RAG pipeline.

## Phase C — Target Unified System

### Proposed folder structure

```txt
platform/
  adapters/
    browser/
    coding/
    cua/
    design/
  orchestration/
    intent-router/
    execution-tracker/
  memory/
    short-term/
    long-term/
    rag/
  ui/
    switcher/
    chat/
    projects/
  providers/
  config/
```

### Layer mapping
- **Core layer:** provider abstraction + config + session/auth hooks built around open-webui backend interfaces.
- **Chat layer:** open-webui frontend/backend as primary shell.
- **Tool layer:** adapter wrappers to call openwork/nanobrowser/open-design capabilities.
- **Memory layer:** open-webui retrieval pipeline as base; project memory keys from openwork project identities.
- **Orchestration layer:** intent router decides adapter usage; execution tracker normalizes tool state.
- **UI layer:** unified switcher and project nav mounted in chat shell.

## Phase D — Smallest Safe Integration Layer Implemented

Implemented in this repository as design+architecture deliverables (non-breaking, reversible):
1. Created this integration blueprint file.
2. Created a switcher UI spec that maps image cues into concrete component behavior.
3. Created a repo inventory + command catalog for reproducible analysis.

No upstream repository code was modified yet; this avoids breaking each project before adapter contracts are locked.

## Phase E/F — Validation and Fixes
- Verified downloads and extracted repos.
- Verified inventory scripts and architecture scan command outputs.

## Phase G — Switcher UI (image-matching implementation notes)
From reference images, the switcher should be:
- compact segmented control, three tabs (`Chat`, `Code`, `Cowork`)
- soft gray container background
- small horizontal padding and low-height pills
- active segment appears white with subtle border/shadow
- typography: understated, medium-small weight and size
- roundness: outer radius and inner selected radius visibly rounded, not full pills
- spacing rhythm: equal tab widths, centered labels, minimal vertical height

## Phase H — Documentation
This file plus `REPO_ARCHITECTURE_MAP.md` and `SWITCHER_UI_SPEC.md` document acquisition, mapping, target architecture, risks, and remaining work.

## Risks / Tradeoffs
- Different stacks (Svelte + React + Rust + Python) require adapter boundaries, not deep merge.
- Premature code merge would create high breakage risk and poor upgradeability.
- UI parity with image requires implementing switcher in chosen host frontend (recommended: open-webui frontend shell first).

## Remaining Work
1. Add concrete adapter contracts (JSON schemas) and mock runtimes.
2. Implement orchestration router service.
3. Embed switcher component into selected host frontend.
4. Wire memory/project identity to chat sessions.
5. Add end-to-end tests for chat->route->adapter->response loop.
