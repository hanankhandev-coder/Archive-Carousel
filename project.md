# ARCHIVE (Northform) — Project Metadata & Replica Prompt Guide

---

## 1. Quick Submission Metadata

- **Short Description (Under 30 Characters)**:
  `3D Circular Funnel Archive` *(26 characters)*
- **Short Description (Under 30 Words)**:
  `An interactive 3D circular funnel project gallery and editorial visual archive built with Vanilla JS, CSS 3D cylinder transforms, and GSAP, inspired by Capitol Records.` *(25 words)*
- **Description (Concise Overview)**:
  `ARCHIVE is a full-viewport 3D circular project gallery inspired by Capitol Records and contemporary art direction studios. Built with Vite, Vanilla JavaScript, CSS 3D transforms, and GSAP without heavy WebGL shaders, it arranges 37 curated editorial photographs across four tapering horizontal rings that spin in alternating directions and scroll vertically like a 3D vortex. It includes a scattered Objects index, a layered Art collage view, a minimal About statement, a detail lightbox, and a pure Black/White theme switcher.`
- **Type**:
  `Interactive 3D Portfolio / Editorial Visual Archive / Creative Agency Showcase`
- **Vibe**:
  `Minimalist, Cinematic, Curatorial, High-Fashion Editorial, Brutalist Swiss Precision, Kinetic 3D`
- **Category**:
  - `Portfolio & Agency`
  - `3D & WebGL / CSS 3D`
  - `Photography & Editorial Archive`
  - `Interactive Exhibition`
- **Claude Model Used Most**:
  `Claude Opus 4.6 (with Claude 3.7 Sonnet for rapid UI iterations)`
- **How Many Tries**:
  `7 tries (iterative refinements from initial 3-ring prototype to final 4-tier tapering 3D cylinder funnel)`

---

## 2. Skills & Connectors Used

### Skills Used
- **`impeccable`**: Enforced high-craft layout discipline, negative-space calibration, sharp `0px` editorial framing, and zero-clutter typographic hierarchy.
- **`ponytail`**: Applied fluid kinetic motion curves, alternating ring counter-rotation, lerped scroll/drag momentum, and magnetic cursor micro-interactions.
- **`frontend-design`**: Structured the single-font `Inter` design system, dual theme variables (`#080809` Obsidian vs. `#FFFFFF` Pure White), and multi-view transitions.
- **`modern-web-guidance`**: Replaced heavy Three.js shader passes with hardware-accelerated CSS `preserve-3d` cylinder projection (`Z <= 0` calibration) for 60fps performance and native 1:1 Retina text sharpness.
- **`generative_ui`**: Designed the interactive 4-view architecture (`ARCHIVE`, `OBJECTS`, `ART`, `ABOUT`) and keyboard-navigable detail inspection modal.

### Connectors & Inspiration Sources Used
- **`Mobbin`**: Referenced layout patterns for minimal top navigation chrome, filterable index grids, and lightbox inspection flows.
- **`Higgsfield`**: Guided the high-contrast cinematic lighting, motion choreography, and atmospheric editorial photography curation.
- **`Capitol Records (capitolrecords.com)`**: Primary structural inspiration for the tapering 3D circular funnel gallery and vertical scroll-through-rings mechanic.
- **`Unsplash Editorial Curations`**: High-resolution (`w=1200&q=90`) 35mm and medium-format monochrome, cyanotype, architectural, and kinetic portrait photography.

---

## 3. Workflow (Step-by-Step Build Process)

1. **Reference Analysis & Direction**: Studied the Capitol Records 3D circular project funnel Alongside minimalist editorial studio archives (Sandcastle Studio, Kunumi) and curated 5 core reference photographs via Higgsfield/Unsplash.
2. **Architecture & Performance Pivot**: Started with a 3-ring prototype, then migrated from Three.js WebGL to **pure Vanilla JavaScript + CSS 3D Cylinder Transforms (`preserve-3d`) + GSAP** to eliminate GPU lag and achieve instant load times (`~96 kB` bundle).
3. **3D Funnel Math & Sharpness Calibration**: Engineered a 4-row tapering funnel (`940px -> 750px -> 590px -> 450px` radii) with negative Z-centers (`-820px` to `-940px`) inside an `1800px` perspective stage so front cards render at 1:1 native DOM resolution without bitmap upscaling blur.
4. **Solid Depth Shading (Zero Transparency Overlap)**: Set all cards to `opacity: 1` so front cards cleanly block back cards, using an internal solid `.ring-card-shade` overlay to darken back-hemisphere cards and `backface-visibility: hidden` on captions to prevent mirrored text.
5. **Unified Single-Font System & Theme Polish**: Standardized all typography to `Inter`, removed decorative brackets and image number badges, connected the `OBJECTS` / `ART` / `ABOUT` views, and calibrated the `B / W` switcher for Obsidian (`#080809`) and Pure White (`#FFFFFF`) modes.

---

## 4. Master Prompt (One-Shot Exact Replica Prompt)

Copy and paste the prompt below to recreate this exact website in a single shot:

```markdown
Build a full-viewport, 60fps 3D Circular Funnel Editorial Archive website using Vite + Vanilla JavaScript + HTML5 + CSS 3D Transforms + GSAP (DO NOT use React and DO NOT use Three.js/WebGL). It should feel like an award-winning curatorial agency archive inspired by https://www.capitolrecords.com.

### 1. Layout & 4-Row Tapering 3D Cylinder Funnel
- Full-screen viewport (`100vw x 100vh`, `overflow: hidden`) with a `.funnel-viewport` (`perspective: 1800px; perspective-origin: 50% 46%`) and `.funnel-world` (`transform-style: preserve-3d`).
- Create 4 stacked horizontal 3D rings (`.funnel-ring`, `transform-style: preserve-3d`) that taper downward like a funnel from largest at the top to smallest at the bottom:
  - Row 0 (Top): 10 cards, desktop radius `940px` (mobile `480px`), zCenter `-820px`, scale `1.00`, baseY `-195px`, speed `-0.052deg/frame`
  - Row 1 (Second): 10 cards, desktop radius `750px` (mobile `390px`), zCenter `-860px`, scale `0.85`, baseY `+155px`, speed `+0.058deg/frame`
  - Row 2 (Third): 9 cards, desktop radius `590px` (mobile `315px`), zCenter `-900px`, scale `0.72`, baseY `+455px`, speed `-0.064deg/frame`
  - Row 3 (Bottom): 8 cards, desktop radius `450px` (mobile `250px`), zCenter `-940px`, scale `0.60`, baseY `+715px`, speed `+0.072deg/frame`
- Apply `translate3d(0px, ringScreenY, zCenter) rotateX(-2.2deg) rotateY(totalRingDeg)` on each ring, and `rotateY(thetaDeg) translateZ(effectiveRadius) scale(effectiveScale)` on each card so the cards form a true 3D circular cylinder with zero vertical overlap between rows.
- Every `.ring-card` (`width: 236px`) must have `opacity: 1` (100% solid opaque — never make cards semi-transparent so back cards never bleed through front cards) and sharp `0px` corners with mixed editorial aspect ratios (`4:5` -> `214px` tall, `1:1` -> `192px` tall, `3:4` -> `224px` tall).
- Inside each card's image box, place a solid `.ring-card-shade` div (`background: var(--bg-color)`) whose opacity is `0` on the front half of the cylinder (`cos(angle) >= 0`) and smoothly increases up to `0.55` on the back half (`cos(angle) < 0`).
- Under each card, place a left-aligned `.ring-card-caption` with `backface-visibility: hidden` (so back-facing cards never show mirror-flipped text): title in `13.5px` medium (`#fff` in dark mode) and uppercase subtitle in `10.5px` (`#8a8a92`, `letter-spacing: 0.08em`). Do NOT put number badges on the images.

### 2. Typography & Dual Theme (`B / W`)
- Use ONLY ONE font family across the entire site: `Inter` (`--font-sans: 'Inter', sans-serif`). Do not use serif or monospace fonts, and do not use brackets `()` or `[]` in any navigation links or labels.
- Top header bar (`.ui-header`):
  - Left: `ARCHIVE` brand wordmark (`14px`, weight `600`, `letter-spacing: 0.08em`).
  - Center nav links: `ARCHIVE`, `OBJECTS`, `ART`, `ABOUT` with an underline on the active view.
  - Right: `BACK TO ARCHIVE` button (visible when inside secondary views) and a `B / W` theme switcher.
- Clicking `B` activates the Dark Theme (`--bg-color: #080809`, `--text-primary: #ffffff`). Clicking `W` activates the Light Theme with a pure full white background (`--bg-color: #ffffff`, `--text-primary: #0a0a0c`).

### 3. Motion & Interactions
- Continuous slow alternating auto-rotation on the 4 rings ( slows to `20%` when hovering a card).
- Vertical mouse wheel or vertical touch-drag scrolls down/up through the 4 funnel tiers (`targetScrollY` from `-40px` to `+740px` with lerped damping) and expands lower rings slightly (`focusBoost`) as they rise to eye level.
- Horizontal click-drag or touch-drag spins all 4 rings with momentum.
- Mouse movement tilts `.funnel-world` (`±2.8°` Y, `±1.8°` X) with smooth lerp.
- Custom magnetic cursor (`#custom-cursor`) that expands from a `5px` dot into a `46px` circle reading `VIEW` when hovering a card.
- Clicking any card opens a blurred Detail Lightbox overlay with a larger image, title, subtitle, curatorial description, `PREV` / `NEXT` buttons, and `CLOSE` button.

### 4. Connected Secondary Views & Modular Code
- `OBJECTS` view: 4-column scattered editorial grid (`.scatter-1` to `.scatter-4` vertical offsets) with `ALL`, `OBJECTS`, `ART`, `ARCHITECTURE` filter buttons.
- `ART` view: 6-frame overlapping editorial collage showcase in the center of the viewport.
- `ABOUT` view: Centered studio manifesto with 3 discipline columns (`01 OBJECTS`, `02 ART`, `03 SPATIAL`) and a `RETURN TO ARCHIVE` button.
- Organize the code cleanly into `src/data.js` (42 high-res `w=1200&q=90` Unsplash editorial photography items), `src/scene.js`, `src/rings.js`, `src/interaction.js`, `src/ui.js`, `main.js`, and `style.css`.
```

---

## 5. Iterative Follow-Up Prompts (If Building Step-by-Step)

1. **Prompt 1 (Core 3D Carousel Prototype)**:
   *"Build a full-screen archive section with a 3D circular carousel of editorial image cards using Vite, vanilla JS, and GSAP. Include alternating ring rotation, drag inertia, mouse parallax, a custom VIEW cursor, and a detail modal."*
2. **Prompt 2 (Capitol Records Funnel & Vanilla JS Optimization)**:
   *"Make the circular project gallery taper like a 4-row 3D funnel inspired by capitolrecords.com where the top row is largest and lower rows get progressively smaller, allowing vertical scrolling down the funnel and horizontal drag spinning using pure Vanilla JS and CSS 3D without Three.js lag."*
3. **Prompt 3 (Visual Polish, Single Font & Solid Card Depth)**:
   *"Use only the Inter sans-serif font across the whole site, remove brackets and image number badges, make the light mode background pure white (#ffffff), keep all funnel cards 100% opaque so overlapping images never look see-through, and size the 4-row 3D cylinder radii to 940px, 750px, 590px, and 450px."*
