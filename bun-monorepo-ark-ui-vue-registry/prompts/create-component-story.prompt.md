---
agent: agent
---

# Creating Storybook Stories for Vue Components

## File Structure

Stories go in `apps/storybook/stories/ui/{component-name}/`:
- `{ComponentName}.stories.ts` - Story meta and exports
- `{ComponentName}DefaultStory.vue` - Default story implementation
- `{Description}{ComponentName}Story.vue` - Additional variants
- `items.ts` - Data records for complex stories (when needed)

## Story File Structure

```ts
import type { Meta, StoryObj } from '@storybook/vue3-vite'
import { html } from 'common-tags'

import { ComponentName } from '@/components/ui/component-name'
import { registryItem } from '@/components/ui/component-name/_registry'
import ComponentNameDefaultStory from './ComponentNameDefaultStory.vue'
import ComponentNameDefaultSource from './ComponentNameDefaultStory.vue?raw'

const meta = {
  title: 'Components/ComponentName',
  component: ComponentName,
  tags: ['autodocs'],
  parameters: {
    docs: {
      description: { component: registryItem.description },
    },
  },
} satisfies Meta<typeof ComponentName>

export default meta
type Story = StoryObj<typeof meta>

export const Default: Story = {
  parameters: {
    docs: { source: { code: ComponentNameDefaultSource } },
  },
  render: args => ({
    components: { ComponentNameDefaultStory },
    setup() { return { args } },
    template: html`<ComponentNameDefaultStory v-bind="args" />`,
  }),
}
```

## Story Vue File

```vue
<script setup lang="ts">
import { Component } from '@/components/ui/component-name'

const storyArgs = defineProps<{
  prop1: string
  prop2: boolean
}>()
</script>

<template>
  <Component.Root :prop1="storyArgs.prop1">
    <Component.Child :prop2="storyArgs.prop2" />
  </Component.Root>
</template>
```

## Multiple Subcomponents Meta

```ts
import {
  ComponentRoot,
  ComponentItem,
  ComponentTrigger,
  ComponentContent,
} from '@/components/ui/component-name'

const meta = {
  title: 'Components/ComponentName',
  component: ComponentRoot,
  subcomponents: { ComponentItem, ComponentTrigger, ComponentContent },
  tags: ['autodocs'],
  ...
} satisfies Meta<typeof ComponentRoot>
```

## ArgTypes

```ts
argTypes: {
  variant: {
    control: { type: 'select' },
    options: ['default', 'outline'],
    table: {
      type: { summary: 'string' },
      defaultValue: { summary: 'default' },
    },
  },
},
```

## Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Story file | `{ComponentName}.stories.ts` | `Button.stories.ts` |
| Default story | `{ComponentName}DefaultStory.vue` | `ButtonDefaultStory.vue` |
| Variant story | `{Description}{ComponentName}Story.vue` | `SizeButtonStory.vue` |
| Story title | `Components/{ComponentName}` | `Components/Button` |
| Default export | `Default` | `export const Default` |

## Common Pitfalls

- Missing registry item import for component description
- Not importing `?raw` source for docs code panel
- Inconsistent file casing (use PascalCase)
- Defining `args` in stories instead of meta
- Forgetting `subcomponents` in meta for complex components
