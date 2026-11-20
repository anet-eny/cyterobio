@AGENTS.md

# Project

Single-page landing page built from a Figma prototype.

- Design source: Figma prototype, **desktop only**. Colors and text styles are defined as Figma styles. Spacing was done by eye, so treat it as approximate and round it to the Tailwind scale.
- Figma file: (https://www.figma.com/design/XLGAVtqgKObNCMSEj3M4rp/CyteroBio?node-id=149-201&t=hKMLhikYsBFbm3vx-4)
- Convention reference (read-only): `../fibralis`. Take its structure and conventions, **not** its content, colors or copy. Do not modify it.
- Images: originals are in `_assets/`. Move them to `public/images/`.

## Stack

Next.js (latest via `create-next-app`) · TypeScript · Tailwind v4 · App Router

## How to work with me

- Reply to me in Czech. Code, comments and identifiers in English.
- For anything bigger than a small fix: propose a plan first and wait for approval before writing code.
- Build section by section (tokens and layout first, then hero, features, footer, ...). Commit after each finished section. Do not push unless I ask.
- If it is unclear which image belongs where, or which logo variant is for light/dark backgrounds, ask me.
- Animations and hover effects are not in Figma. Do not add them until I describe them.

## Core rules

- One component per file
- Simple readable code over production patterns
- No unnecessary abstraction
- Before writing Next.js code, check `node_modules/next/dist/docs/` (see AGENTS.md). Do not rely on memory of older versions.

## Folder structure

```
src/app/            layout.tsx, page.tsx, globals.css
src/components/     one section per file (hero.tsx, features.tsx, footer.tsx, ...)
src/components/ui/  small reusable pieces (button.tsx, section-label.tsx, ...)
src/hooks/          custom hooks, only if needed
src/lib/            typography.ts (shared Tailwind class strings for text styles)
public/images/      all images and logos
```

## Naming

- Files: `kebab-case.tsx`
- Components: `PascalCase`
- CSS tokens: `--color-*`, `--font-*`, `--spacing-*`
- Images: lowercase, no spaces or diacritics (`hero-product.png`, `logo-dark.svg`)

## Tailwind v4

- Design tokens live in `@theme {}` inside `globals.css`. There is no `tailwind.config`.
- Custom tokens use `--color-*` naming so Tailwind generates classes automatically (`bg-bg`, `text-cream`).
- All colors are defined in `@theme`. Use token classes, never arbitrary hex values.
- Take colors and fonts from the Figma styles. Convert colors to `oklch()`.
- `@theme` is for design tokens. Component variants go in the component itself.
- In `@layer base` reference tokens with `var(--color-*)`, not the v3 `theme()` function.
- Define custom utilities (e.g. container) with `@utility`, not `@layer utilities`, so variants work.

## Spacing

- Round Figma values to the Tailwind scale (4, 6, 8, 12, 16, 24, 32, 48 ...) and keep a consistent rhythm.
- Section vertical padding is a single token: `--spacing-section: clamp(...)`, used as `py-section`. Never hardcode `py-28` or similar on sections.
- Container: one shared `container` utility with a max-width and fluid horizontal padding via `clamp()`.

## Responsive

- Mobile-first. Figma has desktop only, so design the mobile and tablet layouts sensibly from the desktop one.
- Use fluid type via `clamp()` rather than many breakpoint overrides.
- Verify at roughly 375, 768 and 1280 px.

## Typography

- Text styles from Figma become named class strings in `src/lib/typography.ts` (e.g. `sectionTitle`, `sectionBody`, `eyebrowLabel`). Components import them instead of repeating long class lists.
- Font loaded with `next/font/google` in `layout.tsx`, exposed as `--font-sans`.

## Images

- Use `next/image` with explicit `width` + `height`, or `fill` + `sizes`.
- Always write meaningful `alt` text (empty `alt=""` only for purely decorative images).
- Prefer SVG for logos and icons.

## Animation (when requested)

- Keep animation CSS in `globals.css` and always add a `prefers-reduced-motion: reduce` fallback.

## SVG dashed lines (dividers and workflow connector)

The design has three dashed SVG lines. Colors come from tokens (Figma styles "CB Primary 700" and "CB Primary 100"), never hex in JSX.

| Line      | Where                                      | Stroke                            | Notes                                                                              |
| --------- | ------------------------------------------ | --------------------------------- | ---------------------------------------------------------------------------------- |
| Divider   | between "Our services" and "Our portfolio" | primary-700 (#3B486D), 7px dashed | full-bleed wave, about 1612x132 px in Figma (wider than the 1440 frame on purpose) |
| Divider 2 | between CTA and Footer                     | primary-700 (#3B486D), 7px dashed | same wave, mirrored horizontally (`scale-x-[-1]`)                                  |
| Connector | between Workflow Cards in "How we work"    | primary-100 (#D2CAEA), 7px dashed | about 611x1153 px in Figma; desktop only                                           |

**Figma caveat:** Figma's CSS shows these as boxes with a dashed `border`. That is only the bounding box of the vector. Take the real path from the exported SVG (`_assets/svg/`, or via Figma MCP), not from the CSS border. If the SVG files are missing, ask me for them. Stroke width and dash pattern come from Figma, check them visually.

**Technique (all three lines):**

- One SVG per line, with the path normalized to `viewBox="0 0 100 100"` and `preserveAspectRatio="none"`. The path never changes, the SVG element itself is stretched or squashed to the size we need.
- `fill: none` and `overflow: visible` on the SVG so the stroke edges are not clipped.
- `vector-effect: non-scaling-stroke` on the path. This is required: it keeps stroke width and dash pattern in real screen pixels, so stretching the SVG never distorts the dashes.
- Set `stroke-width` and `stroke-dasharray` in px. Use `stroke-linecap: round` only if the Figma dashes are round.
- Shape the path so it degrades gracefully when the SVG gets narrow: for each curve, the first control point is horizontally aligned with the start point and the second with the end point. Then a narrow SVG becomes a straight line instead of a squashed curve.
- Define the shared SVG properties once (for example an `@utility` in `globals.css`), do not repeat them per component.
- All three are decorative: `aria-hidden="true"`, `focusable="false"`, `pointer-events-none`.

**Dividers:** no JavaScript. Full viewport width (`w-full`), fixed height (about 132 px on desktop, check if it should be lower on mobile). Wrap in `overflow-x-clip` so the bleed never causes a horizontal scrollbar. Each divider is a small component in `src/components/ui/`.

**Workflow connector:** needs JavaScript because it must line up with the cards.

- Client Component (`"use client"`). The section container is `relative`, the SVG is `absolute` inside it.
- Measure the cards with refs and `getBoundingClientRect()` (relative to the container) and set the SVG's left, top, width and height so the line runs between the card centers shown in Figma.
- Width and height must be at least 1px, because zero-sized elements are not painted.
- Recalculate with a `ResizeObserver` on the container, plus the window `resize` event.
- Check in Figma whether it is one long path through all cards or separate segments between each pair, and build it accordingly. If unclear, ask me.
- Hidden when the cards stack (small tablet and mobile): `hidden lg:block`. Choose the breakpoint (`md` or `lg`) according to where the card layout stops matching the Figma arrangement, and tell me which one you picked.
- On mobile and small tablet the cards are simply stacked one under another, with no line.

Test all three at about 375, 768, 1024, 1280 and 1920 px.

## Security headers

Copy the `headers()` block from the reference project's `next.config.ts` (nosniff, X-Frame-Options, Referrer-Policy, Permissions-Policy).

## Do not

- Use `@apply`. Write Tailwind classes directly in JSX.
- Use `:root` for design tokens. Always `@theme`.
- Use arbitrary hex colors or hardcoded section padding.
- Edit or delete `AGENTS.md`.
- Skip `rm -rf .next` when tokens are not resolving.
