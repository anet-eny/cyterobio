# CyteroBio – Desktop layout (Figma)

Source: Figma file `XLGAVtqgKObNCMSEj3M4rp`, frame `149:201` "Desktop" (1440 × 6304). Read on 2026-11-22 via Figma MCP: `get_metadata` (structure, positions, sizes) + one `get_screenshot` of the whole frame (549 × 2400 px, overview only). Do not re-read Figma for this.

**Source of every value:**
- **[M]** = from `get_metadata` (exact Figma coordinates, px)
- **[S]** = estimated from the low-res screenshot (colors, content, look; not exact)

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

## Backgrounds [S]

No section has its own background fill in the metadata, except Hero, which has a full-size `base` rounded-rectangle (1440 × 866) [M]. On the screenshot the page reads as **one continuous dark navy background** in the `neutral-900` → `primary-700` range, with lighter and darker zones [S]:

| Area | Look [S] | Likely token (to confirm) |
| ---- | -------- | ------------------------- |
| Nav + Hero | lighter at the top, fading to dark at the bottom | Gradient 1 (`bg-gradient-1`, primary-700 top → neutral-900 bottom) on `base` |
| Our services | dark | neutral-900 |
| Our portfolio → About us | gradually lighter again around the portfolio card, dark again below the molecule | gradient / soft glow, unclear |
| How we work | dark at the top, slightly lighter towards the bottom | Gradient 2-like? unclear |
| CTA + Footer | medium navy | unclear |

→ Exact backgrounds can't be read from the screenshot. Confirm per section (designer, or `get_design_context` on a single section, only with approval).

Glows: `Ellipse 1` in Hero (x 720, y 198, 346 × 344) [M] and `Ellipse 1` in About us (x 526, y 316, 442 × 412) [M] are light blurred spots behind the molecules [S]. Their color/blur is unknown.

## Content width (container)

| Element | x | width | Source |
| ------- | - | ----- | ------ |
| Service cards row | 100 | 1240 | [M] |
| Portfolio "Card with Tabs" | 102 | 1235 | [M] |
| Footer content row | 83 | 1213 | [M] |
| Nav logo | 54 | 265 | [M] |
| Workflow cards (outer edges) | 198 – 1233 | 1035 | [M] |

→ **Content width ≈ 1240 px** (100 px side margin on the 1440 frame). Proposal: `container` with max-width 1240 px content + fluid side padding. The nav logo (x 54) and footer (x 83) sit further out; treated as Figma inaccuracy, align them to the container (to confirm).

## Sections in detail

### 1. Nav (149:279)
- `Logo` instance (mark + wordmark): x 54, y 40, 265 × 78 [M]. Color `primary-100` (decided).
- No menu links, no button [M].

### 2. Hero (149:223)
- `base` rounded-rectangle 1440 × 866 [M] → background.
- `hero text` frame: x 190, y 43, 753 × 309 [M]. Has a **dashed rounded border** around the text [S] (box only, no SVG).
  - Headline "Let us design your next molecule." x 32, y 32 (in Group 1), 689 × 188 [M]; serif [S] → **Heading 1 Alt** (72 px), 2 lines.
  - Subline "We shape proteins around what your research needs." 562 × 30 [M]; sans, muted color [S].
- `Ellipse 1` glow x 720, y 198, 346 × 344 [M].
- `nanodsf_curve_axes 2` (chart) is **hidden** in Figma [M] → not built.
- **Image `hero_img_VEGF_v04`** is a page-level layer (not inside Hero): x 296, y −82, 1193 × 1193 [M] (page coordinates). It reaches behind the Nav and to the right edge of the frame. File: `hero_img_VEGF_v04.png`.

### 3. Our services (149:216)
- Heading x 597, y 54, 246 × 45 [M].
- `Cards` frame x 100, y 143, 1240 × 272 [M]: 3× `Service Card` 392 × 270 at x 0 / 424 / 848 [M] → **gap 32 px**.
- Card titles [S] (serif, ~Heading 3 Alt): "Protein & Enzyme Engineering", "In Silico Feasibility Analysis", "Confidential Contract Research". Body: Paragraph-size text.
- Card look [S]: translucent/glassy, light border, a colored (pink/violet) glow inside. Exact fills unknown.

### 4. Our portfolio (149:213)
- Heading x 578, y 42, 284 × 45 [M].
- `Card with Tabs` instance x 102, y 154, 1235 × 723 [M]. The metadata does not show its insides (instance).
- From the screenshot [S]:
  - 3 **tab pills** centered above the card: "VEGF-Pro" (active, filled), "TGF-β3-Pro", "PDGF-BB-Pro".
  - Card (glassy, gradient border, pink/violet glows): left column = "Recombinant VEGF-Pro" (Heading 1-ish, sans), description, "Chain length" + value, "Typical dissolution buffer" + value; right = **vial image**.
  - → The 3 vials are one per tab: `vial_VEGF.png`, `vial_TGF.png`, `vial_PDGF.png`. **Tabs = interactive client component** (content of TGF/PDGF tabs not visible in Figma).
- Vial position/size inside the card: unknown [M not available]; ≈ right side, ~25 % of card width [S].

### 5. About us (149:210)
- Heading "WHO ARE WE?" x 597, y 42, 247 × 45 [M].
- Paragraph x 597, y 162, 397 × 230 [M] (left-aligned with the heading, sits over the molecule's top-right area [S]).
- `Ellipse 1` glow x 526, y 316, 442 × 412 [M].
- **Image `aboutus_img_TGFb3`** x 135, y 55, 1044 × 1044 [M] → overflows the section bottom (994) by 105 px into How we work. File: `TGFb3.png`.

### 6. How we work (149:202)
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
- **Image `cta_img_PDGF`** x 0, y 48, 1042 × 586 [M] (left, bleeds to the left edge). File: `PDGF.png` (16:9 matches 1042 × 586).
- `Frame 3` x 912, y 324, 344 × 143 [M]:
  - "Want to work with us?" 344 × 42 [M]; serif [S] → Heading 2 Alt (32 px).
  - `Button` instance x 103.6, y 77, 136.8 × 66 [M] (incl. possible shadow/padding); label "Contact", outlined pill [S].

### 8. Footer (165:243)
- `Frame 2` x 83, y 210, 1213 × 68 [M]:
  - `Logo_footer` (mark only) 68 × 68 [M], color `primary-500` (decided).
  - Email "contact@cyterobio.com" x 82, y 18, 252 × 31 [M].
  - `ri:linkedin-fill` icon (Remix Icon) x 1165, y 10, 48 × 48 [M], right-aligned. **No SVG in `_assets/`**.
- Top of the footer (y 0–210) is mostly occupied by Divider2 [M + S].

## Image placement summary

| Figma layer | File in `_assets/` | Section | Position / size [M] |
| ----------- | ------------------ | ------- | ------------------- |
| hero_img_VEGF_v04 | hero_img_VEGF_v04.png | Hero (page-level layer) | page x 296, y −82, 1193 × 1193 |
| (inside Card with Tabs) | vial_VEGF / vial_TGF / vial_PDGF.png | Portfolio, one per tab | unknown; right side of the card [S] |
| aboutus_img_TGFb3 | TGFb3.png | About us | x 135, y 55, 1044 × 1044 |
| cta_img_PDGF | PDGF.png | CTA | x 0, y 48, 1042 × 586 |
| Logo | logo.svg | Nav | x 54, y 40, 265 × 78 |
| Logo_footer | logo-footer.svg | Footer | 68 × 68 |

## Open questions

1. Exact backgrounds per section (screenshot is not reliable).
2. Portfolio tabs: content for the TGF-β3-Pro and PDGF-BB-Pro tabs (text), and confirmation that tabs are interactive (click switches the card).
3. Vial size/position inside the portfolio card and card internals (instance not expanded in metadata).
4. Glow ellipses: color and blur.
5. LinkedIn icon: SVG asset (or allowed to use the Remix Icon path inline) and profile URL.
6. "Contact" button target (probably `mailto:contact@cyterobio.com`).
7. Hidden nanoDSF chart in Hero: confirm it's not used.
8. Nav logo (x 54) and footer row (x 83) are outside the 1240 content width; align to container or keep?
