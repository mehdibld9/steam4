---
name: Vite envDir when root is a subdirectory
description: Vite root set to a subfolder (e.g. client/) stops it from reading a project-root .env file unless envDir is set explicitly
---

When `vite.config.ts` sets `root` to a subdirectory (e.g. `client`), Vite's env file loading defaults to that same directory, not the project root. If `.env` lives at the project root (common in fullstack Express+Vite templates), `VITE_*` vars silently fail to load client-side, throwing "Missing env variable" type errors at runtime.

**Why:** Vite's `envDir` option defaults to `root`. Fullstack templates often keep `root: "client"` for the frontend but keep a single `.env` at the repo root shared with the backend.

**How to apply:** If a project's `.env` is at the repo root but `vite.config.ts` sets `root` to a subfolder, add `envDir: path.resolve(import.meta.dirname)` (pointing at the repo root) to the Vite config.
