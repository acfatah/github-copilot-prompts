---
agent: agent
---

# Create Namespace File

Create `namespace.ts` for the given component directory (or directories) using
the RadioGroup pattern below. Also update `index.ts` to export the namespace object.

## Pattern (RadioGroup example)

```ts
import RadioGroupDescription from './RadioGroupDescription.vue'
import RadioGroupIndicator from './RadioGroupIndicator.vue'
import RadioGroupItem from './RadioGroupItem.vue'
import RadioGroupItemContent from './RadioGroupItemContent.vue'
import RadioGroupItemControl from './RadioGroupItemControl.vue'
import RadioGroupItemDescription from './RadioGroupItemDescription.vue'
import RadioGroupItemHiddenInput from './RadioGroupItemHiddenInput.vue'
import RadioGroupItems from './RadioGroupItems.vue'
import RadioGroupItemText from './RadioGroupItemText.vue'
import RadioGroupLabel from './RadioGroupLabel.vue'
import RadioGroupRoot from './RadioGroupRoot.vue'
import RadioGroupRootProvider from './RadioGroupRootProvider.vue'

export const RadioGroup = {
  /**
   * RadioGroupRoot component
   */
  Root: RadioGroupRoot,

  /**
   * RadioGroupLabel component
   *
   * Label for the radio group (use ItemText for individual item labels)
   */
  Label: RadioGroupLabel,

  /**
   * RadioGroupDescription component
   *
   * Description for the radio group
   */
  Description: RadioGroupDescription,

  /**
   * RadioGroupItems component
   *
   * A flex column used to wrap radio button items. Handles orientation and spacing.
   */
  Items: RadioGroupItems,

  /**
   * RadioGroupItem component
   *
   * Represents a single radio button item in the group
   */
  Item: RadioGroupItem,

  /**
   * RadioGroupItemControl component
   *
   * The visual control element for the radio button
   */
  ItemControl: RadioGroupItemControl,

  /**
   * RadioGroupIndicator component
   *
   * The indicator shown when the radio is checked
   */
  Indicator: RadioGroupIndicator,

  /**
   * RadioGroupItemContent component
   *
   * A flex column used to group ItemText and ItemDescription.
   * Not required if you have no description.
   */
  ItemContent: RadioGroupItemContent,

  /**
   * RadioGroupItemText component
   *
   * Text label for individual radio items
   */
  ItemText: RadioGroupItemText,

  /**
   * RadioGroupItemDescription component
   *
   * Description for individual radio items
   */
  ItemDescription: RadioGroupItemDescription,

  /**
   * RadioGroupItemHiddenInput component
   *
   * Hidden input for form submission
   */
  ItemHiddenInput: RadioGroupItemHiddenInput,

  /**
   * RadioGroupRootProvider component
   *
   * See: https://ark-ui.com/docs/components/radio-group#using-the-root-provider
   */
  RootProvider: RadioGroupRootProvider,
}
```

## Note

For components without repeated inner items, use `Content` instead of `ItemContent`
to group `Label` and `Description`.
