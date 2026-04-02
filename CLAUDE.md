# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Trench Coat Goblins - A D&D web application with API backend.

## Tech Stack

- Runtime: Bun
- Language: TypeScript
- API: Hono
- Web: React + Vite
- Deployment: Docker + Jenkins CI/CD

## Commands

```bash
bun install              # Install all workspace dependencies
bun run dev:api          # Run API in dev mode (port 3001)
bun run dev:web          # Run web in dev mode (port 3000)
bun run build            # Build all apps
bun run lint             # Lint all apps
bun run test             # Test all apps
```

## Architecture

Monorepo with Bun workspaces:

```
apps/
├── api/     # Hono API server (port 3001)
└── web/     # React + Vite frontend (port 3000)
```

## Deployment

- Jenkins pipeline triggered on push to main
- Docker Compose orchestrates api and web containers
- Nginx reverse proxy handles routing
