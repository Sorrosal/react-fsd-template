# Create New Entity

Create a new entity slice at `src/entities/$ARGUMENTS` following Feature-Sliced Design.

## Structure to generate:
```
src/entities/$ARGUMENTS/
├── ui/
│   └── (presentational components for the entity).tsx
├── model/
│   └── $ARGUMENTS.types.ts       # Main interface and related types
├── api/
│   └── $ARGUMENTS.api.ts         # TanStack Query hooks (queries, not mutations)
└── index.ts                       # Barrel export
```

## Rules:
- Entities are business objects: User, Product, Order, etc.
- Their UI components are purely presentational (no business logic)
- Types are defined as interfaces (extensible)
- API hooks are queries only (GET). Mutations belong in features.
- ONLY imports from shared. NEVER from features, widgets, or pages.
- NEVER import from other entities.
