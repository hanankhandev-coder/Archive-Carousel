Live: https://hanankhandev-coder.github.io/Archive-Carousel/

# ARCHIVE — 3D Circular Funnel & Editorial Visual Catalogue

A full-viewport, hardware-accelerated **3D Circular Funnel Project Gallery** built with **Vite + Vanilla JavaScript + HTML5 + CSS 3D Transforms + GSAP** (zero Three.js/WebGL overhead). Inspired by the circular project funnel of **[Capitol Records](https://www.capitolrecords.com)** and minimalist editorial design archives, it pairs a 4-tier tapering 3D cylinder carousel with a scattered editorial index (`OBJECTS`), a layered visual composition showcase (`ART`), a minimal studio manifesto (`ABOUT`), and a dual Obsidian/Pure-White theme toggle (`B / W`).

---

## 1. Design Philosophy & Visual Direction

- **Tapering 3D Funnel Architecture**: Instead of a flat grid or uniform cylinder, 37 curated editorial works are arranged across **4 stacked horizontal rings** that taper downward like a 3D vortex/funnel—from a wide `940px` radius top ring down to a `450px` radius bottom ring.
- **100% Solid Card Presence (Zero Ghosting)**: Every card maintains `opacity: 1` so front-facing works cleanly occlude background cards without double-exposure transparency bleed. Depth attenuation on the back half of each ring is achieved via a solid internal `.ring-card-shade` layer that blends toward the active theme background (`#080809` in Dark Mode, `#FFFFFF` in Light Mode).
- **Native 1:1 Retina Sharpness**: Each ring's Z-origin (`-820px` to `-940px` inside a `1800px` CSS perspective stage) places the front-most arc near `Z = 0`. Cards never upscale above `1.0x` their DOM raster size and never use `filter: brightness()`, ensuring razor-sharp typography and crisp `1200px` editorial photography.
- **Unified Single-Font Swiss Typography**: The entire interface uses **Inter** (`--font-sans`) with tight negative tracking (`-0.01em` to `-0.02em`) for titles and clean uppercase tracking (`0.06em` to `0.08em`) for metadata, navigation, and category labels—free of decorative brackets or image number badges.

---

## 2. 3D Funnel Geometry & Mathematical Specifications

| Funnel Tier | Card Count | Desktop Radius | Mobile Radius | Desktop Z-Center | Base Scale | Desktop Y-Offset | Auto-Spin Speed | Direction |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **Row 0 (Top Tier)** | `10` | `940px` | `480px` | `-820px` | `1.00` | `-195px` | `-0.052°/frame` | Clockwise |
| **Row 1 (Upper-Mid)** | `10` | `750px` | `390px` | `-860px` | `0.85` | `+155px` | `+0.058°/frame` | Counter-Clockwise |
| **Row 2 (Lower-Mid)** | `9` | `590px` | `315px` | `-900px` | `0.72` | `+455px` | `-0.064°/frame` | Clockwise |
| **Row 3 (Funnel Tip)** | `8` | `450px` | `250px` | `-940px` | `0.60` | `+715px` | `+0.072°/frame` | Counter-Clockwise |

### Key 3D Rendering Mechanics
1. **Perspective Stage (`.funnel-viewport`)**:
   - `perspective: 1800px; perspective-origin: 50% 46%;`
   - `.funnel-world` and `.funnel-ring` maintain `transform-style: preserve-3d`.
2. **Ring Transform Formula**:
   ```js
   ring.el.style.transform = `translate3d(0px, ${ringScreenY}px, ${ring.zCenter}px) rotateX(-2.2deg) rotateY(${totalRingDeg}deg)`;
   ```
   - The subtle `-2.2deg` pitch reveals the back arc of each ring slightly above the front arc while preserving `95px–106px` of vertical clearance between adjacent rows.
3. **Card Cylinder Placement Formula**:
   ```js
   card.el.style.transform = `rotateY(${card.thetaDeg}deg) translateZ(${effectiveRadius}px) scale(${effectiveScale})`;
   ```
   - `.ring-card-caption` uses `backface-visibility: hidden` so captions on the front hemisphere (`-90° < θ < +90°`) are crisp and readable, while back-hemisphere captions automatically hide so mirror-reversed text never appears.
4. **Mixed Editorial Aspect Ratios**:
   - Base card width: `236px` (`-118px` centered X-offset).
   - `4:5` portrait: `236px × 214px`
   - `1:1` square: `236px × 192px`
   - `3:4` tall portrait: `236px × 224px`
   - Sharp `0px` corners with a subtle `1px` hairline border.

---

## 3. Animations & Interaction System

- **Dual-Axis Scroll & Spin (`src/interaction.js` & `src/rings.js`)**:
  - **Vertical Mouse Wheel / Touch Vertical Drag**: Scrolls vertically down and up through the 4 funnel tiers (`targetScrollY` from `-40px` to `+740px` with `0.085` lerp damping) while imparting a subtle rotational impulse to all rings.
  - **Dynamic Eye-Level Expansion (`focusBoost`)**: As lower funnel rows (`Row 1–3`) rise toward eye level during vertical scrolling, their radius expands by up to `+10.4%` and their scale boosts by up to `+0.16` so smaller tiers open up for inspection.
  - **Horizontal Click-Drag / Touch-Drag / Horizontal Trackpad Swipe**: Spins all 4 rings with momentum and alternating directional factors (`dirFactor = rIndex % 2 === 0 ? 1 : -0.9`), easing smoothly back into continuous auto-rotation.
- **Mouse Camera Parallax (`src/scene.js`)**:
  - Moving the cursor tilts `.funnel-world` by up to `±2.8°` on the Y-axis and `±1.8°` on the X-axis with `0.06` lerp smoothing.
- **Card Hover & Custom Magnetic Cursor (`#custom-cursor`)**:
  - Hovering a front-hemisphere card scales its image container (`scale(1.04)`), elevates its shadow, slows ring auto-rotation to `20%`, dims non-hovered cards via `.ring-card-shade`, and expands the `10px` cursor dot into a `46px` circle displaying `VIEW`.
- **Detail Lightbox Fly-To & Keyboard Navigation (`src/ui.js`)**:
  - Clicking any card triggers `sceneManager.flyToCard()` and opens the full-screen blurred detail overlay with `PREV` / `NEXT` project stepping, `CLOSE` button, and keyboard shortcuts (`Escape`, `ArrowLeft`, `ArrowRight`).
- **Reduced Motion Accessibility**:
  - Automatically detects `prefers-reduced-motion: reduce` to disable continuous auto-rotation and camera parallax.

---

## 4. Typography & Color Tokens

### Typography (`Inter` Single-Font System)
| Element | Font Family | Size | Weight | Tracking | Transform |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **Brand Wordmark (`ARCHIVE`)** | `Inter` | `14px` | `600` | `0.08em` | Uppercase |
| **Top Navigation Links** | `Inter` | `12px` | `500` | `0.06em` | Uppercase |
| **Funnel Card Title** | `Inter` | `13.5px` | `500` | `-0.01em` | Title Case |
| **Funnel Card Subtitle** | `Inter` | `10.5px` | `500` | `0.08em` | Uppercase |
| **Index Heading** | `Inter` | `clamp(28px, 4vw, 48px)` | `500` | `-0.02em` | Title Case |
| **Detail Modal Title** | `Inter` | `20px` | `500` | `-0.02em` | Title Case |
| **Footer Status & Hints** | `Inter` | `10px` | `500` | `0.08em` | Uppercase |

### Theme Tokens (`B / W` Switcher)
| Token | Dark Theme (`B` — Default) | Light Theme (`W` — `body.light-theme`) |
| :--- | :--- | :--- |
| `--bg-color` | `#080809` (Obsidian Black) | `#FFFFFF` (Pure Full White) |
| `--bg-elevated` | `rgba(8, 8, 9, 0.94)` | `rgba(255, 255, 255, 0.96)` |
| `--text-primary` | `#FFFFFF` | `#0A0A0C` |
| `--text-secondary` | `#8A8A92` | `#62626A` |
| `--text-muted` | `#52525A` | `#9898A0` |
| `--border-color` | `rgba(255, 255, 255, 0.14)` | `rgba(0, 0, 0, 0.12)` |

---

## 5. Multi-View Site Architecture

1. **`ARCHIVE` (Default View)**: Full-viewport 4-tier 3D circular funnel with vertical scroll descent and horizontal drag spin.
2. **`OBJECTS` (`#objects-view`)**: Scattered 4-column editorial index grid with staggered vertical offsets (`.scatter-1` through `.scatter-4`) and live category filter buttons (`ALL`, `OBJECTS`, `ART`, `ARCHITECTURE`).
3. **`ART` (`#art-view`)**: 6-frame overlapping editorial collage composition (`.slot-top`, `.slot-left`, `.slot-beige`, `.slot-center-main`, `.slot-center-small`, `.slot-bottom-right`) with hover z-index elevation and direct lightbox inspection.
4. **`ABOUT` (`#about-view`)**: Minimalist centered curatorial statement highlighting the archive's three core disciplines (`01 OBJECTS`, `02 ART`, `03 SPATIAL`) and a `RETURN TO ARCHIVE` action button.

---

## 6. Project Structure & Running Locally

```text
archive-carousel/
├── index.html                  # Standalone app shell (open directly in any browser)
├── style.css                   # CSS 3D funnel stage, theme tokens & responsive layouts
├── bundle.js                   # Self-contained JS bundle (3D funnel math, interactions, UI & GSAP)
├── favicon.svg                 # Custom geometric concentric ring SVG favicon
├── editorial/                  # 5 curated local high-res editorial photographs (editorial-1..5.jpg)
├── README.md                   # Complete design, math, animation & architecture documentation
└── project.md                  # Replica prompt guide & project submission metadata
```

### How to Run
1. **Direct Browser Launch (Zero Setup)**:
   - Double-click `index.html` to open it directly in Chrome, Edge, Safari, or Firefox (`file:///` works out of the box).
2. **Via Local Static Server (Optional)**:
   ```bash
   npx serve .
   ```
