---
agent: agent
---

Accordion `_registry.ts` component as example:
```typescript
import type { RegistryItem } from 'shadcn/schema'
import { html } from 'common-tags'

export const registryItem = {
  type: 'registry:ui',
  name: 'accordion',
  title: 'Accordion',

  description: html`
    A vertically stacked set of interactive headings that each reveal a section of content.

    References:
    - Headless API: https://ark-ui.com/docs/components/accordion
    - shadcn/ui: https://ui.shadcn.com/docs/components/accordion
  `,

  dependencies: [
    '@ark-ui/vue',
    '@iconify/vue',
    '@vueuse/core',
  ],

  files: [
    {
      path: 'src/composables/dynamic.ts',
      type: 'registry:file',
      target: 'src/composables/dynamic.ts',
    },
    {
      path: 'src/composables/use-forward-props.ts',
      type: 'registry:file',
      target: 'src/composables/use-forward-props.ts',
    },
  ],

  tailwind: {
    config: {
      theme: {
        extend: {
          animation: {
            '--animate-accordion-down': 'accordion-down 0.25s ease-out',
            '--animate-accordion-up': 'accordion-up 0.25s ease-out',
          },
          keyframes: {
            'accordion-down': {
              from: { height: '0' },
              to: { height: 'var(--height)' },
            },
            'accordion-up': {
              from: { height: 'var(--height)' },
              to: { height: '0' },
            },
          },
        },
      },
    },
  },
} satisfies RegistryItem

export default registryItem
```

Use the above as a reference to create similar `_registry.ts` files for the given
directory (or directories) by analyzing the components within it. Skip all tests.
Use spaces instead of tabs.

