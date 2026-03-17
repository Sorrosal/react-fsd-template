# Create New Widget

Create a new widget slice at `src/widgets/$ARGUMENTS` following Feature-Sliced Design.

## Structure to generate:
```
src/widgets/$ARGUMENTS/
├── ui/
│   └── (main component in PascalCase).tsx
├── model/
│   └── $ARGUMENTS.store.ts       # Zustand store if local UI state is needed
└── index.ts                       # Barrel export
```

## Rules:
- Widgets are composed UI blocks: Header, Sidebar, Footer, DataTable, etc.
- They compose features and entities to create page sections
- They may have their own UI state (collapsed, expanded) in Zustand
- They may import from features, entities, and shared
- NEVER import from pages
- Must be responsive (mobile 320px+ and desktop)
