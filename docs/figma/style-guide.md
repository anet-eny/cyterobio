# CyteroBio – Figma Style Guide

Source: Figma file `XLGAVtqgKObNCMSEj3M4rp`, node `184:211` (Style Guide). Read on 2026-11-21 via Figma MCP (`get_variable_defs`), then corrected by the designer (3 styles renamed Primary → Secondary). Do not re-read Figma for these values.

## Colors

| Figma style      | Hex     | oklch                    | Token                   |
| ---------------- | ------- | ------------------------ | ----------------------- |
| CB Primary 100   | #ACBEF1 | oklch(0.806 0.075 269.5) | `--color-primary-100`   |
| CB Primary 300   | #5F75B2 | oklch(0.571 0.098 268.1) | `--color-primary-300`   |
| CB Primary 500   | #4D5D8B | oklch(0.485 0.077 268.8) | `--color-primary-500`   |
| CB Primary 700   | #3B486D | oklch(0.407 0.065 268.7) | `--color-primary-700`   |
| CB Secondary 100 | #D2CAEA | oklch(0.855 0.045 296.9) | `--color-secondary-100` |
| CB Secondary 500 | #5C4D8B | oklch(0.464 0.099 293.3) | `--color-secondary-500` |
| CB Secondary 700 | #3D335D | oklch(0.352 0.072 293.3) | `--color-secondary-700` |
| CB Accent 300    | #4D7C8B | oklch(0.558 0.056 220.2) | `--color-accent-300`    |
| CB Accent 500    | #1A8F84 | oklch(0.587 0.098 185.0) | `--color-accent-500`    |
| CB Accent 700    | #10665E | oklch(0.461 0.077 185.1) | `--color-accent-700`    |
| CB Neutral 100   | #ECEFF5 | oklch(0.952 0.009 264.5) | `--color-neutral-100`   |
| CB Neutral 200   | #D5D9E3 | oklch(0.885 0.014 268.5) | `--color-neutral-200`   |
| CB Neutral 300   | #A3AABB | oklch(0.738 0.026 267.9) | `--color-neutral-300`   |
| CB Neutral 500   | #6B7388 | oklch(0.556 0.034 268.8) | `--color-neutral-500`   |
| CB Neutral 800   | #1F2638 | oklch(0.271 0.035 267.7) | `--color-neutral-800`   |
| CB Neutral 900   | #0F1420 | oklch(0.192 0.026 266.6) | `--color-neutral-900`   |
| Gradient 1       | –       | –                        | values missing (MCP returned empty); fill in when the section using it is built |
| Gradient 2       | –       | –                        | same as Gradient 1      |

Secondary has only 100, 500 and 700 (no 300).

## Text styles

| Figma style   | Font           | Size  | Weight | Line height | Letter-spacing |
| ------------- | -------------- | ----- | ------ | ----------- | -------------- |
| Heading 1 Alt | IBM Plex Serif | 72 px | 600    | 100 %       | 0              |
| Heading 1     | Outfit         | 48 px | 600    | 100 %       | 0              |
| Heading 2     | Outfit         | 36 px | 400    | 100 %       | 0              |
| Heading 2 Alt | IBM Plex Serif | 32 px | 600    | 100 %       | 0              |
| Heading 3     | Outfit         | 24 px | 400    | 1.3         | 0              |
| Heading 3 Alt | IBM Plex Serif | 24 px | 600    | 100 %       | 0              |
| Paragraph     | Outfit         | 16 px | 400    | 1.4         | 0              |

- Fonts: Outfit → `--font-sans`, IBM Plex Serif → `--font-serif` ("Alt" styles use serif).
- Weights to load: Outfit 400 and 600; IBM Plex Serif 600.
- Fluid sizes: the Figma (desktop) size is the `clamp()` maximum; the mobile minimum is about 60 % (e.g. Heading 1 Alt 40 → 72 px, Heading 1 ~29 → 48 px, Heading 2 ~22 → 36 px, Heading 2 Alt ~20 → 32 px, Heading 3 / 3 Alt ~16–18 → 24 px). Paragraph stays fixed at 16 px.

## Spacing

No spacing styles in the Style Guide. Take spacing from the section designs and round to the Tailwind scale (4, 6, 8, 12, 16, 24, 32, 48 …).

## Usage decisions

| Element                         | Token                                     |
| ------------------------------- | ----------------------------------------- |
| Divider, Divider 2 stroke       | `primary-700` (#3B486D)                   |
| Workflow connector stroke       | `secondary-100` (#D2CAEA)                 |
| Navbar logo (`logo.svg`)        | `primary-100` (#ACBEF1), via `currentColor` |
| Footer logo (`logo-footer.svg`) | `primary-500` (#4D5D8B), via `currentColor` |

## Discrepancies found

1. The first MCP read returned only one style per Primary/Secondary pair, because 3 styles were mis-named "Primary" instead of "Secondary". The designer renamed them; the table above is the corrected state. (Resolved)
2. CLAUDE.md listed the connector as "primary-100 (#D2CAEA)". #D2CAEA is now Secondary 100, so the connector uses `secondary-100` (matches the exported `connecting vector.svg`). CLAUDE.md fixed. (Resolved)
3. Both logo SVGs hard-code `fill: rgb(77,93,139)` = #4D5D8B = Primary 500. They will be converted to `currentColor` so the color comes from tokens. (Decided, not yet implemented)
4. The exported line SVGs (`_assets/svg/`) have the dashes baked in as separate subpaths. Measured values: 7 px stroke, ~13 px dash / ~13 px gap, round caps. The paths will be rebuilt as one continuous path + `stroke-dasharray`. (Decided, not yet implemented)
5. Gradient 1 / Gradient 2 values were not returned by MCP. (Open)
