# Soc Ops — Social Bingo (React 19 + TypeScript + Tailwind v4)

## Development Checklist (mandatory after every change)
- [ ] `npm run lint`
- [ ] `npm run build`
- [ ] `npm test`

## Architecture
Single-page app, no router. `GameState: 'start' | 'playing' | 'bingo'` drives screen switching. Hook `useBingoGame` owns all state + localStorage persistence. Pure logic in `src/utils/bingoLogic.ts`. Components are presentational. Types in `src/types/index.ts`. 24 prompts in `src/data/questions.ts`.

## Conventions
- **Tailwind v4** — `@theme` tokens in `src/index.css`, no `tailwind.config.js`. See `.github/instructions/tailwind-4.instructions.md`.
- **Strict TS** — `strict`, `noUnusedLocals`, `noUnusedParameters`, `verbatimModuleSyntax`
- **Named exports** for components; default export only for `App`
- **Props interfaces** co-located in component files, not in `types/`
- **Immutable updates** — `board.map(...)`, spread; no mutation
- **Tests** — pure logic in `src/utils/*.test.ts` (Vitest); components via `@testing-library/react`
- **Mobile-first** — touch targets `min-h-[60px]`, `active:` states, tap-highlight disabled

## Key Patterns
Board is flat 25-element array; index 12 = free space. Win detection checks 12 lines. `queueMicrotask` in `handleSquareClick` avoids synchronous setState during render. State persisted to localStorage with version validation.

## Deployment
GitHub Pages via `.github/workflows/deploy.yml` on push to `main`. Base path from `VITE_REPO_NAME` env var.
