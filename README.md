# Fear & Loathing Trail

> *"We can't stop here — this is bat country."*

A Fear and Loathing-themed Oregon Trail multiplayer road trip game. Drive from Las Vegas to Bogotá, Colombia through 11 stops across Mexico and Central America. Buy drugs, hunt Red Hats, survive micro-events, and arrive with your sanity (mostly) intact.

**Live:** Deploy via [Vercel](https://vercel.com) from this repo — one click, zero config.

---

## Changelog

### v17.0.0 — Car Radio
| # | Category | Change |
|---|----------|--------|
| 01 | Version | All version strings, PEER_PREFIX, STORE_KEY bumped to v17 |
| 02 | Car Radio | In-game car radio using Howler.js (jsDelivr CDN) |
| | | 15 MP3 tracks served from `/public/audio/` via jsDelivr |
| | | Requires user gesture to activate (browser autoplay policy) |
| | | ⏮ ⏯ ⏭ controls + volume slider in persistent radio bar |
| | | Track name marquee scrolls in radio bar on scr-map |
| | | Howler.js `html5:true` for streaming (no full-file download) |
| | | Auto-advances to next track on end; skips on load error |
| 03 | Vercel | `vercel.json` added: audio byte-range headers, SW cache headers |

---

### v16.3.0 — Drug System, DOOM Fix, Player List
| # | Category | Change |
|---|----------|--------|
| 01 | Version | Title/CFG/manifest/sw bumped to v16 |
| 02 | Version | PEER_PREFIX flt16room, STORE_KEY flt16_player |
| 03 | Trail Stops | Route redesigned: Las Vegas to Bogotá, Colombia |
| | | Phoenix / El Paso / Mexico City / Oaxaca / Guatemala City |
| | | Managua / San Jose / Panama City / Medellin / Bogotá |
| 04 | Character Create | Age buttons replaced with range slider 18–80 |
| | | Live display of chosen age value |
| 05 | Geo Location | Non-blocking geo screen shown before char create |
| | | Allow/deny: allow pulls skills bonus from lat/lon |
| 06 | Hunt / DOOM | Full Wolf3D raycaster replaces v15 parallax engine |
| | | DFS-generated 22×22 maze, DDA ray casting per column |
| | | Wall height = W×0.72/dist perspective projection |
| | | Sprite z-buffer: enemies hidden behind walls |
| | | 4-direction D-pad (forward/back/strafe L/R) mobile |
| | | Torch sprites with flicker and glow halo |
| | | Screen-space blood particles on kill (gore splat) |
| | | Per-tile wall shading: 4 tile types, side darkening |
| | | Enemy sprites projected via camera-plane transform |
| | | Pixel art per enemy type (bat, freak, flag shirt) |
| | | Gold outline on heavy/elite tier enemies |
| 07 | Hunt Timer | Hunt timer extended: 30s to 90s |
| 08 | Travel Screen | Metal Slug X style cinematic travel screen |
| | | 5 parallax layers (sky/mountains/mid/fg/road) |
| | | 5 biomes based on route segment (desert/jungle/mountain/coast/city) |
| | | Road perspective trapezoid with sine-wave inclines |
| | | Pixel-art car: bounce, lean, wheels, exhaust, glow |
| | | Background entities every 55 frames: cars, trucks, |
| | | pedestrians, UFO tractor beam, bigfoot, Godzilla |
| | | Mini world map overlay with animated route dot |
| 09 | Travel Events | Minimum 3 events per travel leg (up to 4) |
| 10 | Ration System | 4 ration tiers selectable from travel screen |
| | | tiny_tim (0 supply cost, sanity −5) |
| | | normal (1 supply, no modifier) |
| | | fat (2 supply, sanity +5) |
| | | cholesterol_daddy (3 supply, sanity +10) |
| 11 | Hustle Mini-game | Canvas slider timing game; green zone scales with skills.smooth |
| | | One use per stop (hustleUsed flag) |
| 12 | Busk Mini-game | Simon-says 4-color pad, up to 4 rounds |
| | | Partial credit on fail; one use per stop (buskUsed) |
| 13 | Shank Mechanic | 2s dodge window via SHANK_ALERT WebRTC broadcast |
| | | SHANK_DODGE message sets _shankDodged on attacker |
| 14 | Per-stop Flags | hustleUsed/buskUsed/shankUsedThisStop reset on _travelArrive() |
| 15 | UI | Hustle/Busk show greyed "done" state when used |
| | | (.btn-used CSS: opacity 45%, pointer-events none) |
| 16 | Route Timeline | Total distance rescaled to 5,000 miles |
| 17 | Route Timeline | map-canvas expanded to 200px; bottom 44% is route timeline |
| | | with car sprite + orange progress glow |
| 18 | Route Timeline | City stops shown as evenly-spaced dots with emoji labels |
| | | completed = green, current = orange pulse |
| 19 | Route Timeline | 3 micro-event warning triangles between each stop pair |
| | | passed dots dim; active dots show orange ▲ |
| 20 | Route Timeline | Car sprite moves in real-time along timeline |
| | | headlight glow when traveling; miles label under |
| 21 | Travel Pacing | Travel now real-time: ~30s per leg in MapAnim RAF loop |
| | | stays on scr-map (no scr-travel switch) |
| 22 | Travel Pacing | Progress pauses at 25/50/75% to fire micro-event decision card |
| | | resumes after choice |
| 23 | Travel Pacing | phase='traveling' shows "On the road..." UI panel |
| | | Page reload during traveling resets to 'travel' |
| 24 | Solo Reset | Solo game (1 player) is NOT saved on page reload |
| | | Cash resets to default $350 on each fresh start |
| 25 | Drug System | Buy Drugs: market screen with 5 drug types |
| | | price scales by stop index (cheap near Colombia, pricey early on) |
| 26 | Drug System | Make Drugs: 4 production methods |
| | | Cook Meth: timing slider mini-game, $40 chemicals |
| | | Process Coke: 15-tap in 5s, $50 equipment |
| | | Grow Weed: passive, harvest in 2 stops |
| | | Moonshine Still: passive, collect next stop |
| 27 | Drug System | Sell Drugs: burner phone UI with 8 FIEND contacts |
| | | Each fiend wants a specific drug at their price |
| | | High-risk contacts flagged with bust % warning |
| 28 | Drug System | Deal Mini-Game "The Drop": heat meter 0–100% |
| | | Survive 8s mashing STAY COOL to drain heat |
| | | Random cop/siren events spike heat |
| | | Win = cash paid; Lose = stash seized + fine + sanity |
| 29 | Drug System | Drug inventory shown in stat bar chip (💊 count) |
| | | Cook flags methCookUsed/cokeCookUsed reset on arrive |
| 30 | DOOM Bug Fix | Enemy alpha was 1.4/dist — at dist=5, alpha=0.28 |
| | | Fix: al=1.0 (fully opaque, DOOM-style) |
| 31 | DOOM Bug Fix | Enemy sy=H/2−sh×0.9 pushed 90% into dark ceiling |
| | | Fix: sy=H/2−sh×0.55 (centers at eye-level horizon) |
| 32 | Player List | Convoy player list shown in action-area with name and alive/dead status |
| 33 | Multiplayer | PeerNet BATCNT default room — CHUNK 2 (pending) |

---

### v15.0.0 — DOOM FPS Hunt
| # | Category | Change |
|---|----------|--------|
| 01 | Version | Title/CFG/manifest/sw bumped to v15 |
| 02 | Version | PEER_PREFIX → flt15room, STORE_KEY → flt15_player |
| 03 | CSS | .bar: safe-area-inset-top padding for iPhone notch |
| 04 | CSS | #hunt-canvas: flex:1 (fills screen, no fixed height) |
| 05 | HTML | scr-hunt: quit button moved to BOTTOM bar |
| 06 | HTML | scr-hunt: wave counter displayed in HUD |
| 07 | HTML | Hunt timer changed from 60s → 30s display |
| 08 | MapAnim | _drawCar: isFinite guard prevents NaN crash |
| 09 | Hunt FPS | Full DOOM-style FPS rewrite with player.angle |
| 10 | Hunt FPS | Building parallax driven by player.angle / 2PI × W |
| 11 | Hunt FPS | 3 enemy depth tiers (far/mid/near) via scaleMult |
| 12 | Hunt FPS | Crosshair fixed at H×0.54; enemies chest at H×0.54 |
| 13 | Hunt FPS | WASD + arrow keys for desktop left/right rotation |
| 14 | Hunt FPS | Mouse drag delta-X to rotate view |
| 15 | Hunt FPS | Mobile: left-half D-pad, right-half drag-to-look |
| 16 | Hunt FPS | Mobile: tap right half = shoot |
| 17 | Hunt Enemies | 3 tiers: easy (40%), middle (37%), heavy (23%) |
| 18 | Hunt Enemies | 8 variants: bat, lizard, freak, rh_norm, rh_fat, rh_flag, elite_a, elite_b |
| 19 | Hunt Enemies | American flag shirt variant (rh_flag) with stripes |
| 20 | Hunt Enemies | Heavy tier: narrow hitbox (±13% h), head/chest only |
| 21 | Hunt Enemies | Middle tier: center-mass hitbox (±26% h) |
| 22 | Hunt Enemies | Easy tier: full-body hitbox (±44% h) |
| 23 | Hunt Enemies | Gold outline on heavy/elite enemies |
| 24 | Hunt Enemies | Kill caps per enemy type prevent endless farming |
| 25 | Hunt Waves | 3 waves of 6/7/7 enemies = 20 total per hunt |
| 26 | Hunt Waves | Wave text flash + synthesized air-raid siren alert |
| 27 | Hunt Carry | Max carry weight: 150 lbs (hunt ends at max) |
| 28 | Hunt Sound | 5 cycling kill sounds (Web Audio synthesized): moo, toasty, elvis, ranch-up, wilhelm |
| 29 | Hunt Sound | Air-raid siren on wave spawn (synthesized sawtooth) |
| 30 | Hunt BgEvents | Periodic background events every ~240 frames |
| | | UFO (with beam), nuclear explosion, helicopter |
| 31 | Hunt Misc | Quit button at bottom; hints in bottom bar |
| 32 | Hunt Misc | Supplies += floor(meat/10) on hunt end |

---

## Tech Stack

- **Frontend:** Vanilla JS, single `index.html` — no build step
- **Multiplayer:** PeerJS WebRTC mesh (peer-to-peer, no backend)
- **Audio:** Howler.js 2.2.4 via jsDelivr CDN, MP3s via jsDelivr GitHub CDN
- **Maps:** Canvas 2D — raycaster (DOOM/Wolf3D DDA), parallax travel, route timeline
- **PWA:** Service worker + web app manifest, OffscreenCanvas-generated icons
- **Deploy:** Vercel (static, zero-config)

## Deployment

```bash
# Push this repo to GitHub, then connect to Vercel
# vercel.json handles routing, audio byte-range headers, and SW cache headers
vercel --prod
```

## Audio Credits

Tracks in `/public/audio/` are served via jsDelivr from the GitHub repo.
