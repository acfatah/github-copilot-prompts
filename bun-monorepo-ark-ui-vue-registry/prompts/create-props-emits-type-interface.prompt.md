---
agent: agent
---

Example:
```vue
<script setup lang="ts">
import type { HTMLAttributes } from 'vue'
import { useVModel } from '@vueuse/core'
import { cn } from '@/lib/utils'

interface Props {
  defaultValue?: File[]
  modelValue?: File[]
  multiple?: boolean
  accept?: string
  name?: string
  disabled?: boolean
  class?: HTMLAttributes['class']
}

interface Emits {
  (e: 'update:modelValue', payload: File[]): void
  (e: 'change', payload: File[]): void
}

const props = defineProps<Props>()
const emits = defineEmits<Emits>()
</script>
```

Use the above example as a reference to create Props and Emits interfaces for the
components or components under a directory (or directories) mentioned. Skip all tests.
