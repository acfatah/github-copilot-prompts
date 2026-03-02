---
agent: agent
---

# Create Context File

Analyze the given component directory (or directories) and create a `context.ts`
file for each that requires shared state across sub-components. Skip all tests.

## When to Use

Create a `context.ts` when:
- A component has multiple sub-parts that need shared state (e.g., Root passes
  options to children)
- Custom props on the Root component must be consumed by descendant components
  without explicit prop drilling
- The component wraps an Ark UI root but needs to expose extra options
  (e.g., `hideArrow`, `orientation`, `collapsible`)

## Pattern (Tooltip example)

```ts
import type { ComputedRef } from 'vue'

import { createContext } from '@/composables/create-context'

export interface TooltipOptions {
  hideArrow?: boolean
}

export const [TooltipOptionsProvider, useTooltipOptions]
  = createContext<ComputedRef<TooltipOptions>>('TooltipOptions')
```

## Usage in Root Component

```vue
<script setup lang="ts">
import { computed } from 'vue'
import { reactiveOmit } from '@vueuse/core'
import { useForwardPropsEmits } from '@/composables/use-forward-props'
import { TooltipOptionsProvider } from './context'

interface Props extends TooltipRootProps {
  class?: HTMLAttributes['class']
  hideArrow?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  hideArrow: false,
})
const emit = defineEmits<TooltipRootEmits>()
const delegatedProps = reactiveOmit(props, ['class', 'hideArrow'])
const forwardedProps = useForwardPropsEmits(delegatedProps, emit)

const options = computed(() => ({
  hideArrow: props.hideArrow,
}))

TooltipOptionsProvider(options)
</script>
```

## Usage in Child Component

```vue
<script setup lang="ts">
import { useTooltipOptions } from './context'

const options = useTooltipOptions()
</script>

<template>
  <div v-if="!options.hideArrow" data-scope="tooltip" data-part="arrow" />
</template>
```

## Steps

1. Identify which custom props on the Root cannot be forwarded to Ark UI.
2. Define an `Options` interface for those props.
3. Export `[Provider, useOptions]` from `createContext`.
4. Update the Root component to compute and provide the context.
5. Update child components to consume the context where needed.
6. Run `bun format {component-directory}` when done.

## Notes

- Always wrap the context value in `computed()` so reactivity is preserved.
- Name the context string after the component (e.g., `'TooltipOptions'`).
- Use `context7` to check Ark UI docs for which props are safe to forward.
