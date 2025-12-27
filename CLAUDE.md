# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
pnpm dev          # Start dev server with HMR
pnpm build        # Production build to dist/
pnpm preview      # Preview production build
pnpm check        # Type-check Svelte and TypeScript
pnpm lint         # Run ESLint on src/
pnpm lint:fix     # Auto-fix lint issues
pnpm format       # Format with Prettier
pnpm format:check # Check formatting
```

## Architecture

Static single-page therapy website built with Svelte 5 + Vite + TypeScript.

**Entry point:** `src/main.ts` mounts `App.svelte` to `#app`

**Page sections** are composed in `App.svelte` from components in `src/lib/components/`:
- Navigation, Hero, About, Gallery, Specialties, Contact

**Styling:** Global styles in `src/app.css`, component-scoped styles in `<style>` blocks.

No routing, no backend, no environment variables required.
