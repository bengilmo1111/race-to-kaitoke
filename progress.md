Original prompt: Build "Race to Kaitoke" - a 3D Three.js kids game (ages 6-10). Baby taniwha swims upstream from Te Whanganui-a-Tara (Wellington Harbour) to Kaitoke through Te Awa Kairangi (Hutt River). 5 sections with increasing difficulty. Procedural geometry only, no external assets. Toy-plastic diorama aesthetic. Full game with river generation, taniwha character, fish/eating/leveling, obstacles, controls, HUD, start/finish screens.

## Progress

### Task 1: Project Scaffolding
- [x] Create index.html with Three.js
- [x] Set up game loop with advanceTime hook
- [x] Add render_game_to_text

### Task 2: River + World Generation
- [x] River spline path
- [x] Water surface with vertex animation
- [x] Banks/terrain
- [ ] Section landmarks

### Task 3: Taniwha Character
- [x] Procedural body from capsule segments
- [x] Head with eyes, horns
- [x] Tail fin
- [x] Swim animation
- [x] Growth scaling

### Task 4: Controls + Physics
- [x] WASD/arrow input
- [x] Dash + brace
- [x] Semi-implicit Euler physics
- [x] Camera follow
- [x] Blockage crawl mode

### Task 5: Fish + Obstacles
- [x] Instanced fish
- [x] Eating/chomp mechanics
- [x] Growth meter + leveling
- [x] Obstacle types (logs, rocks, nets, eels, bridges)
- [x] AABB collision

### Task 6: HUD + Menus
- [x] Start screen
- [ ] Tutorial overlay
- [x] HUD (score, growth, dash cooldown, section name)
- [x] Finish screen with confetti
- [x] Replay buttons

### Task 7: Testing + Polish
- [x] Playwright tests (manual via web_game_playwright_client)
- [x] All controls verified (swim, steer, dash, brace)
- [ ] All 5 sections work (tested through section 3)
- [ ] Performance check

### 3D Design Pass (completed)
- [x] Fix: HUD distance display now updates every frame (was only on fish-eat)
- [x] Rocks/obstacles partially submerged in water for natural look
- [x] Riverbanks: organic sloped terrain with vertex displacement (replaced flat boxes)
- [x] Rolling green hills behind riverbanks for depth
- [x] Water sparkle/shimmer particles (white emissive flickers on surface)
- [x] Sky gradient dome (warm cream horizon -> light blue zenith, jade-green below)
- [x] Distant procedural mountains (16 cones with vertex distortion, follow player)
- [x] Puffy clouds (grouped spheres, slowly drifting)
- [x] River foam edges (animated white strips at water/bank boundary)
- [x] Swim wake trail (expanding white circles behind taniwha when moving)
- [x] Improved reeds with leaf tips and sinusoidal sway animation
- [x] Taniwha bob animation (gentle vertical sine bob on water surface)
- [x] Taniwha roll animation (slight body roll during swim)

## TODOs / Suggestions for Next Agent
- [ ] Section landmarks: each section should have unique visual markers (e.g., harbour buoys for section 1, rapids whitecaps for section 3, blockage debris for section 4)
- [ ] Tutorial overlay: brief animated hint on first play ("Press W to swim!")
- [ ] Fish are a bit hard to eat — consider slightly larger hitbox or homing behavior when very close
- [ ] Cloud visibility could be improved — they're subtle in the current fog distance
- [ ] Water could have depth-based color variation (darker center, lighter edges)
- [ ] The eel model animation could be more dramatic — currently subtle side-to-side
- [ ] Consider adding ambient sound (water rush, splash SFX)
- [ ] Performance: test with more obstacles at higher sections; consider InstancedMesh for rocks/fish
- [ ] Test sections 4 (blockage) and 5 (final sprint) more thoroughly
- [ ] Add a "chomp" animation on the taniwha head when eating fish (jaw open/close)

### Task 6 / World Update (this session)
- [x] Tutorial overlay: added first-play animated hint near HUD (`W` / arrow up), auto-hides after ~6.5s and does not repeat after replay.
- [x] Section landmarks implemented with procedural geometry and section-specific themes:
- [x] Section 1: twin harbour buoys
- [x] Section 2: cross-river marker posts + rope
- [x] Section 3: rapid whitecaps cluster
- [x] Section 4: blockage debris marker cluster
- [x] Section 5: sprint entry flags
- [x] Landmarks reset correctly on restart and are included in `render_game_to_text` (`landmarksSpawned`, `tutorialVisible`).
- [x] Testing: Ran develop-web-game Playwright loop after changes (skill client copy in `tests/web_game_playwright_client.mjs`) and confirmed no console/page errors artifacts generated.
- [x] Tutorial overlay verification: DOM-level Playwright check confirms overlay class is shown immediately on first game start.
- [x] Section coverage: added deterministic debug hooks for testing (`window.debug_warp_to_distance`, `window.debug_spawn_all_landmarks`) and captured section checkpoints S1-S5 with states under `output/web-game/landmarks-warp-check/`.
- [x] Remaining checklist item "All 5 sections work" validated via warp-check states (`currentSection` 0..4 observed, section 3 blockage mode transitions observed).

### Notes
- Some far-distance warp screenshots show aggressive shadow/fog artifacts in this build; gameplay state and section transitions still validated via JSON state + visual checkpoint context.

## Updated TODOs / Suggestions
- [ ] Performance check with sustained real-time play through full run (non-warp).
- [ ] Investigate far-distance visual artifact seen in warp-based screenshots (large dark disk around center).
- [ ] Decide whether to keep or remove debug test hooks (`window.debug_*`) for production.
- [x] Mobile touch controls remediation (this session):
- [x] Fixed long-press text selection/callout on touch buttons (CSS `user-select`/`-webkit-touch-callout` + JS `contextmenu`/`selectstart`/`dragstart` prevention).
- [x] Fixed off-screen touch control issue by replacing wide bottom bar with left/right anchored thumb pods and responsive sizing for narrow screens.
- [x] Improved mobile UX layout: steer controls grouped on left thumb, swim/dash/brace grouped on right thumb, pause moved above right action cluster.
- [x] Verification: ran Playwright client and dedicated iPhone 12 emulation screenshot check; all touch buttons are in viewport (`output/web-game/mobile-controls-layout-check/button-rects.json` all `inViewport: true`).
- [x] Game-feel polish pass 1 implemented:
- [x] Added impact systems: hit-stop, camera shake, hit flash, reward pop text.
- [x] Added squash/stretch on taniwha for dash/eat/hit moments.
- [x] Added simple procedural audio cues (dash, fish eat, obstacle hit, level up, finish).
- [x] Improved control responsiveness: stronger swim/steer force and slightly reduced drag.
- [x] Improved camera behavior: FOV speed kick + lateral clamp to reduce bank-clipping camera angles.
- [x] Added debug testing helpers (`debug_set_player_pos`, fish/obstacle references) for deterministic feel tests.

### Polish Testing
- [x] Baseline quick play capture before major changes: `output/web-game/feel-baseline-tiny/`
- [x] Post-polish play pass: `output/web-game/feel-polish-pass1/` (no runtime errors observed)
- [x] Deterministic event tests for fish-eat and obstacle-hit moments: `output/web-game/feel-polish-events/`
- [x] Manual-style scripted control pass: `output/web-game/feel-polish-manual/` (errors.json is empty)

### Observations
- Reward feedback now appears clearly (`+10` pop), and dash/turn feel snappier.
- Camera no longer clips into bank as aggressively during sharp lateral movement.
- Tutorial + section popup can visually overlap action moments near spawn; acceptable but could be staged in future polish.

### 3D Priority Pass (physics -> models -> textures/lighting) - this session
- [x] Physics: improved fish collection feel for kids with subtle near-player fish assist + larger eat radius.
- [x] Physics: added obstacle-hit cooldown to reduce repeated collision jitter/spam feedback.
- [x] Models/animation: added taniwha chomp animation trigger on fish eat (jaw open/close pulse).
- [x] Models/animation: improved eel silhouette (dorsal fin + whiskers) and made eel movement more dramatic (surge + body undulation + roll).
- [x] Textures/lighting: added water depth-based color variation (lighter edges, deeper center) via vertex colors.
- [x] Lighting/background: boosted cloud readability and added soft fill directional light for clearer scene depth.

### Testing (playtest after each feature)
- [x] Baseline 3D pass: `output/web-game/3d-baseline-pass/`
- [x] Physics verification pass: `output/web-game/3d-physics-pass1/` (`fishEaten: 3` in short run)
- [x] Model/animation pass: `output/web-game/3d-model-pass1/` (`fishEaten: 4` in short run)
- [x] Texture/lighting pass: `output/web-game/3d-visual-pass1/` (`fishEaten: 1`, stable controls)

### Notes
- `PLAYER_SPEED_MULT` remains `2.0` as requested.
- Current open visual issue: occasional bright white blob artifact appears in some captures; likely from particle/lighting interaction and should be investigated in next pass.
- [x] Feature: Added stumpy little arms + legs to taniwha with tiny claw details (procedural meshes).
- [x] Added subtle paddle animation for limbs tied to swim phase/input so they feel alive but readable.
- [x] Verified in gameplay pass: `output/web-game/taniwha-limbs-pass/`.
- [x] River path update: made spline much more sinuous/serpentine (stronger meanders + higher-frequency sub-curves, smooth catmull tension).
- [x] Verified with gameplay pass: `output/web-game/serpentine-pass/`.

### Content Variety Pass (this session)
Baseline observations from playtest:
- Repeated obstacle rhythm (frequent rock/log/bridge silhouettes) with limited new hazard behaviors in short runs.
- Pacing and outcomes often felt similar (threading static obstacles + occasional fish pickups).
- Existing bright white visual blob artifact is still present in some views.

Implemented additions (reusing existing systems):
- [x] New hazard: `whirlpool`
  - Procedural rotating ring model.
  - Fair pull-zone behavior (gentle inward pull + slight spin) when nearby.
  - Added to section obstacle pools from section 2 onward.
- [x] New hazard: `reedSnag`
  - Bank-rooted reed cluster that sweeps laterally into channel.
  - Uses obstacle movement/collision system with readable oscillation.
  - Added to section pools from section 2 onward.
- [x] New pacing system: river event chunks
  - Periodic fish-school burst with flanking hazards for risk/reward moments.
  - Reuses `spawnFish`/`spawnObstacle` and resets on restart.

Testing after each addition:
- [x] Baseline: `output/web-game/variety-baseline/`
- [x] Whirlpool targeted pass: `output/web-game/variety-whirlpool-pass/`
- [x] Reed sweeper targeted pass: `output/web-game/variety-reed-pass/`
- [x] Integrated short-run pass: `output/web-game/variety-final-pass/`

Validation notes:
- Variety pass increased active content in comparable runtime (`fishActive`/`obstaclesActive` rose in final run).
- New hazards behaved fairly (player can recover/steer out; no unavoidable trap observed).
- No runtime errors encountered during these scripted playtests.
- Open bug remains: intermittent bright white blob artifact in scene; should be prioritized next.

### Gameplay Elements Pass (this session)
Baseline playtest findings vs modern indie web-game pacing:
- Core loop was still mostly fish pickup + hazard avoidance without many positive state shifts.
- Existing visual bug still reproducible: intermittent bright white blob on water-plane area.

Implemented this pass:
- [x] Bug fix: removed stray trailing JS line after closing `</html>` that could break parsing in strict contexts.
- [x] New gameplay element: **Pounamu Pearl power-up**
  - Rare collectible orb.
  - Grants temporary shield (`shieldTimer`), resets dash cooldown, and gives +30 score.
  - Added HUD status line for active timers.
- [x] New gameplay element: **Current Gate boost rings**
  - Gate obstacle type that grants temporary speed boost (`speedBoostTimer`) and +20 score when passed through.
  - Integrates with obstacle spawn pools from section 2+.
- [x] Visual bug mitigation attempt: reduced sparkle opacity/scale intensity in `updateSparkles()`.

Testing after each feature:
- [x] Baseline pass: `output/web-game/gp-baseline/`
- [x] Power-up targeted pass: `output/web-game/gp-powerup-pass2/`
  - Confirmed `powerupsActive: 0`, `shieldTimer: 5.5`, score increased (+30).
- [x] Current gate targeted pass: `output/web-game/gp-gate-pass/`
  - Confirmed `speedBoostTimer: 2.3`, score increased (+20).
- [x] Integrated gameplay pass: `output/web-game/gp-final-pass/`
  - No script/runtime failures observed in this pass.

Notes:
- New elements preserve art-direction color/shape language (rounded toy forms, jade/glow accents, non-hostile feel).
- White blob artifact is still present in screenshots after sparkle reduction; likely requires deeper material/lighting investigation next.

### Look & Feel Pass (this session)
Baseline findings from playtest:
- Water still showed an intermittent bright white blob/glare artifact that hurt readability.
- Section transitions worked functionally, but camera movement lacked the intended "river bend sweep" feel.
- Score changes were readable but lacked punch/celebration motion.

Implemented this pass:
- [x] Added score punch animation on positive score changes (`#score-display` scale pulse) to match art-direction text behavior.
- [x] Added 1s section-entry camera sweep (`fx.sectionSweep`) layered on follow camera for bend-like motion during section popups.
- [x] Reworked sparkle placement to chunked river-distance recycling to reduce clustering artifacts.
- [x] Reworked pearl power-up visual to faceted toy-gem + ring (reduced transparent white glow accumulation).
- [x] Reduced foam overdraw/brightness and tuned water material roughness/metalness to remove specular white glare blob.

Testing (playtest after each feature):
- [x] Sparkle/powerup artifact checks:
  - `output/web-game/lookfeel-pass2-blobfix-file/`
  - `output/web-game/lookfeel-pass5-foamfix/`
  - `output/web-game/lookfeel-pass7-water-spec/`
- [x] Section transition sweep verification:
  - `output/web-game/lookfeel-pass3-sectionsweep-sliced/`
  - Transition confirmed in state (`currentSection: 1` by `state-2.json`).
- [x] Score punch verification:
  - `output/web-game/lookfeel-pass6-scorepunch/`
  - Positive score deltas occurred with no runtime/page errors.

Notes:
- The bright white blob artifact visible in earlier runs is no longer present in latest passes after foam/water material tuning.
- Added temporary action files for deterministic look-and-feel checks:
  - `tests/actions-lookfeel-pass2.json`
  - `tests/actions-lookfeel-pass3.json`
  - `tests/actions-lookfeel-pass3-long.json`
  - `tests/actions-lookfeel-pass3-sliced.json`
  - `tests/actions-lookfeel-pass4.json`

### 3D Priority Pass 2 (physics -> models -> textures/lighting) - this session
Baseline findings from playtest (`output/web-game/3d-priority-baseline/`):
- Movement could still feel sticky around dense obstacle/bridge edges, especially while holding upstream input.
- World art readability was improving but still had repeated static prop silhouettes.
- Rocks were shape-varied but material variation was subtle at a glance.

Implemented this pass:
- [x] Physics: added near-bank flow assist and anti-stuck recovery:
  - Inward + slight upstream nudge when player rides high-lateral bank edge.
  - Collision tangential slide impulse to reduce hard-stop sticking on obstacle faces.
  - Short anti-stuck booster when sustained obstacle contact + low forward speed while swimming upstream.
- [x] Models/animation: added procedural river duck critter props (toy style) with animated bob + wing flap to increase environmental life.
- [x] Textures/materials: added per-vertex warm rock color variation and adjusted rock roughness for richer toy-plastic stone readability without neutral greys.

Testing after each feature:
- [x] Physics pass: `output/web-game/3d-priority-physics-pass/`
- [x] Model pass (ducks visible/animated): `output/web-game/3d-priority-model-pass/`
- [x] Visual/material pass: `output/web-game/3d-priority-visual-pass2/`
- [x] Extra collision stress pass: `output/web-game/3d-priority-physics-stress/`
- [x] No runtime `errors-0.json` generated in these runs.

Notes:
- Duck props were visible in gameplay captures and stayed consistent with the toy-diorama art direction.
- Anti-stuck behavior improved recovery from contact chains and edge riding in short scripted runs.
- Remaining candidate for future tuning: bridge-underpass collision shaping (camera + obstacle spacing) to further reduce awkward moments when approaching bridge posts at shallow angles.

### Game Feel Polish Pass 2 (this session)
Baseline playtest findings (`output/web-game/feel-pass2-baseline/`):
- Gameplay feedback was decent but still had flatter moments in quick fish chains and dash readiness readability.
- A readability bug remained around bridges/near bank geometry where large foreground occlusion could hide player action.

Implemented this pass:
- [x] HUD/dash juice:
  - Added dash ring readiness pulse (`#dash-cooldown.ready`) and active burst state (`#dash-cooldown.active`).
  - Keeps cooldown readability strong without adding text clutter.
- [x] Action feedback tuning:
  - Dash now includes tiny hit-stop + slightly stronger shake for tactile launch.
  - Fish-eat now spawns richer orange+glow particles, adds micro hit-stop, and introduces occasional combo reward callout (`YUM xN`) every 5 fish.
  - Slight random pitch variance on fish-eat tone to avoid repetitive audio feel.
- [x] Camera readability:
  - Added subtle velocity-based look-ahead in `camera.lookAt(...)` so steering intent reads earlier.
- [x] Bug fix (priority):
  - Improved near-bank occlusion by narrowing/moving near bank mesh outward in `createBankSegment(...)`.
  - Added bridge fade system when near player/camera to prevent hard under-bridge view blocking.
  - Fixed transparency artifact from bridge fading by setting `depthWrite: false` on fadeable bridge deck/rails.

Testing after each feature:
- [x] Baseline: `output/web-game/feel-pass2-baseline/`
- [x] Occlusion pass: `output/web-game/feel-pass2-occlusion/` then bug-fix validation `output/web-game/feel-pass2d-occlusion-fix/`
- [x] Dash/fish feedback pass: `output/web-game/feel-pass2-dash-fish/` and `output/web-game/feel-pass2c-dash-fish/`
- [x] Camera readability pass: `output/web-game/feel-pass2-camera/` and `output/web-game/feel-pass2c-camera/`

Notes:
- Some intermediate parallel runs produced AudioContext console warnings in headless mode and stayed on menu; sequential reruns (`feel-pass2c-*`) validated gameplay behavior correctly.
- Final bridge/occlusion fix run (`feel-pass2d-occlusion-fix`) shows clear forward readability with no bridge stripe artifacts.

### Visual Color Rebalance Pass (this session)
Baseline finding: Entire scene was monochrome green/teal — mountains, water, banks, sky all same hue. Taniwha blended into water. Art direction 25% Diorama Sand was barely present.

Implemented:
- [x] Mountains: warm blue-grey (`0x6B7E8B`, `0x5D7080`, `0x7A8D9A`, `0x526878`) replacing green-teal. Clear depth separation.
- [x] Water: brighter shallow edges (`0x65E0C2`), higher base lerp (25% min brightness), brighter base material color and emissive.
- [x] Sandy shore strip: widened from 2.0 to 3.0 units with repositioned offset for visible golden sand at water edges.
- [x] Far hill grass: warmer yellow-green (`0x6B9B44`) to contrast with blue-grey mountains.
- [x] Near-bank grass transition: warmer (`0x8BA94E`) to carry sand color further.
- [x] Sky dome below-horizon ground: warmer olive-green instead of dark jade.
- [x] Bank decorations: wildflower clusters (orange/glow/yellow accent blooms) spawning 45% chance per chunk.
- [x] Bank decorations: pebble scatter (warm-colored small stones) spawning 35% chance per chunk.
- [x] Taniwha glow: boosted emissive from dark green `0x1A6B50` to bright pounamu `0x3DEBB5` at intensity 0.3 (was 0.2). Tail fin matched.

Testing:
- [x] Color rebalance pass 1: `output/web-game/color-rebalance-pass1/`
- [x] Color rebalance pass 2 (water/shore refinement): `output/web-game/color-rebalance-pass2/`
- [x] Bank decorations pass: `output/web-game/bank-decorations-pass1/`
- [x] Taniwha glow pass: `output/web-game/taniwha-glow-pass1/`
- [x] Long-run validation (sections 0-3, 5 iterations): `output/web-game/visual-pass-longrun/`
- No runtime errors in any pass. 82 obstacles active in section 3 with no performance issues.

Results:
- Scene now has clear color zones: blue-grey mountains (depth), warm-green hills (mid), golden shores (warm accent), jade water (river), orange fish/flowers (pop accents).
- Taniwha glows visibly against water surface with pounamu-tinted emissive.
- Banks feel more alive with scattered wildflowers and pebbles.

### Content Variety Pass 2 (this session)
Implemented:
- [x] Fish color variants: Silver (+15 pts, 20% in S1+), Golden (+25 pts, 8% in S2+) with per-variant colors, particles, pop text, sounds
- [x] Golden Run event chunk: 4 golden fish in tight corridor with flanking obstacles, 25% of events in S2+
- [x] Section-specific decoration density: sparse harbour → dense rapids → moderate sprint
- [x] Section water color tints: per-section deep/shallow vertex color pairs
- [x] Jumping fish (salmon leap) obstacle: parabolic arc across river on 2s cycle, sections 2-4

### Look & Feel Pass 2 (this session)
Baseline playtest findings:
- Blockage (S3) land strip was a flat green box — jarring vs organic terrain
- Scene lighting was flat/cool, missing art direction "golden afternoon"
- Fish too small and hard to see at play distance
- Water section colors too similar
- Start screen plain, no visual life
- Finish screen: section popup + tutorial bled through (z-index bug)

Implemented:
- [x] Blockage terrain: replaced flat box with organic displaced PlaneGeometry, vertex-colored mud-to-grass, scattered rocks
- [x] Lighting warmth: boosted toneMappingExposure (1.1→1.35), sun intensity (1.2→1.45), warmed ambient/hemisphere colors
- [x] Pushed fog back (60-120 → 75-140) for more mid-distance visibility
- [x] Strengthened section water tints: per-section deep+shallow color pairs instead of blended single tint
- [x] Fish visibility: scale pulse per-frame, golden fish larger (1.3x) with glow halo, boosted emissive on all variants
- [x] Start screen: added animated CSS wave shapes (pounamu glow + sand gold) at bottom
- [x] Bug fix: finish screen now hides section popup + tutorial overlay to prevent bleed-through

Testing:
- [x] All 5 sections screenshotted and verified with Playwright
- [x] No runtime errors across all tests
- [x] Fish variant spawning confirmed (orange-only in S0, silver in S1, golden in S2+)
- [x] Water color differentiation visible across sections

### Speed Run Timer + Leaderboard (this session)
Implemented:
- [x] Live speed run timer in HUD: mm:ss.s format, updates every frame, pause-aware (deducts paused duration)
- [x] Timer hidden in chill mode (no competitive pressure)
- [x] localStorage leaderboard: stores top 3 fastest completion times
- [x] Finish screen: if time qualifies for top 3, shows "NEW TOP TIME!" with 3-character initials input
- [x] Initials input: styled text field, auto-uppercase, Enter key support, SAVE button
- [x] Leaderboard display on finish screen: medal emojis, orange initials, white times, sorted by fastest
- [x] Leaderboard display on start screen: shown below PLAY button when entries exist, hidden when empty
- [x] Chill mode runs excluded from leaderboard

Testing:
- [x] Full end-to-end test: 3 runs with initials entry, all saved to localStorage
- [x] Start screen leaderboard renders correctly on page load with seeded data
- [x] No runtime errors across all tests

## Updated TODOs / Suggestions
- [ ] Performance check with sustained real-time play through full run (non-warp).
- [ ] Decide whether to keep or remove debug test hooks (`window.debug_*`) for production.
- [ ] Bridge-underpass collision shaping (camera + obstacle spacing) for shallow-angle approaches.
- [ ] Consider section-specific bank color variation (e.g., darker banks in rapids, sandier in harbour).
- [ ] Consider adding subtle water reflection/mirror effect for extra toy-diorama depth.

### Mobile Playability Pass (this session)
Implemented:
- [x] Added touch-first on-screen controls for gameplay:
- [x] Hold buttons: `SWIM`, `LEFT`, `RIGHT`, `BRACE`
- [x] Tap button: `DASH`
- [x] Touch pause button (`II`) mapped to existing pause flow
- [x] Touch controls auto-show during gameplay on touch devices and narrow screens (`<= 900px`), auto-hide on finish/pause states.
- [x] Added mobile-safe input/CSS behavior:
- [x] `touch-action: none` on canvas/control layer to prevent scrolling/gesture conflicts while playing
- [x] `overscroll-behavior: none` on body
- [x] Reduced render pixel ratio on touch/narrow devices (`1.5`) for smoother mobile performance
- [x] Added responsive HUD and menu sizing/positions for small screens (score, growth bar, timer, section labels, tutorial, dash indicator, popup)

Testing:
- [x] Automated run succeeded after changes: `output/web-game/mobile-pass2/state-0.json`, `output/web-game/mobile-pass2/shot-0.png`
- [x] Manual viewport verification at phone size (390x844): touch controls visible and styled in screenshot `output/web-game/mobile-pass2/phone-ui.png`

Notes:
- Desktop keyboard controls remain unchanged.
- Existing console warning during manual browser inspection was only missing `favicon.ico` (404), unrelated to game logic.

### Continuation Note (2026-02-12)
- Reviewed current uncommitted `index.html` changes (touch control layout + physics anti-stuck tuning).
- Attempted Playwright validation via `tests/web_game_playwright_client.mjs`, but browser launch/network context was unstable in this session:
  - non-escalated run: Chromium launch EPERM
  - escalated run: local server isolation (ERR_CONNECTION_REFUSED)
  - combined escalated server+runner: command hung/timed out
- No additional gameplay code changes were made in this continuation pass.
- Next step: rerun the normal Playwright loop in a stable context and confirm touch controls + collision feel.

### Playtest + Targeted 3D Improvement Pass (2026-02-12)
Goal: playtest first, then improve in priority order (physics -> models -> textures -> lighting/background), respecting `art_direction.md`.

Playtest findings:
- Repro'd collision feel issue: repeated frame-by-frame contact with same obstacle could feel sticky.
- Repro'd visual regression during iteration: large black circular background artifact when rapidly warping sections during automated tests.

Implemented:
- [x] Physics: added per-obstacle contact cooldown (`contactCooldown`) to smooth repeat contacts and reduce sticky obstacle grinding.
- [x] Models + textures: introduced procedural wood textures (canvas-generated bark + end grain) and applied them to toy logs/drift logs/current-gate posts.
- [x] Models: replaced plain log cylinders with richer `createToyLog()` composition (body + end caps + knots), also used in blockage debris logs.
- [x] Lighting: added subtle warm rim directional light for better object separation while keeping the golden-afternoon palette.
- [x] Background stability fix: removed unstable sky-accent experiment and replaced shader-dome dependency with a stable solid sky background to avoid black background artifact in playtest runs.

Testing:
- [x] Added deterministic scenario test harness: `tests/feature-playtest.mjs` (physics/models/lighting scenarios).
- [x] Re-ran scenarios multiple times after each fix via Playwright + local server.
- [x] No JS/page console errors in final scenario runs (`errors.json` all `[]`).
- [x] Verified updated artifacts:
  - `output/web-game/feature-pass/physics/shot.png`
  - `output/web-game/feature-pass/models/shot.png`
  - `output/web-game/feature-pass/lighting/shot.png`

Notes:
- Some automated warp-based screenshots can still show aggressive far-field culling seams/void edges due to camera/test positioning at extreme transitions; this appears tied to world streaming visibility rather than runtime JS errors.

Next suggestions:
- [x] Add a small skybox/horizon skirt mesh to hide far-field world-stream seams during extreme camera/warp states. (Done: full sky gradient dome added)
- [ ] Add a dedicated close-up obstacle/material test scenario that positions camera near logs to validate texture readability in CI artifacts.
- [ ] Tune world chunk preload radius slightly for debug warp flows (optional; may trade memory/perf).

### Harbour Mouth Bank Artifact Fix (2026-02-13)
- Confirmed issue: start-zone bank seam/pop-in at Harbour Mouth that visually settles after initial movement/time.
- Root cause: `lastSpawnedDist` initialized/reset to `0`, so first `spawnWorldInRange()` pass starts at `6` (step=6), skipping distance `0` bank segment creation on frame 1.
- Fix: initialize/reset `lastSpawnedDist` to `-6` so first pass always includes `dist=0` banks.
- Verification: Playwright run with immediate/short-interval captures (`output/web-game/harbour-bank-fix/shot-0.png`, `shot-1.png`) shows stable Harbour Mouth bank geometry from early frames.

### Harbour Mouth Visual Bug Retry (2026-02-13, follow-up)
- Reproduced startup Harbour artifacts in timed Playwright gameplay captures.
- Root cause for remaining startup artifacts: downstream chunk generation at start (`needMax` allowed positive z), creating invalid folded terrain/bank geometry that looked like temporary Harbour bank glitches.
- Fixes applied:
  - Clamp terrain/water/foam/riverbed chunk generation upper bound at river start (`needMax = Math.min(0, playerZ + RIVER_VISIBLE_BEHIND)`).
  - Keep section-0 bank strips disabled in `spawnWorldInRange` and rely on stable ground chunks in Harbour Mouth.
  - Preserve DoubleSide on bank/ground materials to avoid backface culling holes.
- Verification:
  - Fresh gameplay captures in `output/web-game/harbour-final2/shot-0.png` and `output/web-game/harbour-final2/shot-4.png` show stable Harbour banks with no startup folding/triangle artifacts.

### Visual Atmosphere Pass (2026-02-13)
Baseline playtest findings:
- Sky was a flat solid color (0x9FD7EC) — sky dome had been removed due to past artifact issues. This was the biggest atmosphere gap vs art direction's "warm cream horizon → light blue zenith."
- Mountains used MeshBasicMaterial — no lighting response, looked flat and disconnected from the lit scene.
- No ambient environmental life beyond ducks — art direction says "nothing is ever still" and "the world breathes."
- Water surface lacked surface detail props at play distance.

Implemented:
- [x] Sky dome: vertex-colored SphereGeometry (radius 160, BackSide) with warm cream (#FFF0D4) horizon → light blue (#7EC8E8) zenith, warm olive-green (#8BAF5E) below horizon. Follows camera position for stability. No black artifacts across all 5 section warps.
- [x] Mountains: upgraded from MeshBasicMaterial to MeshStandardMaterial with vertex colors. Added snow-capped peaks (white blend above 82% height), darker bases, per-vertex noise variation. Responds to scene lighting now.
- [x] Floating river debris: 30 recycled leaf/twig meshes drifting on water surface. Warm sand/brown leaf colors (#C4A85A, #D4A030, etc). Gentle spin + bob animation. Drift downstream slowly. Chunk-based recycling like sparkles.
- [x] Ambient butterflies: 14 butterfly meshes near bank vegetation. Accent colors (orange, glow, yellow, pink). Triangular wing geometry with flap animation. Circular flutter paths at bank lateral offsets. Recycled when out of range.
- [x] Fog color warmed: adjusted from 0xC8E6D0 → 0xD8E8D0 for better blend with sky dome horizon.

Testing:
- [x] Per-feature screenshots: `screenshots/sky-test/`, `screenshots/mountain-test/`, `screenshots/debris-test/`, `screenshots/butterfly-test/`
- [x] Full 5-section playtest: `screenshots/final-playtest/` — S0 through S5 all verified.
- [x] Zero console errors across all tests.
- [x] Player ate fish, scored points, leveled up during gameplay sections — core gameplay unaffected.

Results:
- Scene now has a proper atmospheric gradient sky instead of flat color.
- Mountains have visible snow caps and respond to scene lighting (sun highlights, shadows).
- Water feels more alive with floating debris props.
- Banks feel more alive with fluttering butterflies near vegetation.
- Fog blends smoothly with the warm sky horizon.

### Content Variety Pass 3 (2026-02-13)
Baseline playtest findings:
- Section 0 only had 2 obstacle types (rock, log) — felt repetitive.
- Only 1 powerup type (Pounamu Pearl) — all collection moments felt the same.
- Only 1 ambient critter (duck) + butterflies — limited sky/overhead life.
- 4 event chunk types existed but no gate-focused reward sequence.

Implemented:
- [x] New obstacle: **kelp bed** — floating seaweed patch that slows player without damage. Gentle friction variety. Added to S0-S1 obstacle pools. Animated frond sway. Warm green-brown toy colors.
- [x] New powerup: **starfish magnet** — 40% of powerup spawns are now starfish (orange accent). Temporarily boosts fish attraction range (8 units, 4.5x strength) for 6s. +20 score. HUD shows "Magnet Ns" timer.
- [x] Ambient birds: **seagulls + skua** — 8 birds circle overhead with wing flap/glide animation. White seagulls in S0-S1 harbour, darker skua mix in S2+. Section-appropriate NZ species.
- [x] New event: **treasure corridor** — 3-4 centered current gates with fish between, ending with a powerup reward. S1+ event pool (~14% chance). Rewards threading a straight line.
- [x] Event pool rebalanced: golden run 18%, treasure corridor 14%, weave 20%, pinch 24%, river event 24%.

Testing:
- [x] Per-feature tests: `screenshots/kelp-test/`, `screenshots/starfish-test/`, `screenshots/bird-test/`, `screenshots/corridor-test/`
- [x] Comprehensive final playtest: `screenshots/variety-final/` — S0 through S5 verified.
- [x] Zero console errors across all tests.
- [x] Core gameplay unaffected (fish eating, scoring, leveling, obstacle progression all work).

Results:
- S0 harbour now has 3 obstacle types (rock, log, kelp) instead of 2.
- Powerup collection moments are now varied (shield pearl vs magnet starfish).
- Overhead bird life adds atmosphere appropriate to NZ river setting.
- Treasure corridor events add a focused reward sequence that rewards skilled play.

### Hutt River Visual Alignment Pass (2026-02-13)
Goal: Align each game section with the real-world Hutt River description from art_direction.md.

Implemented:
- [x] **Per-section bank terrain palettes** (`BANK_PALETTES` array):
  - S0 Harbour: pale shingle/gravel shores, open dry grassland hills
  - S1 Lower River: warm sand shores, lush green grass/terraces
  - S2 Rapids: rocky gravel shores, steep scrubby valley walls (slopeScale 1.6)
  - S3 Near Kaitoke: dark earthy shores, leaf litter, deep native forest
  - S4 Kaitoke Sprint: mossy cool stone, deep mountain bush (slopeScale 2.0)
- [x] **Per-section bank steepness**: slopeScale/hillScale vary from 0.7 (flat open S0) to 2.0 (narrow mountain valley S4)
- [x] **Native bush trees** (`createNativeTree`): rimu (tall trunk, wide flat canopy, drooping sub-lumps) and tōtara (thick trunk, buttress roots, dense rounded canopy). Dark deep-green palette. Used 80% in S3-4, 40% in S2, 0% in S0-1.
- [x] **Raupō bulrush** (`createRaupo`): tall stalks with brown cigar-shaped seed heads. Reuses reed sway animation. S1 primary margin plant.
- [x] **Flax/harakeke bush** (`createFlaxBush`): fan of blade-like leaves. S1-S4 margin plant.
- [x] **Section-specific vegetation selection**: S0 sparse with wider tree spacing, S1 raupō/flax margins, S2 mixed native/generic, S3-4 predominantly native bush.
- [x] **Adjusted density arrays**: rocks higher in S2 (0.50), flowers decrease in bush sections, pebbles higher in open sections.
- [x] **S2 rapids boulders**: larger rocks (0.6-1.4 size) that poke above water surface.
- [x] **Dynamic atmosphere progression** (`SECTION_ATMOSPHERE` + `updateAtmosphere`):
  - Fog color shifts from warm jade-white (S0) to cool blue-green (S4)
  - Fog distance tightens: near 80→50, far 150→105
  - Sun intensity dims: 1.45→1.15
  - Hemisphere light dims: 0.6→0.48
  - Tone mapping exposure decreases: 1.35→1.15
- [x] Atmosphere resets on game restart

Testing:
- [x] Screenshots across all 5 sections verified visual progression
- [x] Zero JS errors across full game distance (0-1400m)
- [x] All existing gameplay systems unaffected
