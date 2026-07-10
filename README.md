# ANNALS — a living kingdom in a single file

A procedurally generated fantasy kingdom rendered in real-time 3D that you can
watch for five minutes or five hours. Zoom from a satellite view of the whole
realm down to a market square. Time runs; harvests come in; caravans crawl the
roads; a queen dies without a clear heir and the great houses raise banners;
plague follows the trade routes; a dragon notices the treasury has gotten
large. Everything that happens is written into a scrolling **Chronicle** in the
voice of a medieval annalist, and a cinematic **auto-director** flies the
camera to the story as it unfolds.

**The whole app is one file: [`index.html`](index.html).**
Vanilla JS + Three.js r128 from CDN. No build step, no framework, no backend,
no assets — everything is procedural (terrain, buildings, heraldry, names).

## Run it

Open `index.html` in a browser, or drop it on any static host (Netlify, GitHub
Pages). That's it.

- **Persistence is the seed**: the URL hash (`#s=1234567`) fully determines the
  generated world. *Copy share link* reproduces your realm exactly.
- **Export chronicle** downloads the full annals of your run as a `.txt`.

## Controls

| Input | Action |
|---|---|
| drag | orbit · **right-drag** pan · **scroll** zoom (5 m – 4 km) |
| click | inspect settlements, buildings, armies, caravans, the dragon |
| `Space` | pause · `1–4` speeds (up to 30 sim-days/sec) |
| `C` | **Watch mode** — pure documentary screensaver |
| `H` | hide UI · `Esc` deselect / cancel placement |

The left drawer has four tabs: **Rates** (harvest, plague virulence, house
aggression, myth dial…), **Acts** (Unleash plague · Wake the dragon ·
Assassinate the monarch · Contest the succession…), **Overlays** (territories,
trade, prosperity, plague, unrest), and **Realm** (seed, houses, succession).

## How it works

- Deterministic worldgen via seeded `sfc32` RNG with **separate streams** for
  generation and history — intervening in history never changes the map.
- Worldgen pipeline: fBm terrain with domain warping and a mountain spine →
  flow-accumulation rivers → biomes → settlement siting → A* king's roads →
  organic street/building layout (12 archetypes × 3 tiers) → houses, heraldry,
  and a cast of ~140 named notables.
- Sim tick = 1 day: Weather → Economy → Population → Politics → Military →
  Threats → Growth → Chronicle. Every positive feedback loop ships with a
  predator (big treasuries attract dragons and courtly waste; strong houses
  chafe; growth strains granaries).
- Two-layer population model: pools per settlement drive economy and levies;
  named notables age, marry, inherit, win epithets, and die on camera.
- Threats are couplings, not effects: plague rides caravans (settlements above
  15% infected refuse trade — emergent quarantine), fire spreads through the
  building graph biased by wind and drought, bandit camps prey on the roads,
  and the dragon's wake probability scales with the treasury.

Verified: 200 unattended sim-years keep population, treasury, and the houses
within sane bounds — and the realm still produces story.
