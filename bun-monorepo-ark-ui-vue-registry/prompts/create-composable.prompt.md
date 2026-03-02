---
agent: agent
---

# Create Composable

Create a Vue composable in `packages/registry/src/composables/` following project
conventions. Use `kebab-case` for the file name (e.g., `use-example.ts`).

## Conventions

- File name: `kebab-case` (e.g., `use-forward-props.ts`)
- Function name: `camelCase` prefixed with `use` (e.g., `useForwardProps`)
- Export as named export (not default)
- Full TypeScript — define generics and return types explicitly
- No side-effectful imports (no auto-importing from VueUse unless necessary)

## Pattern

```ts
import type { Ref } from 'vue'
import { computed, toValue } from 'vue'

/**
 * Brief description of what this composable does.
 *
 * @param input - description of the parameter
 * @returns description of the return value
 */
export function useExample<T>(input: Ref<T> | T) {
  const value = computed(() => toValue(input))

  return {
    value,
  }
}
```

## Existing Composables (do not duplicate)

- `create-context.ts` — typed provide/inject factory (`createContext<T>`)
- `dynamic.ts` — dynamic component resolution
- `use-forward-props.ts` — forward props to child with `useForwardProps`
- `use-id.ts` — generate stable unique IDs

## Steps

1. Determine if an existing composable or VueUse utility covers the need.
2. Create the file in `packages/registry/src/composables/`.
3. Write the composable with full TypeScript types and a JSDoc comment.
4. If the composable should be part of the registry (installable), add it to
   the relevant `_registry.ts` `files` array.
5. Run `bun format packages/registry/src/composables/{file}` when done.

## Notes

- Prefer `computed()` over `watchEffect()` for derived reactive values.
- Use `toValue()` (Vue 3.3+) instead of `unref()` to handle both refs and
  plain values.
- Use `context7` to verify Vue Composition API patterns and VueUse utilities.
