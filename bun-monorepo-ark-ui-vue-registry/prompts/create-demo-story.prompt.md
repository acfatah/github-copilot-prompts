---
agent: agent
---

# Create Demo Story

Create a `Demo{ComponentName}Story.vue` that showcases the component in a
realistic, real-world context — not just isolated prop variations.

Add it as a `Demo` named export in the existing `{ComponentName}.stories.ts`.

## Goal

A demo story answers: "What does this component look like in actual use?"
It should feel like a UI fragment from a real product, not a component catalog.

## Examples of Good Demo Contexts

| Component | Demo idea |
|---|---|
| Button | Form submit button inside a login card |
| Dialog | "Delete account" confirmation dialog |
| Select | Country selector inside a settings form |
| Tabs | Dashboard layout with content panels |
| Toast/Sonner | Notification triggered by a form action |
| Checkbox | Cookie consent banner |
| Tooltip | Icon button with descriptive tooltip |
| Card | Product listing card with image and actions |

## Demo Story Vue File

```vue
<script setup lang="ts">
import { ref } from 'vue'
import { Button } from '@/components/ui/button'
import { ComponentName } from '@/components/ui/component-name'
// Import other components needed for the realistic context
</script>

<template>
  <div class="flex min-h-[200px] items-center justify-center p-8">
    <!-- Realistic usage in context -->
  </div>
</template>
```

## Wiring into .stories.ts

```ts
import DemoComponentNameStory from './DemoComponentNameStory.vue'
import DemoComponentNameSource from './DemoComponentNameStory.vue?raw'

export const Demo: Story = {
  name: 'Demo',
  parameters: {
    docs: { source: { code: DemoComponentNameSource } },
  },
  render: () => ({
    components: { DemoComponentNameStory },
    template: html`<DemoComponentNameStory />`,
  }),
}
```

## Steps

1. Read the existing component files to understand its API.
2. Read `{ComponentName}.stories.ts` to see current exports and avoid duplication.
3. Design a realistic scenario that shows the component's primary use case.
4. Create `Demo{ComponentName}Story.vue` with the scenario.
5. Add the `Demo` export to `.stories.ts`.
6. Run `bun format apps/storybook/stories/ui/{component-name}/` when done.

## Notes

- Keep the demo self-contained: use `ref()` for local state, no external stores.
- Use other registry components (Button, Card, Input, etc.) to build context.
- Wrap the demo in a centered container so it renders well in the docs panel.
- Do not pass `args` to the Demo render function — it should be opinionated.
- Demo stories are placed last in the `.stories.ts` export list.
