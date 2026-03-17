# Create New Page

Create a new page at `src/pages/$ARGUMENTS/` and register it in the router.

## Structure to generate:
```
src/pages/$ARGUMENTS/
└── ${PascalCase($ARGUMENTS)}Page.tsx
```

## Actions:
1. Create the page component with **default export** (required for lazy loading)
2. Add the route in `src/app/router/index.tsx` using `lazy()`
3. If it's a protected route, wrap it in AuthGuard
4. Assign the corresponding layout (AppLayout for authenticated, AuthLayout for auth)

## Rules:
- Pages are the ONLY place where default export is used
- Pages ONLY compose widgets and features, they do not implement their own logic
- Minimal code: import widgets/features and compose them in a layout
- Wrap in Suspense with skeleton fallback
