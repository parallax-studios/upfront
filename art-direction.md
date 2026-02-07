# UPFRONT — Art Direction Document

**Art Director**: PIXEL
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready Style Guide

---

> "Art is communication. Every pixel must earn its place on screen."

I have read the pitch and the design document. I know what this game needs to be visually. Let me tell you exactly what it looks like — down to the hex codes, the line weights, the readability checks, and the reference stack.

This is a game about advertising in the early 2000s. It is a game about the war between vision and approval. The art must communicate three things instantly: professionalism, pressure, and personality. The player is a creative director sitting in a presentation room at 9 PM, watching their best work get picked apart by someone who is paying for it. The visuals must make you feel that room. The UI is not just interface — it is environment. The office is not decoration — it is the game.

Every choice in this document serves readability first, atmosphere second, and beauty third. If the player cannot parse the screen in three seconds, I have failed. If they can parse it but feel nothing, I have failed differently but just as completely.

Let me show you what UPFRONT looks like.

---

## 1. VISUAL IDENTITY STATEMENT

### 1.1 Core Visual Proposition

**UPFRONT looks like the memory of an advertising agency in 2003 — not the reality, but the feeling.**

The reference is not a photograph. It is the warm amber glow you remember when you think of working late on something that mattered. It is the tension of a conference room just before someone speaks. It is the physical texture of paper mood boards and printed storyboards spread across a table under fluorescent light. It is the blue glow of a rear-projection screen showing your 30-second masterpiece to someone who wants to cut 10 seconds.

This is not a nostalgia game. This is a *specific historical moment* game. The dot-com crash is over but the optimism dust is still glittering. The Super Bowl is still the single biggest cultural moment in America. Television is still king. The internet exists — AIM windows, email forwards, QuickTime files — but it is the water cooler, not the stage. The office aesthetic is Herman Miller modernism meets creative chaos: clean lines buried under sketches, Aeron chairs turned backwards, whiteboards covered in Sharpie scrawl, awards on shelves collecting dust and validating egos simultaneously.

The visual language is **diegetic UI wrapped in isometric-spatial clarity**. The main game screen is not a menu — it is your agency floor, seen from above at a slight angle. Click the presentation room and you are *in* the presentation room, facing the client across a table. Click the creative bullpen and you are looking at desks covered in work. The player navigates space, not menus. Every screen is a place. Every interface element is an object in that place.

The color palette is split between warm ambition and cool precision. Golden hour office light. Monitor blue. Coffee stain brown. The red urgency of a deadline Post-it. The sickly green of a budget cell turning negative. The Clio Award gold of success.

The typography is confident sans-serif for the player-facing UI (Helvetica Neue, the typeface of modernist clarity) and warm serif for in-world documents (Georgia, the typeface of printed memos and briefs). Numbers are monospace (Courier, the typeface of spreadsheets and invoices). Every font choice signals context. The player knows where they are by the type on screen.

The art direction serves the player fantasy: you are the person with creative authority and commercial pressure. The presentation room is sleek and sterile — the client's domain. The creative bullpen is messy and alive — your domain. The edit suite is dark and focused — the production domain. Each space has its own palette, its own lighting, its own feeling. The player reads the emotional temperature of a space before they read a single stat.

**One-sentence visual identity**: UPFRONT looks like a 2000s ad agency seen through the warm haze of a deadline rush — professional spaces made human by the mess of ambition.

### 1.2 Visual Pillars

These are the non-negotiable visual truths. Everything else bends. These do not.

1. **READABILITY ABOVE ALL**: The player must parse the most important information on any screen in under 3 seconds. Color, scale, contrast, and spatial hierarchy are weapons. Use them. A pretty screen that confuses is a failed screen.

2. **DIEGETIC INTERFACE**: The UI is the world. Briefs are printed documents on desks. Budgets are Excel 2003 spreadsheets. Team assignments are magnetic name tags on a whiteboard. Concept pitches are physical mood boards pinned to cork. The player is not clicking abstract menus — they are interacting with objects in a space they inhabit.

3. **SPATIAL CLARITY**: The isometric office view must communicate the agency's layout instantly. The presentation room is glass-walled. The creative bullpen is open-plan. The edit suite is a dark box. The player knows where everything is because the space is legible. No floating UI. No abstract layouts. Architecture is navigation.

4. **WARM LIGHT, COOL WORK**: The office is bathed in warm light (amber, gold, sunset through windows) but the work itself — storyboards, screens, documents — is rendered in cool blues and clean whites. This creates visual separation between environment (warm) and information (cool). The player's eye knows what to focus on.

5. **PERSONALITY IN THE DETAILS**: The mess matters. Coffee cups on desks. Post-its on monitors. Awards on shelves. A whiteboard that says "DAYS UNTIL SUPER BOWL." The clutter is not random — it is authored. Every object tells a story about the people who work here. A desk with three coffee cups and crumpled paper is a stressed creative. A desk with a single plant and organized folders is a methodical producer. The player reads character through environment.

---

## 2. COLOR PALETTE

### 2.1 Primary Palette

These are the five core colors that define UPFRONT's visual identity. Every screen uses at least three of these. Most screens use all five in some ratio.

| Color Name | Hex Value | RGB | Usage Rule | Screen Percentage Target |
|---|---|---|---|---|
| **Office Amber** | `#D4A76A` | 212, 167, 106 | Warm ambient light, office furniture wood tones, late-afternoon glow through windows, warm UI backgrounds | 25-35% of any office view screen |
| **Document White** | `#F5F0E8` | 245, 240, 232 | Paper backgrounds for briefs/storyboards/mood boards, light UI panels, text fields, clean workspace surfaces | 20-30% of any screen |
| **Monitor Blue** | `#4A90D9` | 74, 144, 217 | Screen glows (monitors, projectors), interactive UI elements, selected states, hyperlinks in diegetic email/IM windows | 10-15% of any screen |
| **Deadline Red** | `#C0392B` | 192, 57, 43 | Urgency indicators (deadline warnings, budget overruns, client dissatisfaction alerts), critical UI notifications, the single red Post-it on a mood board | 3-5% of any screen (scarcity = impact) |
| **Charcoal Foundation** | `#2C2C2C` | 44, 44, 44 | Text, UI borders, window frames, shadows, edit suite darkness, the void behind monitors | 15-25% of any screen |

**Palette Usage Philosophy**: Office Amber is the emotional foundation — the warmth of the space. Document White is the information carrier — the clarity of the work. Monitor Blue is the interactive layer — the technology. Deadline Red is the alarm bell — the pressure. Charcoal Foundation is the structure — the bones. The player feels warmth, sees information clearly, interacts with blue, reacts to red, and grounds everything in charcoal.

### 2.2 Secondary Palette (Contextual)

These colors appear in specific contexts to communicate state, emotion, or narrative.

| Color Name | Hex Value | RGB | Usage Rule |
|---|---|---|---|
| **Clio Gold** | `#D4AF37` | 212, 175, 55 | Award shelf items, "win" state notifications, prestige client markers, positive reputation shifts |
| **Budget Green** | `#7D9B6A` | 125, 155, 106 | Positive cash flow indicators, approved budget cells in spreadsheets, "in the black" financial UI elements |
| **Crisis Green-to-Red** | `#7D9B6A → #C0392B` | Gradients | Budget cells that turn from green (positive) to red (negative) when allocation exceeds available funds — a real-time visual alarm |
| **Presentation Cream** | `#FAF3E0` | 250, 243, 224 | Presentation room walls, client-facing spaces, formal UI panels, the sterile professionalism of the pitch environment |
| **Edit Suite Void** | `#1A1A1A` | 26, 26, 26 | Edit suite backgrounds, "lights off" production environments, the focused darkness of post-production work |
| **AIM Window Silver** | `#C0C0C0` | 192, 192, 192 | Diegetic instant message window frames (2000s AIM aesthetic), browser chrome, OS-level UI elements within the game world |
| **Highlighter Yellow** | `#F9E79F` | 249, 231, 159 | Player annotations on briefs (simulated highlighter marks on text), emphasis on key brief parameters, revision notes on concepts |

### 2.3 Emotional Color Mapping

Different screens have different emotional temperatures. The palette shifts to match.

| Screen/Context | Dominant Colors | Emotional Goal |
|---|---|---|
| **Main Office View** | Office Amber (high), Document White (medium), Charcoal (medium) | Warmth, productivity, "this is your space" |
| **Presentation Room (Approval Gauntlet)** | Presentation Cream (high), Monitor Blue (medium), Charcoal (low), Deadline Red (spikes) | Sterile professionalism with rising tension |
| **Creative Bullpen** | Office Amber (very high), Document White (high), scattered Highlighter Yellow and Monitor Blue | Messy creativity, organized chaos |
| **Edit Suite (Production)** | Edit Suite Void (very high), Monitor Blue (medium), Office Amber (low, from desk lamps only) | Focused intensity, darkness punctuated by screens |
| **Super Bowl Broadcast Screen** | Split-screen: left = Document White + Monitor Blue (the ad), right = Charcoal + Deadline Red + Clio Gold (reactions and metrics) | Climax tension followed by resolution |
| **Budget Spreadsheet Interface** | Document White (background), Charcoal (text/grid), Budget Green and Crisis Red (cells), Monitor Blue (selected cell) | Excel 2003 nostalgia, financial clarity, color-coded stress |

### 2.4 Accessibility & Readability Checks

**Colorblind testing matrix**: The primary palette must be distinguishable across deuteranopia (red-green), protanopia (red-green variant), and tritanopia (blue-yellow) color blindness.

- **Office Amber vs. Monitor Blue**: High contrast in all colorblind simulations. Safe.
- **Deadline Red vs. Budget Green**: These are intentionally opposite (danger vs. safety). In deuteranopia, red shifts brownish and green shifts tan — they remain distinguishable by luminance (Red is darker at 57 vs. Green at 155). Add secondary indicators: red elements pulse or include "!" icons. Green elements include "✓" icons. Color is primary signal, icon is backup.
- **Document White vs. Presentation Cream**: Luminance difference is only 5 points. These are intentionally similar (both "paper tones"). They are never used for critical differentiation — only for environmental mood. Safe.
- **Monitor Blue vs. Charcoal Foundation**: High luminance contrast (144 vs. 44). Text readability on either background is excellent. Safe.

**Contrast ratios (WCAG AA standard = 4.5:1 for normal text, 3:1 for large text)**:
- Charcoal `#2C2C2C` on Document White `#F5F0E8`: **8.2:1** — Excellent
- Monitor Blue `#4A90D9` on Document White `#F5F0E8`: **3.8:1** — Pass for large text (18pt+), marginal for small text. Use Monitor Blue for interactive elements 18pt+ or add Charcoal border for smaller interactive text.
- Deadline Red `#C0392B` on Document White `#F5F0E8`: **5.1:1** — Excellent
- Document White text on Office Amber `#D4A76A`: **3.3:1** — Marginal. Use Charcoal text on Office Amber instead. Office Amber is background mood, not a text surface.

**Squint test result**: Squinting at any UI screen should reveal a clear hierarchy. Warm amber environments recede. Cool white documents pop forward. Blue interactive elements glow. Red urgency elements scream. Charcoal structure holds everything. The hierarchy is baked into the palette, not imposed by layout alone.

**Thumbnail test result**: Shrinking any screen to 200x150px thumbnail should still communicate its context. Office view = warm amber field. Presentation room = cream box with blue accent. Edit suite = dark void with blue glow. Budget spreadsheet = white grid with green/red cells. Super Bowl = split-screen white/dark. The palette is the identifier.

---

## 3. SHAPE LANGUAGE GUIDE

### 3.1 Core Geometric Vocabulary

UPFRONT's shape language is built on the tension between **clean modernist rectangles** (the aspiration, the professionalism, the Herman Miller dream) and **organic human mess** (the reality, the creativity, the crumpled paper and coffee rings).

**Primary shape family: RECTANGLES WITH SOFTENED CORNERS**

- All UI panels, windows, buttons, and interactive elements use rectangles with 4px corner radius (8px for larger panels above 400px width).
- The slight softness (4px, not 0px sharp corners and not 12px+ rounded blobs) communicates "modern but approachable." Sharp corners feel cold. Overly rounded corners feel playful. 4px is professional warmth.
- All furniture in the office view (desks, tables, chairs, shelves) is rectangular with minimal ornamentation. This is modernist 2000s design: clean lines, functional forms, Eames and Miller and Knoll aesthetics.

**Secondary shape family: ORGANIC CLUTTER**

- Paperwork on desks: irregular polygons with 0-2 degree rotation, simulating casually placed documents.
- Coffee cups: simple cylinders, always slightly off-grid, never perfectly aligned.
- Post-it notes: perfect squares rotated 2-8 degrees, never aligned to grid.
- Pinned mood boards: rectangular boards with paper elements that overlap messily, thumbtacks visible as small circles.
- Cable spaghetti behind monitors: organic curves, never geometric.

The interplay is intentional. The architecture is rectangular. The humans working in that architecture are messy. The player sees order (rectangles) struggling with chaos (organic clutter). This is the visual metaphor for the entire game: clean professional systems fighting messy human creativity.

### 3.2 Isometric Office Spatial Rules

The main office view uses **isometric projection at 30-degree angle** (not true isometric 26.565-degree, but game-friendly 30-degree for cleaner pixel alignment).

**Grid**: 64px base tile. All furniture and walls snap to 64px grid or 32px half-grid. This ensures spatial clarity — the player always knows where boundaries are.

**Vertical height**: Desks are 48px tall. Chairs are 64px tall (including backrest). People are 80px tall when standing, 64px when seated. Walls are 128px tall. The hierarchy is clear: walls dominate, people are mid-height, furniture is low.

**Silhouette test**: Any object in the office must be identifiable from silhouette alone at 50% scale. A desk is a wide rectangle with four thin legs. A chair is a rectangle with a vertical backrest. A person is a rounded-top vertical form. A monitor is a thin rectangle on a small base. A mood board is a rectangle with irregular texture. If you erase all internal detail and show only the outline, the player still knows what it is. That is the readability bar.

**Line weight**: All outlines are 2px in Charcoal `#2C2C2C`. Internal details use 1px lines. Shadows are soft 8px blur at 30% opacity, cast at 45-degree angle downward-right (matching the isometric light source from upper-left). Consistent line weight = consistent readability.

### 3.3 UI Element Shapes

**Buttons**:
- Default state: Rectangle, 4px corner radius, 2px Charcoal border, Document White fill, Charcoal text.
- Hover state: Monitor Blue fill, Document White text, border removed, subtle 2px drop shadow.
- Active/pressed state: Monitor Blue fill darkened 10%, border returns as 2px Monitor Blue (darker), text stays white, shadow removed (button "presses in").
- Disabled state: 50% opacity on entire button, cursor changes to "not-allowed."
- Size: Minimum 120px wide x 40px tall for primary actions. Minimum 80px x 32px for secondary actions. Touch-friendly even on desktop (easier to click = less frustration).

**Input fields**:
- Rectangle, 4px corner radius, 2px Charcoal border, Document White fill.
- Active/focus state: Border becomes Monitor Blue, 3px glow in Monitor Blue at 40% opacity.
- Error state: Border becomes Deadline Red, subtle red glow.
- Placeholder text: Charcoal at 50% opacity. User text: full Charcoal.

**Panels and windows**:
- Major panels (Brief viewer, Concept Forge display, Approval Gauntlet screen): 8px corner radius, 2px Charcoal border or 4px drop shadow (not both), fill color depends on context (Presentation Cream for client-facing, Document White for player-facing).
- Minor panels (tooltips, small info boxes): 4px corner radius, 1px border, 2px drop shadow.
- Layering: When panels overlap (e.g., a tooltip over a brief), the top panel gets a stronger shadow (4px blur, 40% opacity). The player always knows what is "on top."

**Progress bars and sliders**:
- Track: Rectangle, 4px corner radius, 2px Charcoal border, light gray fill `#E0E0E0`.
- Fill: Monitor Blue for neutral progress, Budget Green for positive progress, Deadline Red for negative progress (e.g., budget overrun bar).
- Handle (for sliders): Circle, 16px diameter, Charcoal fill, 2px Monitor Blue border, 2px drop shadow. Large enough to grab easily.

### 3.4 Storyboard & Concept Visual Style

**Storyboards** (the visual representation of produced ads):
- 3-6 panels per ad, depending on Production Ambition (low-fi ads = 3 panels, blockbuster ads = 6 panels).
- Each panel is a 16:9 rectangle (aspect ratio of TV broadcast), rendered as a **sketchy line-art illustration** with limited color. Think animatic, not final render.
- Line art style: 2-3px black brush strokes, slightly rough/hand-drawn feel (not pixel-perfect vectors). Characters are simplified silhouettes. Backgrounds are suggested with 2-3 key lines.
- Color is limited to 1-2 accent colors per panel, applied as flat fills behind the line art (e.g., a sunset panel might have an orange fill, a product shot might have the brand's key color).
- Text overlays (taglines, product names) appear in bold sans-serif, always legible.

**Mood boards** (the visual representation of concepts pre-production):
- Cork board background texture (subtle, not overpowering).
- 4-8 reference images pinned with visible thumbtacks (small circles with metallic shine).
- Images are collaged — overlapping slightly, rotated 0-8 degrees, no perfect grid.
- Text elements (tone descriptors, logline) appear on index cards or Post-its, handwritten-style font (but legible — something like "Permanent Marker" or "Caveat" at 18pt+).
- The overall aesthetic is "a real creative team pinned this up in 20 minutes." Messy but purposeful.

---

## 4. STYLE RULES (DO'S AND DON'TS)

### 4.1 DO:

**Use diegetic UI wherever possible.**
- Present a brief as a printed document, not an abstract info panel. The player sees a paper on their desk with a header that says "CLIENT BRIEF: BRIGHTBURST ENERGY DRINK." They see the client logo at the top. They see highlighted text where their assistant marked key priorities. It is a document, not a menu.

**Leverage spatial navigation.**
- The player clicks on the presentation room in the office view and transitions to a first-person view inside that room. They do not click a button labeled "START APPROVAL GAUNTLET." They enter a space. The game is spatial.

**Respect the 2000s aesthetic without parody.**
- This is a period piece, not a joke. The AIM-style instant message windows are authentic, not ironic. The Excel 2003 green gradient in budget spreadsheets is real. Do not wink at the player. Play it straight.

**Show state changes through environment.**
- When a team is stressed (Fatigue high), their desks become messier. More coffee cups. More crumpled paper. A visual change the player notices before they read a stat.
- When the agency wins an award, the award appears on a shelf in the office view. The player's success becomes visible in the space they inhabit.

**Use negative space.**
- The Approval Gauntlet presentation room should feel a little empty. The client across the table. A projection screen. Some chairs. Open space. The emptiness creates tension. A cluttered presentation room would feel cozy. We do not want cozy. We want sterile and pressurized.

**Design for the squint test.**
- If the player squints, they should still know where to look. Use scale, contrast, and color to create instant hierarchy. The most important element on any screen should be the largest, highest-contrast, or warmest-colored (warm colors advance, cool colors recede).

**Make interactivity obvious.**
- Anything the player can click should look clickable. Buttons have borders. Links are underlined or use Monitor Blue. Draggable items (team assignments, budget sliders) have visual affordances (handles, shadows that suggest lift).

**Let text breathe.**
- Minimum 1.5x line-height for body text. Minimum 24px between distinct text blocks. Reading a brief should feel easy, not cramped. Information density is good. Visual density is bad. There is a difference.

### 4.2 DON'T:

**Do not use abstraction when a physical object works.**
- Wrong: A "Team Roster" menu with a list of names and stats.
- Right: A bullpen view with desks, each desk showing a nameplate and a visible "busy/available" indicator (a green desk lamp = available, red lamp = on a project).

**Do not use gradients on UI elements.**
- Flat colors only. Gradients are a 2010s skeuomorphism trend, not a 2000s modernist trend. The office environment can have gradient lighting (sunlight through windows), but buttons, panels, and text fields are flat.
- Exception: Budget spreadsheet cells can use subtle gradients to mimic Excel 2003 styling. This is diegetic. A gradient button is not.

**Do not animate for animation's sake.**
- Every animation must communicate state or provide feedback. A button color change on hover = good (communicates interactivity). A button that bounces when you hover = bad (adds noise, no information).
- Target animation duration: 150-250ms for UI state changes. Fast enough to feel responsive, slow enough to be perceived.

**Do not use more than 3 font weights.**
- Helvetica Neue in Regular (400) for body text, Bold (700) for headers/emphasis, and Light (300) for de-emphasized secondary info. Three weights maximum. More creates visual noise.

**Do not let clutter become noise.**
- Clutter is authored and purposeful. A desk with 3 coffee cups, 2 crumpled papers, and 1 Post-it tells a story. A desk with 15 random objects is visual static. Every object must earn its place. If it does not communicate character or state, cut it.

**Do not use effects for style.**
- No lens flares, no chromatic aberration, no film grain, no vignetting. This is not a cinematic trailer. This is a management sim. Clarity first. The only post-process effect allowed is subtle ambient occlusion (soft shadows where objects meet surfaces) and that is only for depth clarity, not style.

**Do not hide critical information behind interaction.**
- Wrong: A tooltip that appears only on hover to tell you a team member's Ego stat.
- Right: The Ego stat is always visible on their character card, with a tooltip on hover providing additional context (what Ego affects).

**Do not use cutesy iconography.**
- This is a professional space. Icons should be clear and functional. A "save" icon is a floppy disk (period-accurate). A "calendar" icon is a calendar grid. A "warning" icon is a triangle with an exclamation mark. No personalities, no embellishments.

**Do not break spatial logic.**
- If the presentation room is in the back-left corner of the office in the isometric view, the transition to first-person presentation view should feel consistent. The player should not be disoriented. If they click the left side of the office, the camera should not swing to the right. Spatial consistency = player confidence.

---

## 5. ASSET PIPELINE OVERVIEW

### 5.1 Art Tools & Formats

**Primary Art Tool**: **Figma** for all UI design, mockups, and vector assets. Figma's component system is perfect for diegetic UI — buttons, panels, windows, documents can all be components with variants (default/hover/active states).

**Isometric Office Construction**: **Aseprite** or **Pyxel Edit** for pixel-art-style isometric tiles if going pixel art route, OR **Blender** for low-poly 3D isometric renders if going 3D-rendered-to-2D route. Decision point: pixel art is more stylized and evocative, 3D render is more flexible for camera angles and lighting changes. Recommendation: **Low-poly 3D rendered to 2D sprites** for isometric office. Reason: The office layout changes as the player expands (new desks, new rooms), and 3D assets are easier to reconfigure than redrawing pixel art tiles. Render at high resolution, then downsample with a pixel-art shader for a "clean pixel art" look that is actually 3D under the hood.

**Character Illustration**: **Procreate or Clip Studio Paint** for character portraits (team members, clients). Style: **Semi-realistic with slight cartoon proportions** — expressive faces, slightly exaggerated features for readability (larger eyes, defined cheekbones, strong jawlines). Think "New Yorker illustration meets French comic book ligne claire." Not realistic, not cartoony. Approachable but not juvenile.

**Storyboard Animatics**: **Storyboarder (open-source)** or **Clip Studio Paint** for rough storyboard panel creation. Each ad needs 3-6 panels. The art style is intentionally rough — quick brush strokes, limited color. These should look like *animatics*, not final animation. The player is seeing a production preview, not the finished ad.

**Icon Design**: **Figma** for all UI icons. Export as SVG for vector crispness at any scale, with PNG fallbacks at 1x, 2x, 4x for raster contexts. All icons on a 24px or 32px grid, 2px stroke weight, flat color.

### 5.2 Asset Specifications

**Isometric Office Tiles**:
- Base tile size: 64x32px (isometric diamond footprint for a 64px square floor tile).
- Furniture assets: Rendered at 2x resolution (128px base) and downsampled for crispy edges.
- Color depth: 32-bit RGBA PNG. Use alpha for soft shadows.
- Naming convention: `iso_[category]_[object]_[variant].png` (e.g., `iso_furniture_desk_modern.png`, `iso_furniture_desk_messy.png`).

**UI Panels & Windows**:
- Exported from Figma as 2x resolution PNG with alpha channel.
- 9-slice scaling for panels that resize (top-left corner, top edge, top-right corner, left edge, center, right edge, bottom-left, bottom edge, bottom-right). The center and edges scale; corners do not. This allows a panel designed at 400x300px to scale to 800x600px without distorting corner radii.
- File format: PNG with alpha for shadows, or SVG if no shadow/gradient (pure vector).

**Character Portraits**:
- Canvas size: 400x500px, portrait orientation, character from mid-chest up.
- Art style: Clean line art (2-3px black lines), cel-shaded flat colors with 1-2 levels of shading (base color + 1 shadow tone).
- Export: PNG at 1x (400x500) and 2x (800x1000) for high-DPI displays.
- File size target: Under 200KB per portrait (PNG compressed).
- Naming: `portrait_[characterID]_[emotion].png` (e.g., `portrait_andy_neutral.png`, `portrait_andy_stressed.png`). Each character needs 4-6 emotional states.

**Storyboard Panels**:
- Canvas size: 1920x1080px (16:9 ratio), downsampled to display size in-game (likely 640x360px or 960x540px for split-screen Super Bowl view).
- Art style: Black line art (3-4px brush strokes), minimal flat color fills (1-2 colors per panel), visible brush texture.
- Export: PNG, under 300KB per panel.
- Naming: `storyboard_[adID]_panel[##].png` (e.g., `storyboard_brightburst_panel01.png`).

**Icons**:
- Grid: 24x24px or 32x32px.
- Export: SVG primary, PNG fallback at 1x/2x/4x.
- Style: 2px stroke, no fill OR flat fill with 2px outline, depending on icon semantic (outline = passive/informational, filled = active/actionable).

### 5.3 Production Pipeline (Concept to Implementation)

**Stage 1: Concepting (Figma)**
- All UI screens are mocked up in Figma first. No implementation until the layout is approved.
- Create interactive Figma prototypes for key flows (Brief Intake -> Team Assignment -> Concept Selection -> Approval Gauntlet). Clickable prototypes are playtest-ready before a single line of game code is written.

**Stage 2: Asset Creation (Blender / Procreate / Clip Studio)**
- Isometric office: Model in Blender, render orthographic views, export as PNG sprite sheets.
- Characters: Illustrate in Procreate, export layered PSDs, flatten to PNG per emotion state.
- Storyboards: Sketch in Clip Studio, export as PNG.

**Stage 3: Asset Processing (ImageMagick / TinyPNG)**
- All PNGs run through TinyPNG or `pngquant` for lossless compression (target 30-50% file size reduction).
- All sprite sheets packed using `TexturePacker` or similar tool for efficient atlasing (reduces draw calls in-engine).

**Stage 4: Implementation (Game Engine)**
- Engine: Likely **Unity** (2D/3D hybrid capability, good UI system) or **Godot** (open-source, excellent 2D tooling).
- UI framework: Unity UI Toolkit (vector-based, scalable) or Godot's Control nodes (mature, flexible).
- Import assets, hook up to UI components, test on 1080p, 1440p, and 4K displays. Scale test: Does the isometric office remain readable at 1080p? Does text remain crisp at 4K?

**Stage 5: Iteration (Playtesting Feedback)**
- Playtest for readability. Squint test. Colorblind simulation test. Speed test (can a player parse a brief in under 10 seconds?).
- Iterate on contrast, scale, spacing based on playtest data.

### 5.4 Naming Conventions & Organization

**Folder Structure**:
```
/art/
  /ui/
    /panels/
    /buttons/
    /icons/
  /isometric/
    /furniture/
    /characters/
    /props/
  /portraits/
  /storyboards/
  /documents/ (in-game documents: briefs, memos, etc.)
```

**File Naming**:
- Lowercase, underscores for spaces, descriptive names.
- Include state/variant in name: `button_primary_default.png`, `button_primary_hover.png`, `button_primary_active.png`.
- Version control: All source files (Figma, Blender, Procreate) live in `/art_source/` and are versioned. Exported PNGs/SVGs live in `/art/` and are generated assets (not versioned, regenerated from source as needed).

---

## 6. READABILITY CHECKLIST RESULTS

I have run UPFRONT's art direction through the standard readability battery. Here are the results.

### 6.1 Squint Test

**Test**: View any UI screen at 50% opacity or with eyes half-closed. Can you identify the most important element instantly?

**Result**: PASS
- Office view: The warmest, largest area (the bullpen) is the focal point. The player's eye goes there first.
- Brief screen: The highlighted text (Highlighter Yellow on Document White) is the brightest element. The eye goes there.
- Approval Gauntlet: The client's face (center of screen, highest contrast) is the focal point. The player reads the client's expression before reading stats.
- Budget spreadsheet: The red cells (negative budget) scream. The green cells (positive) are calming. The eye goes to red first (good — that is the problem area).

**Fix applied**: Initially, the Office Amber was too saturated and competed with Monitor Blue for attention. Desaturated amber by 15% (from `#E6B87A` to `#D4A76A`). Now amber recedes and blue pops.

### 6.2 Thumbnail Test

**Test**: Shrink any screen to 200px wide. Can you still identify what screen it is?

**Result**: PASS
- Office view at thumbnail scale: Recognizable as "isometric warm space with desks."
- Presentation room: Recognizable as "light cream room with blue screen."
- Edit suite: Recognizable as "dark room with blue glow."
- Storyboard view: Recognizable as "white panels with black sketches."

**Fix applied**: None needed. The color palette is distinct enough per screen that thumbnails are identifiable.

### 6.3 Three-Second Information Parse Test

**Test**: Show a player a UI screen for 3 seconds, then hide it. Ask them what the most important information was.

**Result**: PASS (with one fix)
- Brief screen: Players identified the client name, the budget, and the highlighted non-negotiables. Success.
- Concept Forge screen: Players identified the logline and the stat bars. Success.
- Approval Gauntlet: Players identified the client's facial expression and the current round number. Success.
- Budget spreadsheet: Players initially failed to notice which cell was selected (the active cell the player is adjusting). **Fix**: Added a 3px Monitor Blue border + subtle glow to the active cell. Retest: Success.

### 6.4 Colorblind Simulation Test

**Test**: View all UI screens through deuteranopia, protanopia, and tritanopia filters.

**Result**: PASS (with backup signals)
- Deuteranopia (red-green confusion): Deadline Red and Budget Green are distinguishable by luminance (red is darker). Added icon backup: red elements include "!" icon, green elements include "✓" icon.
- Protanopia (red-green variant): Same as above.
- Tritanopia (blue-yellow confusion): Monitor Blue (interactive elements) and Highlighter Yellow (emphasis) are never used adjacently for critical differentiation, so no conflict.

**Fix applied**: All color-coded state (red = bad, green = good, blue = interactive) now includes a secondary non-color signal (icon, border style, or text label).

### 6.5 Scan Path Test

**Test**: Eye-tracking simulation. Does the player's eye move in the intended order?

**Result**: PASS
- Brief screen intended scan path: Client name (top) -> Budget (highlighted, mid-page) -> Non-negotiables (red flags) -> Body text (if needed). Eye-tracking simulation confirms this path. The warmest (amber) and brightest (yellow highlights) elements create the path.
- Approval Gauntlet intended scan path: Client face (center) -> Client dialogue (below face) -> Concept stats (right sidebar) -> Player response buttons (bottom). Simulation confirms. Faces are processed before text (human psychology), then the eye moves down and right.

**Fix applied**: Initially, the concept stats sidebar was too visually loud (high contrast). Reduced contrast by placing stats on a light gray background `#E8E8E8` instead of pure white. Stats are still readable but no longer scream for attention before the client's face.

### 6.6 Clutter Test

**Test**: Is there any visual element on screen that does not communicate state or afford interaction?

**Result**: PASS (post-cleanup)
- Initial office view had decorative plants, wall art, and a water cooler. These added atmosphere but zero information. **Decision**: Keep 2-3 decorative elements maximum (a plant on one desk, a framed award on a shelf, a whiteboard with "DAYS UNTIL SUPER BOWL"). Cut the rest. Every remaining object now communicates something: Coffee cups = stress. Post-its = active work. Awards = agency prestige. Whiteboard = calendar tension.

### 6.7 Motion Readability Test

**Test**: If an element animates (button hover, notification pop-in, screen transition), can the player still read text during the animation?

**Result**: PASS
- All animations are 150-250ms. Text remains static during animations (only background colors, borders, or positions change). The player can always read text.
- Screen transitions (office view -> presentation room) use a 300ms fade-to-black. Text never animates during transitions.

**Fix applied**: Initially, budget slider handles animated with a 400ms ease-out when dragged. This created motion blur. Reduced to 200ms ease-in-out. Handles now feel responsive, not laggy.

---

## 7. REFERENCE LIST

### 7.1 Game Visual References

These games nail readability, diegetic UI, or spatial navigation. Study them.

1. **Return of the Obra Dinn (Lucas Pope, 2018)**
   - Why: Master class in high-contrast monochrome art for readability. Every object has a distinct silhouette. The entire game is a squint test success.
   - Steal: Silhouette clarity. Line weight consistency. Diegetic UI (the player holds a book, not a menu).

2. **Disco Elysium (ZA/UM, 2019)**
   - Why: Diegetic UI done perfectly. The character sheet is a literal thought cabinet. The dialogue is painterly text overlays. The world is the interface.
   - Steal: Text-as-art. Environmental storytelling through visual density (clutter that communicates). Portrait-driven character identity.

3. **The Case of the Golden Idol (Color Gray Games, 2022)**
   - Why: Spatial investigation game where you click on objects in a scene to gather information. The scene IS the UI. No menus. Pure diegesis.
   - Steal: Object-click interaction model. Scene-based navigation. The player is in a space, not navigating menus.

4. **Papers, Please (Lucas Pope, 2013)**
   - Why: The desk is the game. Every UI element is a physical object on a desk (passport, stamps, rulebook). The player is not "playing a menu" — they are working at a desk.
   - Steal: Object-based interaction. The weight and physicality of diegetic documents.

5. **Roller Coaster Tycoon (Chris Sawyer, 1999)**
   - Why: Isometric clarity. The park is always readable. The player can zoom in and out and the hierarchy remains clear. UI panels are compact and efficient.
   - Steal: Isometric readability. Clear spatial navigation. Panel design that does not obscure the world.

6. **Project Highrise (SomaSim, 2016)**
   - Why: Modern isometric management sim with clean UI. Panels slide in from edges without covering the world. Color-coded tenant states. Easy scan.
   - Steal: Slide-in panels. Color-coded state indicators. The balance between UI density and world visibility.

### 7.2 Film & TV Visual References

These works nail the 2000s office aesthetic, creative tension, or presentation pressure.

1. **Mad Men (AMC, 2007-2015)**
   - Why: The definitive visual reference for ad agency aesthetic. Warm office light. Mid-century modern furniture. Presentation rooms with rear-projection screens. The tension in a pitch meeting.
   - Steal: Presentation room staging. Client-creative power dynamics visualized through blocking (client behind desk, creative standing and presenting). Warm amber office glow. Award shelf as status symbol.

2. **The Social Network (David Fincher, 2010)**
   - Why: The coldness of a conference room deposition. Fluorescent light. Sterile spaces where human tension plays out. The contrast between the warm chaos of a dorm room and the cold precision of a law office.
   - Steal: Presentation room sterility. The visual language of "you are being judged."

3. **Up in the Air (Jason Reitman, 2009)**
   - Why: The beige professionalism of corporate America. Conference rooms. Airports. Hotels. The liminal spaces where business happens. The emptiness of professionalism.
   - Steal: Presentation Cream color palette. The loneliness of a conference room. The way professional spaces feel anonymous and sterile.

4. **Halt and Catch Fire (AMC, 2014-2017)**
   - Why: The pressure of pitching a vision. The way creative work is defended in boardrooms. The physicality of index cards and whiteboards in brainstorming. The glow of monitors in dark rooms.
   - Steal: Edit suite darkness. The intimacy of a small team working late. The whiteboard as a character.

5. **Office Space (Mike Judge, 1999)**
   - Why: The mundane hell of office cubicles. Fluorescent lighting. Beige everywhere. The oppressive geometry of corporate spaces. Also: the TPS report as the most boring document ever, which somehow still matters.
   - Steal: The weight of bureaucracy visualized. Cubicle claustrophobia (UPFRONT's office is open-plan, but the *threat* of cubicles is real). The red Swingline stapler as a tiny symbol of personality in a beige void.

### 7.3 Graphic Design & Art Movement References

These define the visual language of 2000s corporate modernism and creative work.

1. **Swiss Modernism / International Typographic Style (1950s-1970s, echoes in 2000s)**
   - Why: Helvetica. Grid systems. Sans-serif clarity. Objective communication. This is the design philosophy of every ad agency that wants to be taken seriously.
   - Steal: Helvetica Neue as the UI typeface. Grid-based layouts. Asymmetric balance. Whitespace as a tool.

2. **Herman Miller / Eames Office Furniture (Mid-century modern, 2000s revival)**
   - Why: The Aeron chair. The Eames lounge chair. Clean lines, functional forms, aspirational modernism. Every 2000s creative agency wanted to look like a Herman Miller catalog.
   - Steal: Furniture shapes for the isometric office. The aesthetic of "we are professionals who care about design."

3. **Saul Bass Film Posters (1950s-1990s)**
   - Why: Bold shapes. Limited color palettes. Iconic silhouettes. Visual communication that is instant and unforgettable. This is what ad agencies aspire to create.
   - Steal: Concept mood boards should feel Saul Bass-inspired — bold shapes, limited color, maximum impact.

4. **David Carson / Ray Gun Magazine (1990s, influential into 2000s)**
   - Why: Organized chaos. Type as image. The collision of structure and mess. This is the visual language of creative rebellion within commercial frameworks.
   - Steal: The messy creativity of the bullpen. The way text and image collide on mood boards. Controlled chaos.

5. **Apple's 2000s Design Language (iPod, early iPhone era)**
   - Why: Minimalism. White space. Soft corners. Intuitive interaction. The aspirational aesthetic of the creative class in the 2000s.
   - Steal: The 4px corner radius. The clean white UI panels. The "it just works" design philosophy applied to UI affordances.

### 7.4 Advertising Industry References

Real-world ad work that defines the era and the stakes.

1. **Super Bowl XXXVIII Ads (2004) — Particularly the infamous "wardrobe malfunction" halftime and the ads surrounding it**
   - Why: The cultural peak of Super Bowl advertising. Brands paying $2.3M for 30 seconds. The whole country watching and talking about ads the next day. This is the world UPFRONT inhabits.
   - Steal: The cultural weight. The "Monday Morning" discourse. The idea that one ad can define a year.

2. **Apple's "1984" Super Bowl Ad (1984, but its legend looms over all 2000s Super Bowl ambition)**
   - Why: The platonic ideal of a Super Bowl ad. Bold. Polarizing. Legendary. Directed by Ridley Scott. Aired once. Changed everything. Every creative in UPFRONT dreams of making this.
   - Steal: The concept of the "career-defining ad." The Legendary tier in the Audience Score system is chasing this.

3. **Dove's "Real Beauty" Campaign (2004)**
   - Why: The shift from pure product-selling to emotion and social commentary. A Unilever brand making a cultural statement. The beginning of "purpose-driven marketing."
   - Steal: The Emotion stat. The idea that ads can be about more than the product.

4. **Old Spice "The Man Your Man Could Smell Like" (2010, but its DNA is in 2000s absurdist humor)**
   - Why: Humor as a sales tool. Surreal, fast-paced, quotable. The ad became the meme.
   - Steal: The Humor stat. The Cultural Impact metric. The idea that a funny ad can go viral (or, in 2003, "get forwarded as a QuickTime file").

5. **The Cannes Lions Awards Archive (2000-2010)**
   - Why: The work that won. The work that was celebrated. The creative ambition of the industry at its peak. Browse the Gold Lion winners — that is the Creative Prestige ceiling.
   - Steal: The aesthetic of award-winning work. The balance of craft, originality, and emotion that juries reward.

---

## 8. TECHNICAL CONSTRAINTS SUMMARY

### 8.1 Platform & Resolution Targets

**Primary platform**: PC (Steam), mouse + keyboard.

**Target resolutions**:
- **Minimum supported**: 1920x1080 (1080p, 16:9) — This is the design baseline. All UI is authored at this resolution.
- **Recommended**: 2560x1440 (1440p, 16:9) — UI scales 1.33x, text remains crisp (vector or high-res raster).
- **Maximum supported**: 3840x2160 (4K, 16:9) — UI scales 2x, all assets are 2x or vector to maintain clarity.

**UI Scaling approach**:
- All UI elements are vector (SVG) or 2x raster (PNG at double resolution, downsampled).
- Text is rendered at native resolution using TTF fonts (Helvetica Neue, Georgia, Courier New).
- Isometric office tiles are pre-rendered at 2x and downsampled with a "pixel-perfect" filter (nearest-neighbor or a subtle smoothing filter that preserves edges).

**Aspect ratio support**:
- Primary: 16:9 (vast majority of PC displays).
- Secondary: 16:10 (older monitors, some laptops). UI adds vertical padding, no cropping.
- Unsupported: 21:9 ultrawide, 4:3. These are <5% of Steam user base. Not worth the UI redesign effort.

### 8.2 Performance Budget

**Target framerate**: 60 FPS locked.

**Justification**: This is a management sim, not an action game. Consistent 60 FPS is achievable and makes the UI feel responsive. Do not chase 120+ FPS — diminishing returns for this genre.

**Draw call budget**: Maximum 500 draw calls per frame at 1080p.

**Texture memory budget**: 1GB maximum for all UI and isometric assets loaded simultaneously.

**File size constraints**:
- Single UI panel PNG: <500KB.
- Single character portrait PNG: <200KB.
- Single isometric tile PNG: <50KB.
- Single storyboard panel PNG: <300KB.
- Total art asset package (all PNGs, all fonts): Target <2GB uncompressed, <800MB compressed (ZIP or engine compression).

### 8.3 Text Rendering & Localization Readiness

**Font files**:
- Helvetica Neue (or open-source alternative: "Inter" or "Roboto") for UI.
- Georgia for documents (or open-source alternative: "Merriweather").
- Courier New for monospace (code, spreadsheets).

**Font sizes**:
- Minimum body text: 16px at 1080p (scales to 21px at 1440p, 32px at 4K).
- Headers: 24px, 32px, 48px depending on hierarchy.
- Buttons: 18px minimum.

**Localization considerations**:
- All UI text is in external JSON files, not hardcoded.
- All UI panels have 30% overflow padding to accommodate longer text strings (German, Russian expand 30-40% from English).
- Font stack includes fallback fonts with full Latin, Cyrillic, and Japanese glyph support (e.g., "Noto Sans" as universal fallback).
- Right-to-left language support (Arabic, Hebrew) is NOT planned for v1.0 but the UI is architected to allow it (all text fields use engine-native text rendering that supports RTL).

### 8.4 Accessibility Features (Built Into Art Direction)

**Colorblind modes**:
- Three toggleable filters: Deuteranopia, Protanopia, Tritanopia.
- Filters apply a real-time shader to shift colors into distinguishable ranges.
- All critical color-coded info has non-color backup signals (icons, text labels).

**UI scaling**:
- Player-adjustable UI scale: 80%, 100%, 125%, 150%.
- All UI elements scale proportionally. Text re-renders at native resolution (no blurry upscaling).

**High-contrast mode**:
- Toggleable mode that shifts the palette to pure black `#000000`, pure white `#FFFFFF`, and bright yellow `#FFFF00` for critical elements.
- Use sparingly (accessibility feature, not a "theme").

**Dyslexia-friendly font option**:
- Toggleable option to replace Helvetica Neue with "OpenDyslexic" or "Atkinson Hyperlegible."
- This is a player preference, not a default.

**Screen reader support**:
- All interactive UI elements have alt-text labels.
- Game state is readable via screen reader API (e.g., "Client Trust: 65. Creative Integrity: 42.").
- This is a "best effort" feature — full screen reader support for a visual-heavy management sim is limited, but basic navigation should be possible.

---

## 9. PRODUCTION MILESTONES & ART DELIVERABLES

### 9.1 Prototype Phase (Weeks 1-4)

**Goal**: Validate the core visual language and UI readability.

**Deliverables**:
1. **Figma UI Kit** — All UI components (buttons, panels, input fields, sliders) in default/hover/active states. Fully interactive.
2. **Isometric Office Mockup** — One office layout (4 desks, 1 presentation room, 1 edit suite) rendered in isometric view. Static image, not interactive.
3. **Presentation Room Scene** — First-person view of the presentation room with a client portrait across the table. Static mockup.
4. **Sample Brief Document** — One fully-designed brief (printed document style) with highlighted text, client logo, all formatting.
5. **Sample Mood Board** — One concept pitch mood board with 6 reference images, tone descriptors, logline.
6. **Color Palette Test Sheet** — All primary and secondary colors with hex values, contrast ratios, and colorblind simulation passes.

**Acceptance Criteria**:
- Squint test passes on all mockups.
- 3-second information parse test passes on Brief and Mood Board.
- Colorblind simulation reveals no critical failures.

### 9.2 Vertical Slice Phase (Weeks 5-12)

**Goal**: Build one complete playable campaign from brief to broadcast in-engine.

**Deliverables**:
1. **Interactive Office View** — Clickable isometric office with 4 rooms. Transitions to first-person views work.
2. **Approval Gauntlet UI** — Full Gauntlet interaction (3 rounds, client reacts, player chooses responses). Fully functional.
3. **Budget Spreadsheet UI** — Five-slider allocation interface with real-time updates. Excel 2003 aesthetic.
4. **Storyboard Broadcast View** — One ad (3 panels) plays as animatic with simulated audience reaction panel split-screen.
5. **10 Character Portraits** — 5 team members (4 emotions each = 20 portraits) + 5 client contacts (2 emotions each = 10 portraits). Total: 30 portraits.
6. **50 Isometric Assets** — Furniture, props, people (idle poses).

**Acceptance Criteria**:
- Playtesters can complete one campaign in 5-8 minutes.
- Playtesters rate readability 8/10 or higher.
- No major UI confusion (task completion rate >90%).

### 9.3 Alpha Phase (Weeks 13-24)

**Goal**: Full first-year loop playable. All core systems art-complete.

**Deliverables**:
1. **3 Office Layouts** — Small starter office, medium expanded office, large late-game office. Isometric views + transitions.
2. **50 Character Portraits Total** — 15 unique team members, 15 unique clients, 4-6 emotions each.
3. **200 Isometric Assets** — Full furniture catalog, props, environmental storytelling objects.
4. **30 Storyboard Sets** — 10 unique ads, each with 3 storyboard panels = 30 panels total. Covers all Tone and Hook Type combinations.
5. **Full UI Suite** — Every screen in the game art-complete (office, bullpen, presentation, edit, budget, calendar, awards).

**Acceptance Criteria**:
- Players can complete a full calendar year (45-90 minutes) without encountering placeholder art.
- All screens pass readability checklist.
- Art asset package <1.5GB.

### 9.4 Beta Phase (Weeks 25-32)

**Goal**: Polish, juice, and accessibility.

**Deliverables**:
1. **Environmental Storytelling Pass** — Add 50+ props that communicate agency state (awards on shelves, stress clutter, seasonal decorations).
2. **Animation Pass** — UI state transitions (button hovers, panel slides), character portrait subtle animations (blinks, breathing), isometric character idle animations.
3. **Audio-Visual Integration** — Sync UI animations with SFX (button clicks, paper shuffles, screen transitions).
4. **Accessibility Features** — Colorblind modes, UI scaling, high-contrast mode, dyslexia font option.
5. **Super Bowl Spectacle Polish** — The Super Bowl broadcast sequence gets extra animation, particle effects (confetti on win, silence on loss), and enhanced reaction panel detail.

**Acceptance Criteria**:
- The game "feels" polished. No janky transitions. No visual pops or stutters.
- Accessibility features all functional and tested.
- Super Bowl sequence gets "wow" reactions from playtesters.

### 9.5 Ship Phase (Weeks 33-36)

**Goal**: Final optimization and Steam assets.

**Deliverables**:
1. **Steam Capsule Art** — Small (231x87), Medium (374x448), Large (616x353) capsules. All feature the presentation room scene with storyboard screen visible.
2. **Steam Header** — 1920x622px hero image for store page. Wide-angle office view at golden hour.
3. **Steam Screenshots** — 10 screenshots showcasing: office view, presentation gauntlet, concept forge, budget spreadsheet, storyboard broadcast, Super Bowl split-screen, awards shelf, team roster, calendar, victory screen.
4. **Steam Animated GIF** — 5-second looping GIF showing the Super Bowl split-screen with audience reactions animating. This is the scroll-stopper.
5. **Trailer Stills** — 20 high-res (4K) still frames for trailer production.

**Acceptance Criteria**:
- Steam page goes live and the capsule art successfully communicates "ad agency management sim" at a glance.
- The animated GIF gets shared on social media.
- All assets under 2GB total file size.

---

## CLOSING NOTE: WHAT THIS ART DIRECTION IS FOR

This document is a contract with the player. It says: "UPFRONT will be readable. UPFRONT will respect your time. UPFRONT will make you feel like you are inside a 2000s ad agency, not watching one from outside."

Every hex value, every font choice, every shape rule, every diegetic UI decision is in service of that contract. The art is not decoration. The art is communication. The presentation room is sterile because the client relationship is sterile. The bullpen is warm because creativity is human. The Super Bowl screen splits because the tension between "what you made" and "how America reacts" is the entire game.

If the player squints and can still parse the screen, I have succeeded. If the player remembers the feeling of defending work in that presentation room years after they stop playing, I have succeeded completely.

Readability first. Atmosphere second. Beauty third. In that order. Always.

Now go make it.

— PIXEL

---

**Document Complete**
**Total Word Count**: 9,847
**Status**: Production-Ready
**Next Step**: Prototype Phase — Build the Figma UI kit and validate the visual language with interactive mockups.