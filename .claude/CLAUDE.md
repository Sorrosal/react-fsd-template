# React Spark Template — Project Context

## Overview
Professional template for React SPA using Feature-Sliced Design (FSD), React 19, strict TypeScript, Vite, shadcn/ui, Tailwind CSS v4, TanStack Query, and Zustand.

## Architecture: Feature-Sliced Design

### Layers (highest to lowest level)
1. `app` — initialization, providers, router, global styles
2. `pages` — composition of widgets and features per route
3. `widgets` — composed UI blocks (header, sidebar)
4. `features` — user actions (auth, notifications)
5. `entities` — business objects (user, product)
6. `shared` — reusable infrastructure (api, hooks, ui, config, lib, types)

### STRICT Import Rules
- Layers may ONLY import from layers below them: app → pages → widgets → features → entities → shared
- NEVER cross-import between slices in the same layer (features/auth MUST NOT import from features/notifications)
- ALWAYS import from the barrel `index.ts`, NEVER from internal files of another slice
- `shared` MUST NOT import from any other layer

### Slice Structure
Every slice (feature, entity, widget) follows this internal structure:
```
slice-name/
├── ui/          # React components
├── model/       # Store (Zustand), types, schemas (Zod)
├── api/         # HTTP calls (TanStack Query hooks + Axios)
├── lib/         # Internal helpers for this slice
└── index.ts     # Barrel export — PUBLIC API only
```

## Tech Stack
- React 19 + TypeScript (strict: true, noUncheckedIndexedAccess: true)
- Vite 8 with SWC
- React Router v7 (SPA mode, lazy loading on all pages)
- TanStack Query v5 (server state)
- Zustand v5 (client state: auth, sidebar)
- shadcn/ui (New York style) + Tailwind CSS v4
- React Hook Form + Zod v4 (forms and validation)
- Axios (centralized instance with interceptors)
- Vitest + React Testing Library

## Code Conventions

### TypeScript
- ZERO `any` — use `unknown` + narrowing
- ZERO `@ts-ignore` or `@ts-expect-error`
- ZERO non-null assertions (`!`) without documented justification
- `interface` for object shapes and component props
- `type` for unions, intersections, and utility types
- `as const` instead of `enum`
- `import type` when importing types only
- Zod schemas as source of truth → derive types with `z.infer<>`
- Discriminated unions to model complex states

### React
- Components as function declarations (`function`, not arrow functions or `React.FC`)
- Props destructured in the signature with explicit interface
- Named exports always (except default export on pages for lazy loading)
- NO `useEffect` to derive state — use computed variables
- `useMemo`/`useCallback` only when there's a measurable reason
- Early returns for loading/error/empty states
- Separate server state (TanStack Query) from client state (Zustand)

### Files and Naming
- Components: PascalCase (`UserCard.tsx`)
- Hooks: camelCase with `use` prefix (`use-debounce.ts`)
- Stores: kebab-case with `.store.ts` suffix (`auth.store.ts`)
- Schemas: kebab-case with `.schemas.ts` suffix (`auth.schemas.ts`)
- API files: kebab-case with `.api.ts` suffix (`user.api.ts`)
- Types: kebab-case with `.types.ts` suffix (`user.types.ts`)
- Tests: `__tests__/name.test.ts` inside their folder
- Always use `@/` alias for imports — never relative imports going up more than one level

### Styles
- Tailwind utility classes as primary method
- `cn()` helper (clsx + twMerge) for conditional classes
- NO CSS modules or styled-components
- shadcn/ui as the base UI component library in `shared/ui/`

## Routes
- Public: `/`, `/login`, `/register`
- Protected (AuthGuard): `/dashboard`, `/settings`
- Catch-all: `*` → NotFoundPage
- All pages use lazy loading via React Router `lazy()`

## Environment Variables
- `VITE_API_URL` — API base URL (required)
- `VITE_APP_NAME` — App name (default: "React Spark")
- Validated at runtime with Zod in `src/shared/config/env.ts`

## Project Commands
- `npm run dev` — Development server
- `npm run build` — Production build
- `npm run preview` — Preview build
- `npm run lint` — Lint with ESLint
- `npm run format` — Format with Prettier
- `npm run test` — Tests with Vitest
- `npm run test:ui` — Vitest UI
