# Create New Feature

Create a new feature slice at `src/features/$ARGUMENTS` following Feature-Sliced Design.

## Structure to generate:
```
src/features/$ARGUMENTS/
├── ui/
│   └── (main component in PascalCase).tsx
├── model/
│   ├── $ARGUMENTS.store.ts       # Zustand store if state is needed
│   └── $ARGUMENTS.schemas.ts     # Zod validation schemas
├── api/
│   └── $ARGUMENTS.api.ts         # TanStack Query hooks + Axios calls
└── index.ts                       # Barrel export with PUBLIC API only
```

## Rules:
- Main component uses function declaration, not arrow function or React.FC
- Props with explicit interface
- Named exports everywhere
- Zustand store uses the slice pattern with explicit types
- Zod schemas are the source of truth for types (use z.infer)
- API hooks use useQuery/useMutation from TanStack Query
- index.ts ONLY exports what other layers need to consume
- NEVER import from other features — only from entities and shared
