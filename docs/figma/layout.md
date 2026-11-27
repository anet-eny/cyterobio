# CyteroBio – Desktop layout (Figma)

Source: Figma file `XLGAVtqgKObNCMSEj3M4rp`, frame `149:201` "Desktop" (1440 × 6304). Read on 2026-11-22 via Figma MCP: `get_metadata` (structure, positions, sizes) + one `get_screenshot` of the whole frame (549 × 2400 px, overview only). Open questions answered by the designer on 2026-11-27. Do not re-read Figma for this.

**Source of every value:**
- **[M]** = from `get_metadata` (exact Figma coordinates, px)
- **[S]** = estimated from the low-res screenshot (colors, content, look; not exact)
- **[D]** = decided / supplied by the designer (authoritative)

All coordinates of a section's children are relative to that section frame unless noted otherwise.

## Section order

| # | Figma frame (id) | Visible heading [S] | y | height | Notes |
| - | ---------------- | ------------------- | - | ------ | ----- |
| 1 | Nav (149:279) | – | 0 [M] | 158 [M] | |
| 2 | Hero (149:223) | "Let us design your next molecule." | 158 [M] | 866 [M] | |
| 3 | Our services (149:216) | OUR SERVICES | 1022 [M] | 552 [M] | overlaps Hero by 2 px [M] (sloppy Figma) |
| – | Divider (149:222) | – | 1476.9 [M] | 132.2 [M] | page-level vector, x −94.5, w 1612 [M]; straddles Services / Portfolio |
| 4 | Our portfolio (149:213) | OUR PORTFOLIO | 1557 [M] | 963 [M] | overlaps Services by 17 px [M] |
| 5 | About us (149:210) | WHO ARE WE? | 2520 [M] | 994 [M] | frame name "About us", heading text "Who are we?" [S] |
| 6 | How we work (149:202) | HOW WE WORK TOGETHER | 3514 [M] | 1677 [M] | contains the connector |
| 7 | CTA (160:200) | "Want to work with us?" | 5191 [M] | 732 [M] | |
| – | Divider2 (165:245) | – | 5857 [M] | 132.2 [M] | page-level vector, x 1478 (= mirrored, negative scale), w 1612 [M]; straddles CTA / Footer |
| 8 | Footer (165:243) | – | 5923 [M] | 381 [M] | |

Suggested component names: `navbar.tsx`, `hero.tsx`, `services.tsx`, `portfolio.tsx`, `about.tsx`, `how-we-work.tsx`, `cta.tsx`, `footer.tsx`, plus `ui/wave-divider.tsx`.

Section headings sit at y 42 [M] inside the section (Services: y 54 [M]), heading box height 45 [M] → consistent with Heading 2 (36 px), uppercase [S], centered [S].

## Backgrounds [D]

| Section | Background | Tailwind class |
| ------- | ---------- | -------------- |
| Nav | primary-700 | `bg-primary-700` |
| Hero | Gradient 1 | `bg-gradient-1` |
| Our services | neutral-900 | `bg-neutral-900` |
| Our portfolio | Gradient 2 | `bg-gradient-2` |
| About us | Gradient 1 | `bg-gradient-1` |
| How we work | Gradient 2 | `bg-gradient-2` |
| CTA | Gradient 1 | `bg-gradient-1` |
| Footer | neutral-900 | `bg-neutral-900` |

Gradient definitions: see `style-guide.md` (Gradient 1 = primary-700 top → neutral-900 bottom, Gradient 2 = neutral-900 top → primary-700 bottom).
In Figma the Hero background is the `base` rounded-rectangle 1440 × 866 [M]; other sections have no fill layer in the metadata [M].

## Glows (Ellipse 1) [D]

- Hero: x 720, y 198, 346 × 344 [M]. About us: x 526, y 316, 442 × 412 [M]. Both behind the molecule images [S].
- Fill `primary-500`, Figma **layer blur 190** [D].
- CSS: Figma's blur value is roughly 2× the CSS `blur()` radius → start with `blur(95px)` and **verify visually against the screenshot**, adjust if needed.
- Decorative: `aria-hidden="true"`, `pointer-events-none`. Use a smaller blur (and/or smaller ellipse) on mobile for performance.

## Content width (container)

| Element | x | width | Source |
| ------- | - | ----- | ------ |
| Service cards row | 100 | 1240 | [M] |
| Portfolio "Card with Tabs" | 102 | 1235 | [M] |
| Footer content row | 83 | 1213 | [M] |
| Nav logo | 54 | 265 | [M] |
| Workflow cards (outer edges) | 198 – 1233 | 1035 | [M] |

→ **Content width ≈ 1240 px** (100 px side margin on the 1440 frame). `container` = max-width 1240 px content + fluid side padding.
→ **Nav and footer are NOT put into the container** [D]: keep the Figma alignment (nav logo x 54, footer row x 83 on 1440).

## Sections in detail

### 1. Nav (149:279)
- Background `primary-700` [D].
- `Logo` instance (mark + wordmark): x 54, y 40, 265 × 78 [M]. Color `primary-100` [D]. Alignment x 54 kept [D].
- No menu links, no button [M].

### 2. Hero (149:223)
- Background Gradient 1 [D] (`base` rounded-rectangle 1440 × 866 [M]).
- `hero text` frame: x 190, y 43, 753 × 309 [M]. Has a **dashed rounded border** around the text [S] (box only, no SVG).
  - Headline "Let us design your next molecule." x 32, y 32 (in Group 1), 689 × 188 [M]; serif [S] → **Heading 1 Alt** (72 px), 2 lines.
  - Subline "We shape proteins around what your research needs." 562 × 30 [M]; sans, muted color [S].
- Glow: see Glows.
- `nanodsf_curve_axes 2` (chart) is hidden in Figma [M] → **not used** [D].
- **Image `hero_img_VEGF_v04`** is a page-level layer (not inside Hero): x 296, y −82, 1193 × 1193 [M] (page coordinates). It reaches behind the Nav and to the right edge of the frame. File: `hero_img_VEGF_v04.png`.

### 3. Our services (149:216)
- Background `neutral-900` [D].
- Heading x 597, y 54, 246 × 45 [M].
- `Cards` frame x 100, y 143, 1240 × 272 [M]: 3× `Service Card` 392 × 270 at x 0 / 424 / 848 [M] → **gap 32 px**.
- Card titles [S] (serif, ~Heading 3 Alt): "Protein & Enzyme Engineering", "In Silico Feasibility Analysis", "Confidential Contract Research". Body: Paragraph-size text.
- Card look [S]: translucent/glassy, light border, a colored (pink/violet) glow inside. Exact fills unknown.

### 4. Our portfolio (149:213)
- Background Gradient 2 [D].
- Heading x 578, y 42, 284 × 45 [M].
- `Card with Tabs` instance x 102, y 154, 1235 × 723 [M]. Insides not in metadata (instance).
- Layout [S]: 3 **tab pills** centered above the card ("VEGF-Pro" active/filled, "TGF-β3-Pro", "PDGF-BB-Pro"); card (glassy, gradient border, pink/violet glows) with text on the left and the vial on the right.
- **Tabs switch on click → client component** [D]. Each tab has its own vial [D].
- **Vial: 470 × 470 px in Figma** [D]. In code responsive: `aspect-square`, max 470 px, `sizes` based on width [D].

**Tab content [D]:**

| Tab | Title | Description | Chain length | Typical dissolution buffer | Vial |
| --- | ----- | ----------- | ------------ | -------------------------- | ---- |
| VEGF-Pro | Recombinant VEGF-Pro | Engineered VEGF with improved thermostability and enhanced expression in E. coli. Designed for cell culture, angiogenesis assays and tissue engineering applications that call for consistent, long-lasting bioactivity. | 165 amino acids per monomer (~19 kDa, homodimer ~38 kDa) | PBS, pH 7.4 | `vial_VEGF.png` |
| TGF-β3-Pro | Recombinant TGF-β3-Pro | Stabilised TGF-β3 variant optimised for high-yield expression in E. coli. Suited to studies of scarless wound healing, chondrogenic differentiation and stem cell research, where reliable and reproducible activity matters. | 112 amino acids per monomer (~12.5 kDa, homodimer ~25 kDa) | 4 mM HCl | `vial_TGF.png` |
| PDGF-BB-Pro | Recombinant PDGF-BB-Pro | Computationally improved PDGF with enhanced stability and expression yield. Ideal for wound-healing research, cell proliferation assays and regenerative matrices. | 109 amino acids per monomer (~12 kDa, homodimer ~24 kDa) | 10 mM acetic acid | `vial_PDGF.png` |

("E. coli" should be set in italics if the design does so; check at build time.)

### 5. About us (149:210)
- Background Gradient 1 [D].
- Heading "WHO ARE WE?" x 597, y 42, 247 × 45 [M].
- Paragraph x 597, y 162, 397 × 230 [M] (left-aligned with the heading, sits over the molecule's top-right area [S]).
- Glow: see Glows.
- **Image `aboutus_img_TGFb3`** x 135, y 55, 1044 × 1044 [M] → overflows the section bottom (994) by 105 px into How we work. File: `TGFb3.png`.

### 6. How we work (149:202)
- Background Gradient 2 [D].
- Heading x 488, y 42, 464 × 45 [M].
- **5 Workflow Cards**, each 380 × 289 [M]. In reading order (top → bottom), titles [S]:

| # | Title [S] | x [M] | y [M] | center x | center y | side |
| - | --------- | ----- | ----- | -------- | -------- | ---- |
| 1 | Get in touch | 198 | 194 | 388 | 338.5 | left |
| 2 | Confidentiality first | 766 | 311 | 956 | 455.5 | right |
| 3 | Feasibility analysis | 284 | 705 | 474 | 849.5 | left |
| 4 | Design & optimisation | 853 | 888 | 1043 | 1032.5 | right |
| 5 | Expression & validation | 335 | 1221 | 525 | 1365.5 | left |

  Cards: serif title (~Heading 3 Alt), short paragraph, list with "→" bullets [S]; glassy light-blue/violet fill [S].
- **Connector** `connecting vector` (149:203): x 465.28, y 151.17, 610.92 × 1152.70 [M].
  - **One continuous path** through all cards (single vector [M]; continuous on the screenshot [S]), drawn **behind** the cards (cards cover parts of it) [S].
  - Endpoints (from the exported SVG, mapped to section coordinates): start ≈ (586, 329) = right edge of card 1; end ≈ (501, 1220) = top edge of card 5. Between them it rises above card 1 (top ≈ y 151), runs down behind card 2, over to card 3, makes a **small self-crossing loop** between cards 3 and 4 (≈ x 800–850, y 680–860), then goes behind card 4 and curves into the top of card 5 [S + exported SVG].
  - Zig-zag layout needs two columns ≥ ~1035 px wide → proposal: connector and zig-zag from **`lg` (1024 px)**, stacked cards without the line below that.

### 7. CTA (160:200)
- Background Gradient 1 [D].
- **Image `cta_img_PDGF`** x 0, y 48, 1042 × 586 [M] (left, bleeds to the left edge). File: `PDGF.png` (16:9 matches 1042 × 586).
- `Frame 3` x 912, y 324, 344 × 143 [M]:
  - "Want to work with us?" 344 × 42 [M]; serif [S] → Heading 2 Alt (32 px).
  - `Button` instance x 103.6, y 77, 136.8 × 66 [M] (incl. possible shadow/padding); label "Contact", outlined pill [S].
  - **Button does nothing for now, only a hover effect** [D]. No hover in Figma → propose a subtle hover and show it to the designer while building the section.

### 8. Footer (165:243)
- Background `neutral-900` [D].
- `Frame 2` x 83, y 210, 1213 × 68 [M]; alignment x 83 kept, not in the container [D]:
  - `Logo_footer` (mark only) 68 × 68 [M], color `primary-500` [D].
  - Email "contact@cyterobio.com" x 82, y 18, 252 × 31 [M].
  - `ri:linkedin-fill` icon (Remix Icon) x 1165, y 10, 48 × 48 [M], right-aligned. **Use the Remix Icon path inline** [D]. Profile URL not known yet → `href="#"` with a `TODO` comment [D]. **Remind the designer about the URL.**
- Top of the footer (y 0–210) is mostly occupied by Divider2 [M + S].

## Image placement summary

| Figma layer | File in `_assets/` | Section | Position / size |
| ----------- | ------------------ | ------- | --------------- |
| hero_img_VEGF_v04 | hero_img_VEGF_v04.png | Hero (page-level layer) | page x 296, y −82, 1193 × 1193 [M] |
| (inside Card with Tabs) | vial_VEGF / vial_TGF / vial_PDGF.png | Portfolio, one per tab | 470 × 470 [D], right side of the card [S] |
| aboutus_img_TGFb3 | TGFb3.png | About us | x 135, y 55, 1044 × 1044 [M] |
| cta_img_PDGF | PDGF.png | CTA | x 0, y 48, 1042 × 586 [M] |
| Logo | logo.svg | Nav | x 54, y 40, 265 × 78 [M] |
| Logo_footer | logo-footer.svg | Footer | 68 × 68 [M] |

## Open questions

1. ~~Exact backgrounds per section~~ → **Resolved** [D], see Backgrounds.
2. ~~Portfolio tabs content and interactivity~~ → **Resolved** [D]: click-to-switch client component, texts in the tab content table.
3. ~~Vial size/position~~ → **Resolved** [D]: 470 × 470, responsive `aspect-square`, max 470 px. Exact position inside the card still from the screenshot [S] (right side).
4. ~~Glow color and blur~~ → **Resolved** [D]: primary-500, layer blur 190 → CSS ~`blur(95px)`, verify visually; smaller on mobile.
5. ~~LinkedIn icon~~ → **Resolved** [D]: inline Remix Icon path. **Still open: profile URL** (`href="#"` + TODO until supplied).
6. ~~Contact button target~~ → **Resolved** [D]: no action for now, subtle hover only (to be proposed and shown).
7. ~~Hidden nanoDSF chart~~ → **Resolved** [D]: not used.
8. ~~Nav / footer alignment~~ → **Resolved** [D]: keep Figma alignment (x 54 / x 83), not in the container.
