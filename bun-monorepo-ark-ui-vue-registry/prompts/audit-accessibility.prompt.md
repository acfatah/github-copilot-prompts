---
agent: ask
---

# Audit Accessibility

Audit the given Vue component(s) for accessibility compliance. Provide ACTIONABLE
findings without making direct code changes.

## Scope

Focus on the following areas, in priority order:

### 1. Keyboard Navigation
- All interactive elements reachable via `Tab` / `Shift+Tab`
- Arrow key navigation for composite widgets (menu, listbox, tabs, radio group)
- `Escape` closes overlays (dialogs, dropdowns, popovers)
- `Enter` / `Space` activate buttons and toggles
- No keyboard traps (focus cannot escape a region unintentionally)

### 2. ARIA Roles, States & Properties
- Correct role applied (`role="dialog"`, `role="menu"`, `role="listbox"`, etc.)
- Required ARIA attributes present (`aria-expanded`, `aria-haspopup`,
  `aria-controls`, `aria-labelledby`, `aria-describedby`)
- Dynamic states updated reactively (`aria-disabled`, `aria-checked`,
  `aria-selected`, `aria-busy`)
- No redundant ARIA (e.g., `role="button"` on `<button>`)

### 3. Focus Management
- Focus moves to the correct element when a dialog/popover opens
- Focus returns to the trigger when a dialog/popover closes
- `aria-modal="true"` set on modal dialogs
- No focus loss when content changes dynamically

### 4. Labelling
- All interactive elements have an accessible name
  (via `aria-label`, `aria-labelledby`, visible text, or `<label>`)
- Icon-only buttons have `aria-label` or `<span class="sr-only">`
- Form fields linked to their label with `for`/`id` or `aria-labelledby`
- Error messages linked with `aria-describedby`

### 5. Color & Contrast
- Text meets WCAG AA contrast ratio (4.5:1 normal, 3:1 large text)
- Focus indicators visible against all background colors
- State not conveyed by color alone (use icons, text, or patterns too)

### 6. Motion & Animation
- Animations respect `prefers-reduced-motion` where applicable

## Output Format

Start with a short summary of what the component does.

Then report findings grouped by area:

- **Keyboard Navigation**
- **ARIA**
- **Focus Management**
- **Labelling**
- **Color & Contrast**
- **Motion**

Severity scale:
- 🟥 Critical — blocks assistive technology users completely
- 🟧 High — significantly degrades the experience
- 🟨 Medium — noticeable but has a workaround
- 🟩 Low — minor improvement opportunity
- ✅ LGTM — no issues found in this area

## Notes

- Ark UI handles many ARIA patterns automatically. Verify via `context7` which
  attributes Ark injects before flagging them as missing.
- Check if the component already uses `data-scope` / `data-part` attributes —
  these may carry Ark UI's built-in ARIA semantics.
- Reference: WCAG 2.2 (https://www.w3.org/TR/WCAG22/), APG patterns
  (https://www.w3.org/WAI/ARIA/apg/patterns/).
- Run `bun format` first to normalize the code before reviewing.
