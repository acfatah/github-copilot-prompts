---
agent: agent
---

# Creating Storybook Stories for Vue Components

## Overview

This document outlines the patterns, conventions, and implementation details for creating new components in the `@packages/registry/src/components/ui/` directory. Use this as a guide when creating new UI components.

## Directory Structure

Each component has its own directory with the following files:
```
components/ui/{component-name}/
├── {ComponentName}Root.vue (for complex components)
├── {ComponentName}Item.vue (if applicable)
├── {ComponentName}Content.vue (if applicable)
├── {ComponentName}Trigger.vue (if applicable)
├── {ComponentName}.vue (for simple components)
├── index.ts
├── namespace.ts (for complex components)
└── _registry.ts
```

## Component Patterns & Conventions

### 1. Vue Component Structure

All Vue components follow this basic structure:

```vue
<script setup lang="ts">
import type { HTMLAttributes } from 'vue'
import { {ArkComponent} } from '@ark-ui/vue/{ark-component}'
import { reactiveOmit } from '@vueuse/core'
import { cn } from '@/lib/utils'
// Import useForwardProps or useForwardPropsEmits as needed

interface Props {
  class?: HTMLAttributes['class']
  // Add other props as needed
}

const props = withDefaults(defineProps<Props>(), {
  // Set default values if needed
})

const delegatedProps = reactiveOmit(props, 'class')
// Use useForwardProps for components without emits
// Use useForwardPropsEmits for components with emits
</script>

<template>
  <{ArkComponent}.{Part}
    v-bind="forwardedProps"
    :class="cn('{default-classes}', props.class)"
  >
    <slot />
  </{ArkComponent}.{Part}>
</template>
```

If the component is not derived from Ark UI, add `data-scope` and `data-part`
(for sub-elements) attributes to the elements. The `data-scope` should be the
component name in kebab-case, and `data-part` should describe the part of the
component.

### 2. Component Types

There are two main types of components:

#### Simple Components (e.g., Button, Badge, Spinner, Separator)
- Single `.vue` file implementation
- May have variant definitions in `index.ts`
- Direct use of Ark UI components or native HTML elements with styling
- Example: Button, Badge, Spinner, Separator

#### Complex Components (e.g., Accordion, Checkbox, RadioGroup)
- Multiple `.vue` files for different parts
- Uses Root component as the main container
- Additional sub-components like Item, Content, Trigger, Label, etc.
- Includes a namespace.ts file
- Example: Accordion, Checkbox, RadioGroup, Field, Fieldset

### 3. Variant Handling

For components with variants (like Button, Badge), create variant definitions in `index.ts`:

```ts
import type { VariantProps } from 'class-variance-authority'
import { cva } from 'class-variance-authority'

// Define variants
export const variant = {
  // variant definitions
}

export const size = {
  // size definitions
}

// Create cva with default styling and variants
export const {componentName}Variants = cva(
  '{base-classes}',
  {
    variants: {
      variant,
      size,
    },
    defaultVariants: {
      variant: 'default',
      size: 'md',
    },
  },
)

export type {ComponentName}Variants = VariantProps<typeof {componentName}Variants>
```

### 4. Index.ts Export Pattern

For simple components:
```ts
// Export variants if applicable
// Export component
export { default as {ComponentName} } from './{ComponentName}.vue'
```

For complex components:
```ts
// Export all sub-components
export { default as {ComponentName}Root } from './{ComponentName}Root.vue'
export { default as {ComponentName}Item } from './{ComponentName}Item.vue'
// ... other sub-components

// Export namespace
export { {ComponentName} } from './namespace'
```

### 5. Namespace.ts Pattern

For complex components with multiple parts:
```ts
import {ComponentName}Root from './{ComponentName}Root.vue'
import {ComponentName}Item from './{ComponentName}Item.vue'
// ... other imports

export const {ComponentName} = {
  /**
   * {ComponentName}Root component
   */
  Root: {ComponentName}Root,

  /**
   * {ComponentName}Item component
   */
  Item: {ComponentName}Item,

  // ... other components with documentation
}
```

### 6. _registry.ts Pattern

Each component needs a registry file:
```ts
import type { RegistryItem } from 'shadcn/schema'
import { html } from 'common-tags'

export const registryItem = {
  type: 'registry:ui',
  name: '{component-name}',
  title: '{Component Name}',

  description: html`
    {A description of the component}

    References:
    - Headless API: https://ark-ui.com/docs/components/{component-name} (if applicable)
    - shadcn/ui: https://ui.shadcn.com/docs/components/{component-name}
  `,

  dependencies: [
    // List dependencies as needed
    '@ark-ui/vue', // For Ark UI components
    '@iconify/vue', // If using icons
    '@vueuse/core', // For reactive utilities
    'class-variance-authority', // If using variants
  ],

  files: [
    // List related files that need to be included
    {
      path: 'src/composables/dynamic.ts',
      type: 'registry:file',
      target: 'src/composables/dynamic.ts',
    },
    // Add other files as needed
  ],
} satisfies RegistryItem

export default registryItem
```

### 7. Import Conventions

- Ark UI components: `@ark-ui/vue/{component-name}`
- Vue utilities: `@vueuse/core`
- Class name utils: `@/lib/utils`
- Composables: `@/composables/*`
- Icons: `@iconify/vue`

### 8. Styling Conventions

- Use Tailwind CSS for styling
- Use `cn()` utility for class name composition
- Follow consistent BEM-like naming for data attributes
- Include `data-scope` attribute for styling context
- Use responsive prefixes where needed (@md, etc.)
- Consistent focus and state styles across components

### 9. Type Safety

- Use TypeScript throughout
- Define proper types for props and emits
- Use `VariantProps` from class-variance-authority for variant types
- Use Ark UI provided types where available

## Creating New Components: Step-by-Step

1. Create the component directory: `components/ui/{component-name}/`
2. Determine if it's a simple or complex component
3. Create the necessary .vue files following the patterns
4. Create index.ts with proper exports
5. Create namespace.ts if it's a complex component
6. Create _registry.ts with proper metadata
7. Run formatter as the final task, `bun format {component-directory}`

## Best Practices

- Follow Ark UI accessibility guidelines
- Use context7 to get documentation and examples on Ark UI and shadcn components
- Use consistent naming patterns
- Keep components composable and flexible
- Maintain proper TypeScript typing
- Use the `cn()` utility consistently for class names
- Follow the forward props pattern for proper attribute delegation
- Add JSDoc comments for complex components in namespace files
- Include proper data attributes for styling context
