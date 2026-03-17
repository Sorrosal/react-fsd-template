# Add API Endpoint

Add a new endpoint to the API file of the slice specified in $ARGUMENTS (format: `layer/slice endpoint-name`).

## Actions:
1. Add the HTTP call function using the Axios instance (`@/shared/api/axios-instance`)
2. Create the corresponding TanStack Query hook:
   - `useQuery` for GET (queries)
   - `useMutation` for POST/PUT/PATCH/DELETE (mutations)
3. Define Request and Response types as interfaces
4. If there's a request body, create a Zod schema and derive the type with `z.infer`
5. Export the hook from the slice's `index.ts`

## Rules:
- ALWAYS explicitly type request and response
- Query keys as constants: `const userKeys = { all: ['users'], detail: (id: string) => ['users', id] }`
- Mutations must invalidate related queries in `onSuccess`
- Handle errors with the `ApiError` type from `@/shared/api/api-error`
