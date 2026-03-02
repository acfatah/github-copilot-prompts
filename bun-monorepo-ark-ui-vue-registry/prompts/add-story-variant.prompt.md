---
agent: agent
---
# Add Story Variant

Add one or more named story variants to an existing component story folder in
`apps/storybook/stories/ui/{component-name}/`.

## What This Does

- Creates a new `{Description}{ComponentName}Story.vue` file
- Wires it up as a named export in the existing `{ComponentName}.stories.ts`

## Variant Story Vue File

```vue
<script setup lang="ts">
import { ComponentName } from '@/components/ui/component-name'
</script>

<template>
  <div class="flex flex-wrap gap-4">
    <!-- Demonstrate the variant here -->
    <ComponentName.Root variant="outline">Outline</ComponentName.Root>
    <ComponentName.Root variant="ghost">Ghost</ComponentName.Root>
  </div>
</template>
```

## Wiring into .stories.ts

Add the import and a new named export at the bottom of the existing stories file:

```ts
import VariantComponentNameStory from './VariantComponentNameStory.vue'
import VariantComponentNameSource from './VariantComponentNameStory.vue?raw'

export const Variant: Story = {
  name: 'Variant Name',
  parameters: {
    docs: { source: { code: VariantComponentNameSource } },
  },
  render: args => ({
    components: { VariantComponentNameStory },
    setup() { return { args } },
    template: html`<VariantComponentNameStory v-bind="args" />`,
  }),
}
```

## Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Vue file | `{Description}{ComponentName}Story.vue` | `SizeButtonStory.vue` |
| Export name | PascalCase description | `export const Size` |
| Story name | Human-readable label | `name: 'Sizes'` |

## Steps

1. Read the existing `{ComponentName}.stories.ts` to understand current exports.
2. Read the existing story Vue files to match the style and import patterns.
3. Create the new `{Description}{ComponentName}Story.vue`.
4. Add the import and named export to `.stories.ts`.
5. Run `bun format apps/storybook/stories/ui/{component-name}/` when done.

## Notes

- Import the `?raw` source for the docs code panel — always include it.
- Keep story components self-contained: no external data files unless the
  component already uses one (e.g., `items.ts`).
- Use `html` from `common-tags` for the render template string.
- Do not add `args` to individual story exports — define them in `meta` only.
