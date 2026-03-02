---
agent: agent
---

# Migrate Component

Update one or more components in `packages/registry/src/components/ui/` to
conform to the current conventions. Read `CLAUDE.md` and `create-component.md`
first to understand the target patterns.

## Current Conventions to Enforce

### 1. Data Attributes

Replace `data-slot` with the two-attribute pattern:

```diff
- data-slot="trigger"
+ data-scope="accordion" data-part="trigger"
```

- `data-scope` = component name in kebab-case (matches the Ark UI component name
  or a custom name for non-Ark components)
- `data-part` = the sub-element role in kebab-case

### 2. Props Interface

Move inline prop types to a typed `Props` interface if not already done:

```diff
- defineProps<{ class?: HTMLAttributes['class']; size?: 'sm' | 'md' }>()
+ interface Props {
+   class?: HTMLAttributes['class']
+   size?: 'sm' | 'md'
+ }
+ defineProps<Props>()
```

### 3. Variant Definitions

If a component has `cva()` variants defined inline in the `.vue` file, move them
to `index.ts` (or a dedicated `variant.ts`) and import them:

```diff
- // inside Button.vue
- const buttonVariants = cva(...)
+ // in index.ts
+ export const buttonVariants = cva(...)
```

### 4. Namespace Exports

If a complex component has no `namespace.ts`, create one using `/create-namespace-file`.
If `index.ts` does not re-export the namespace object, add it.

### 5. _registry.ts

If `_registry.ts` is missing or outdated, use `/create-underscore-registry` to
create or update it.

### 6. Import Order

Ensure imports follow the project's alphabetized order (enforced by ESLint):
1. Type imports (`import type ...`)
2. External packages
3. Internal aliases (`@/...`)
4. Relative imports (`./...`)

## Steps

1. Read all `.vue` files and `index.ts` in the given component directory.
2. Identify which conventions above are violated.
3. Apply fixes file by file, smallest change first.
4. If a `namespace.ts` is missing, run `/create-namespace-file`.
5. If `_registry.ts` is missing or stale, run `/create-underscore-registry`.
6. Run `bun format {component-directory}` as the final step.
7. Run `bun run typecheck` from `packages/registry` to verify no type errors.

## Notes

- Do not change component behavior — only update structure and naming.
- Use `context7` to verify Ark UI prop names before renaming.
- If unsure whether a `data-scope` name is correct, check the existing component
  styles in `src/styles/global.css` for matching selectors.
