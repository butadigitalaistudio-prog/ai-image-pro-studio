# Design System Document

## 1. Overview & Creative North Star: "The Neon Observatory"
This design system is engineered for a high-performance AI image generation workspace. The Creative North Star is **"The Neon Observatory"**—a concept that balances the vast, dark void of creative potential with the surgical precision of advanced technology. 

To move beyond the "standard SaaS" look, this system rejects rigid grids and boxy containment. We utilize **intentional asymmetry**, where control panels feel like floating HUDs (Heads-Up Displays) and the canvas feels infinite. We achieve a premium feel through **tonal depth** rather than structural lines, ensuring the UI recedes so the AI-generated art remains the protagonist.

---

## 2. Colors & Surface Philosophy
The palette is a sophisticated range of deep obsidians and muted charcoals, punctuated by high-energy violets and electric cyans.

### The "No-Line" Rule
Standard 1px borders are strictly prohibited for sectioning. Structural boundaries must be defined solely through background color shifts. To separate a sidebar from the main canvas, transition from `surface` (#0e0e0e) to `surface-container-low` (#131313). This creates a seamless, "molded" look rather than a "pasted" one.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers. 
- **Base Layer:** `surface` (#0e0e0e) – The infinite workspace.
- **Secondary Panels:** `surface-container` (#1a1a1a) – Main navigation or tool groupings.
- **Nested Controls:** `surface-container-high` (#20201f) – Individual tool settings or input groups.
- **Active Overlays:** `surface-bright` (#2c2c2c) – Temporary states or active popovers.

### The "Glass & Gradient" Rule
To inject "soul" into the dark theme, use Glassmorphism for floating toolbars. 
- **Implementation:** Use `surface-container-highest` at 60% opacity with a `24px` backdrop blur. 
- **Signature Gradients:** For primary CTAs (Generate buttons), apply a linear gradient from `primary` (#b6a0ff) to `primary-dim` (#7e51ff) at a 135-degree angle. This provides a tactile, luminous quality that flat colors lack.

---

## 3. Typography: The Editorial Engine
We pair the technical precision of **Inter** with the structural elegance of **Manrope** to create an editorial hierarchy that feels both authoritative and modern.

- **Display & Headlines (Manrope):** Used for high-level branding and workspace titles. The wide apertures of Manrope at `display-lg` (3.5rem) create a cinematic feel.
- **Body & Labels (Inter):** Used for all functional data. Inter's tall x-height ensures maximum readability at `body-sm` (0.75rem) when adjusting complex AI parameters.
- **Functional Contrast:** Always use `on-surface-variant` (#adaaaa) for secondary labels to ensure the `on-surface` (#ffffff) values draw the eye to critical data and primary inputs.

---

## 4. Elevation & Depth: Tonal Layering
In this system, light is the architect of space.

- **The Layering Principle:** Depth is achieved by "stacking" tones. Place a `surface-container-lowest` card on a `surface-container-low` section to create a soft, natural inset. This mimics a physical mold rather than a digital box.
- **Ambient Shadows:** Shadows should be used sparingly. When an element must float (e.g., a modal), use a `48px` blur at 8% opacity. The shadow color must be a tinted version of the primary color (e.g., a dark violet tint) to mimic light refracting through the UI.
- **The "Ghost Border" Fallback:** If accessibility requires a stroke, use the `outline-variant` token at 15% opacity. High-contrast, 100% opaque borders are prohibited.

---

## 5. Components

### Buttons: The Tactile Triggers
- **Primary:** Gradient fill (`primary` to `primary-dim`), `full` roundedness, and `title-sm` typography. On hover, increase the gradient luminosity.
- **Secondary:** Surface-only with a "Ghost Border." No fill.
- **Tertiary:** Text only using `primary` color, strictly for low-priority actions like "Cancel" or "Reset."

### Inputs & Sliders: The Precision Dial
- **Text Inputs:** Use `surface-container-highest` background. Instead of a border, use a 2px bottom-accent of `primary` that only appears on `:focus`.
- **Sliders:** The track should be `surface-variant`. The "thumb" should be a `primary` glow. As the user slides, the track behind the thumb should fill with a `primary-container` color.

### AI Prompt Cards
- **Forbid Dividers:** Use `spacing-6` (1.3rem) of vertical whitespace to separate cards. 
- **Status Chips:** Use `secondary` (#c492fe) for "In Progress" and `tertiary` (#ff97b8) for "Upscaling." Chips must have `0.25rem` (DEFAULT) roundedness to maintain a technical, "tabbed" aesthetic.

### Additional Component: The "Prompt Breadcrumb"
A specialized horizontal list using `label-sm` to show the AI's processing steps (e.g., *Denoising > Refinement > Color Grade*). Use `on-surface-variant` with the active step highlighted in `primary` and a subtle `surface-tint` glow.

---

## 6. Do's and Don'ts

### Do:
- **Use Asymmetric Spacing:** Give more room to the right of a container than the left to create a sense of forward momentum.
- **Embrace the Dark:** Trust the `surface-dim` and `surface-container-lowest` tokens. True blacks provide the best contrast for high-end AI imagery.
- **Color Coding:** Use `error` (#ff6e84) exclusively for destructive actions or failed generations; never use it for aesthetic accents.

### Don't:
- **Don't use 1px Solid Lines:** They break the "Neon Observatory" immersion. Use background shifts instead.
- **Don't use Standard Shadows:** Avoid the "fuzzy grey" shadow. If it doesn't look like ambient light, don't use it.
- **Don't Over-Round:** Stick to `md` (0.375rem) for cards and `full` for buttons. Avoid "pill" shapes for large containers as it looks "bubbly" rather than "high-end."