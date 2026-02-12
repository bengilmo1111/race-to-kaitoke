# Race to Kaitoke — Art Direction

## Vibe
A New Zealand river journey carved from bright bath toys and pounamu, viewed from inside a child's diorama box where the water is alive and everything has googly eyes.

## Emotional Core
This game is about the joy of going home — the stubborn, instinctive pull upstream against everything that pushes you back. The central tension is **smallness vs. determination**: you are a baby creature in a big river, but you are relentless. Every obstacle is a playful "oops!" not a threat — the world is challenging but never hostile. The feeling is: "I'm tiny but I'm DOING it."

## Visual References
- **Claymation stop-motion (Aardman / Laika)** — The slightly-too-shiny, slightly-too-round quality of hand-sculpted toys. Everything looks like it could be picked up and squeezed. Relevant for material feel: plastic-glossy with visible "thumb marks" in the geometry.
- **New Zealand pounamu (greenstone) carvings** — Deep translucent greens with internal glow. The taniwha's color language draws from this: jade-green with warm inner light. Connects to cultural authenticity without being literal.
- **Fisher-Price / Playmobil toy photography** — Oversaturated primary colors against clean backgrounds. Objects are chunky, beveled, and look injection-molded. The river world should feel like a toy playset you'd find at The Warehouse.
- **Hayao Miyazaki's water sequences (Ponyo, Spirited Away)** — Water as a living, joyful character rather than a physics simulation. The river should feel like it has personality: it wobbles, it sparkles, it breathes.
- **Traditional Māori kōwhaiwhai patterns** — The flowing, curvilinear scroll patterns used in wharenui rafters. Not applied literally as textures, but influencing the river's spline curves, the taniwha's body segments, and the rhythm of the world layout.

## Color
### Palette
- **Dominant (60%): Kairangi Jade** — `#2EC4A0` — The river water, the taniwha's body, ambient world tone. A warm teal-green that reads as "alive water" not "hospital scrubs." High saturation, medium-high value.
- **Secondary (25%): Diorama Sand** — `#F5D990` — Riverbanks, terrain, bridges, UI panel backgrounds. A warm golden-sand that grounds the green and feels like sun-warmed clay.
- **Accent (10%): Tītī Orange** — `#FF6B35` — Fish to eat, score pops, dash trail, level-up sparkle, interactive highlights. Hot and attention-grabbing. The "chomp!" color.
- **Accent Alt (5%): Pounamu Glow** — `#7DFFCC` — Emissive accents on the taniwha, growth meter fill, finish-line effects. A luminous mint that feels like light through greenstone.
- **Background: Deep River** — `#1A3A4A` — The riverbed visible through water, the sky gradient base, UI text background. A rich dark teal that makes the brighter colors pop without going to black.
### Rules
- Fish and collectibles ALWAYS use Tītī Orange or Pounamu Glow — never the dominant or secondary colors. Edible things must visually "pop" from the world instantly.
- The taniwha is the ONLY object that uses the full jade-to-pounamu gradient. No other game object shares this color range. The player must always be instantly findable.
- **FORBIDDEN COLOR: Pure grey (#808080 and surrounding neutral greys).** Grey kills the toy-diorama feel. Rocks are warm brown-grey (`#8B7D6B`). Shadows are deep teal. Bridges are warm wood-brown. Nothing is neutral.
- Danger/obstacle objects use a desaturated warm brown (`#7A5C3E`) so they read as "part of the world" not "threat." They are environmental, not menacing.

## Typography
- **Primary: system sans-serif stack (Arial/Helvetica)** — All UI, score, section names. Rendered BOLD, ALL CAPS, with `letter-spacing: 0.1em`. Clean and chunky like toy packaging text. White with a 2px dark teal outline/shadow for readability over 3D.
- **Secondary: same stack, regular weight** — Tutorial prompts, flavor text. Mixed case, slightly smaller. Warm sand color on dark teal background panels.
- **Māori place names: same typeface, BOLD, Tītī Orange color** — Every section title features the te reo Māori name prominently, with English subtitle below in smaller secondary style. Māori names are never italicized — they are primary, not foreign.
- **Text behavior:** Text enters with a quick bounce-scale (0→110%→100%, 200ms, ease-out-back). Score numbers punch-scale on change. Text exits by scaling to 0 with ease-in.

## Shape Language
Everything is **rounded, beveled, and chunky** — like injection-molded plastic toys. Primary shapes are capsules, rounded boxes, and spheres. NO sharp edges on any friendly object. The taniwha is built from overlapping capsule segments. Fish are rounded diamond shapes. Rocks are lumpy spheres. Trees are stacked rounded cones.

Obstacles use slightly more angular shapes (hexagonal logs, faceted nets) to subconsciously read as "different from the friendly world" — but still rounded enough to feel toy-like, never threatening.

Density increases per section: Harbour Mouth is sparse and open. Upper River Sprint is dense and layered. This density progression IS the difficulty curve made visible.

## Lighting & Atmosphere
**Primary light: warm directional sun from upper-right-front** at roughly 45 degrees, color `#FFF5E0` (warm cream). Intensity 1.2. This gives everything a "golden afternoon" feel.

**Ambient light: soft hemisphere** — sky color `#87CEEB` (light sky blue), ground color `#2EC4A0` (jade bounce). Intensity 0.5. Fills shadows with color, never lets anything go dark.

**Shadows: soft, short, warm-tinted.** Shadow opacity 0.3 max. Shadows are tinted slightly toward jade, not grey or black. They exist to ground objects, not for drama.

**Atmospheric effects: gentle fog** starting at 60% of view distance, color blending toward `#C8E6D0` (misty jade-white). Creates depth and hides pop-in. No bloom, no chromatic aberration, no film grain — this is a toy box, not a photograph.

**Water surface: animated vertex displacement** with a subtle sparkle effect (small emissive flickers). Water is semi-transparent near edges, fully opaque at center. Color shifts from jade-green (shallow) to deep-river teal (deep).

## Motion
**Overall feel: bouncy and responsive.** Everything has a slight squash-and-stretch. The taniwha accelerates fast and decelerates with a satisfying drag-through-water feel. Turning has a slight body-flex delay (the tail follows the head).

**Easing: ease-out-back for entries, ease-out for gameplay.** UI elements overshoot slightly on appear. Gameplay movement uses smooth ease-out for deceleration. Dash is instant-acceleration with gradual slowdown.

**Idle behavior: the world breathes.** Water surface undulates. Reeds sway gently (sinusoidal, staggered phase). Fish idle with small figure-8 movements. The taniwha bobs slightly on the surface. Nothing is ever still.

**Transitions between sections: brief 1-second "river bend" camera sweep** with a section title card that bounces in, holds 1.5s, and scales out. No hard cuts. The river is continuous.

## UI Philosophy
**Minimal, playful, diegetic-inspired.** HUD elements float at screen edges like they're painted on the inside of the diorama box.

- **Growth meter: a horizontal bar at top-center** shaped like a fish silhouette that fills with Pounamu Glow as you eat. When full, it does a sparkle-burst and resets for the next level.
- **Score: top-right**, large bold numbers that punch-scale on change.
- **Dash cooldown: small circle near bottom-center** that fills clockwise. No text — purely visual.
- **Section name: appears center-screen** on section entry, then slides to top-left as a small persistent label.
- **Buttons (menus): rounded rectangles** with Diorama Sand fill, dark teal text, 4px border in jade. On hover: scale to 105%, fill shifts to Tītī Orange, text goes white. On press: scale to 95%. Always with bounce easing.

## Anti-Targets
- **NEVER sterile or minimal.** This is not a design portfolio. The world should feel overstuffed with color and life, like a kid decorated it.
- **NEVER dark or moody.** Even the deepest river section is well-lit. No horror lighting. No dramatic shadows. The scariest thing is a silly eel.
- **NEVER realistic water simulation.** The water is a toy-like surface with character, not a physics flex. No caustics, no realistic reflections, no PBR ocean shader.
- **NEVER neutral grey anywhere.** Every surface has color. Even "grey" rocks are warm brown-tan.
- **NEVER thin lines or delicate details.** Everything is chunky, bold, and readable at a glance. If a 6-year-old can't identify it from across the room, it's too subtle.

## Implementation Notes
- **All geometry uses `MeshStandardMaterial`** with `roughness: 0.4–0.6` and `metalness: 0.0–0.1` for the toy-plastic look. The taniwha gets `metalness: 0.15` and subtle `emissive: #1A6B50` for the pounamu glow effect.
- **Instanced meshes for all repeated objects** (fish, reeds, rocks, particles). Use `InstancedMesh` with per-instance color via instance attributes.
- **Water surface: custom vertex shader** applying sin-wave displacement on Y axis, with two overlapping frequencies. Color is the dominant jade with alpha gradient at edges.
- **Particle effects (splashes, sparkles, score pops): small instanced quads** with scale-up-then-fade lifecycle. Use Tītī Orange for chomps, Pounamu Glow for level-ups, white for splashes.
- **Camera: lerp-follow behind and above taniwha** with gentle noise-based sway (amplitude 0.3 units, period 3 seconds). Camera distance increases slightly as taniwha grows.
- **Growth visual: taniwha mesh scales uniformly** with head-to-body ratio shifting (head stays proportionally larger at small sizes for cuteness, normalizes as you grow).
