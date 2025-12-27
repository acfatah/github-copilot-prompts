---
agent: agent
---
# Creating Storybook Stories for Vue Components

## Overview

This document outlines the patterns, conventions, and implementation details for
creating new component stories in the Storybook environment. Follow these guidelines
to maintain consistency and proper documentation across all components.

## File Structure

Stories should be organized in `apps/storybook/stories/` directory with:
- `ui/{component-name}/{ComponentName}.stories.ts` - Main story file
- `ui/{component-name}/{StoryName}.vue` - Individual story implementations
- `ui/{component-name}/items.ts` - Data records for complex stories (when needed)

## Pattern Analysis

### 1. Story File Structure (`ComponentName.stories.ts`)
```ts
import type { Meta, StoryObj } from '@storybook/vue3-vite'
import { html } from 'common-tags'

// Import the main component and its registry item
import { ComponentName } from '@/components/ui/component-name'
import { registryItem } from '@/components/ui/component-name/_registry'

// Import individual story components and their raw source
import StoryName from './StoryName.vue'
import StoryNameSource from './StoryName.vue?raw'

// Define metadata
const meta = {
  title: 'Components/ComponentName',  // Category in Storybook
  component: ComponentName,           // Main component
  tags: ['autodocs'],                 // Enable auto-generated docs

  parameters: {
    docs: {
      description: {
        component: registryItem.description,  // Description from registry
      },
    },
  },

  // Default values for props
  args: {
    prop1: 'defaultValue',
  },

  // Define controls for interactive documentation
  argTypes: {
    variant: {
      control: { type: 'select' },
      options: ['option1', 'option2', 'option3'],
      table: {
        type: { summary: 'string' },
        defaultValue: { summary: 'option1' },
      },
    },
  },
} satisfies Meta<typeof ComponentName>

export default meta
type Story = StoryObj<typeof meta>

// Export stories
export const StoryName: Story = {
  parameters: {
    docs: {
      source: {
        code: StoryNameSource,  // Raw source for documentation
      },
    },
  },

  render: args => ({
    components: { StoryName },
    setup() {
      return { args }
    },
    template: html`
      <StoryName v-bind="args" />
    `,
  }),
}
```

### 2. Story Implementation (`StoryName.vue`)
```vue
<script setup lang="ts">
// Import necessary sub-components from the same component package
import { Component } from '@/components/ui/component-name'
// Import other utilities if needed
import { Icon } from '@iconify/vue'
import { cn } from '@/lib/utils'

// Define props as storyArgs if applicable
const storyArgs = defineProps<{
  prop1: string
  prop2: boolean
}>()
</script>

<template>
  <!-- Implement the story using Ark UI components -->
  <Component.Root :prop1="storyArgs.prop1">
    <Component.Child :prop2="storyArgs.prop2" />
    <Component.Slot />
  </Component.Root>
</template>
```

### 3. Data Records (`items.ts`) - For complex stories

```ts
import { html } from 'common-tags'

export interface ItemRecord {
  value: string
  title: string
  content: string
}

export const items: ItemRecord[] = [
  {
    value: 'item-1',
    title: 'Item Title',
    content: html`
      <p>Content for the story item.</p>
    `,
  },
  // ... more items
]
```

## Naming Conventions

### File Names
- Story file: `{ComponentName}.stories.ts` (e.g., `Button.stories.ts`)
- Default story: `{ComponentName}DefaultStory.vue` (e.g., `ButtonDefaultStory.vue`)
- Additional stories: `{Description}{ComponentName}Story.vue` (e.g., `SizeButtonStory.vue`)

### Story Title Convention
- Components: `Components/{ComponentName}`
- Examples: `Examples/{Category}`

### Export Name Convention
- Default story: `Default` (for the primary example)
- Variants: Descriptive names like `SizeVariants`, `VariantVariants`, `WithIcon`, `Rounded`, etc.
- Special cases: `AsChild`, `Link (asChild)`

## Component Import Patterns

### Single Component Story
```ts
import { ComponentName } from '@/components/ui/component-name'
const meta = {
  component: ComponentName,
}
```

### Multiple Subcomponents Story
```ts
import {
  ComponentRoot,
  ComponentItem,
  ComponentTrigger,
  ComponentContent,
} from '@/components/ui/component-name'

const meta = {
  component: ComponentRoot,
  subcomponents: {
    ComponentItem,
    ComponentTrigger,
    ComponentContent,
  },
}
```

## Documentation and Controls

### ArgTypes Configuration
For each prop, provide:
- Control type ('select', 'radio', 'text', 'boolean', etc.)
- Available options if applicable
- Table configuration showing type and default value

### Parameter Configuration
Always include source code in documentation:
```ts
parameters: {
  docs: {
    source: {
      code: StoryNameSource,
    },
  },
},
```

## Discrepancies Found in Current Implementation

### 1. Naming Inconsistency
- Most stories use `{ComponentName}DefaultStory.vue` pattern
- Empty stories use `{Description}{ComponentName}.vue` pattern (e.g., `EmptyBackgroundStory.vue`)
- Recommendation: Standardize on `{ComponentName}DefaultStory.vue` for primary story

### 2. Filename Capitalization
- Most component names are capitalized consistently
- One file is named `checkbox.stories.ts` instead of `Checkbox.stories.ts`
- Recommendation: Use PascalCase consistently for all story files

### 3. Unused Imports
- In `apps/storybook/stories/ui/badge/Badge.stories.ts`, there's an import from wrong registry: `import { registryItem } from '@/components/ui/spinner/_registry'` instead of `'@/components/ui/badge/_registry'`
- Recommendation: Correct the import to reference the badge's registry

### 4. Inconsistent Args Definition
- Some stories define `args` in the story definition
- Others define default `args` in the meta
- Recommendation: Define default `args` in the meta for consistency

### 5. Missing Stories
- Some components have TODO comments indicating missing stories
- Example: `apps/storybook/stories/ui/empty/Empty.stories.ts` has `// TODO: AvatarStory`, `// TODO: AvatarGroupStory`, `// TODO: InputGroupStory`
- Recommendation: Create the missing stories

## Templates

### Template for Simple Component Story
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
      description: {
        component: registryItem.description,
      },
    },
  },
} satisfies Meta<typeof ComponentName>

export default meta
type Story = StoryObj<typeof meta>

export const Default: Story = {
  parameters: {
    docs: {
      source: {
        code: ComponentNameDefaultSource,
      },
    },
  },

  render: args => ({
    components: { ComponentNameDefaultStory },

    setup() {
      return { args }
    },

    template: html`
      <ComponentNameDefaultStory v-bind="args" />
    `,
  }),
}
```

### Template for Component with Subcomponents
```ts
import type { Meta, StoryObj } from '@storybook/vue3-vite'
import { html } from 'common-tags'

import {
  ComponentRoot,
  ComponentItem,
  ComponentTrigger,
  ComponentContent,
} from '@/components/ui/component-name'
import { registryItem } from '@/components/ui/component-name/_registry'

import ComponentDefault from './ComponentDefault.vue'
import ComponentDefaultSource from './ComponentDefault.vue?raw'

const meta = {
  title: 'Components/ComponentName',
  component: ComponentRoot,
  subcomponents: {
    ComponentItem,
    ComponentTrigger,
    ComponentContent,
  },
  tags: ['autodocs'],

  parameters: {
    docs: {
      description: {
        component: registryItem.description,
      },
    },
  },
} satisfies Meta<typeof ComponentRoot>

export default meta
type Story = StoryObj<typeof meta>

export const Default: Story = {
  parameters: {
    docs: {
      source: {
        code: ComponentDefaultSource,
      },
    },
  },

  render: args => ({
    components: { ComponentDefault },

    setup() {
      return { args }
    },

    template: html`
      <ComponentDefault v-bind="args" />
    `,
  }),
}
```

## Best Practices

1. Use the `html` template tag from `common-tags` for multi-line templates in the `render` function
2. Import the component's registry item to access description and other metadata
3. Always import raw source files (?raw) to show actual code in documentation
4. Use proper TypeScript typing with `Meta` and `StoryObj`
5. Include `tags: ['autodocs']` to enable automatic documentation generation
6. Structure complex stories with appropriate args and argTypes for interactivity
7. Use consistent component paths (@/components/ui/{component-name})
8. Keep story files organized by component type in the stories directory

## Common Pitfalls to Avoid

1. Forgetting to import the registry item for component descriptions
2. Not properly importing raw source for documentation
3. Misnaming files (case sensitivity matters)
4. Incorrect component import paths
5. Forgetting to export the meta and story types
6. Not maintaining consistent naming patterns
7. Not including subcomponents in the meta when applicable
