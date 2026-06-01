# Metal Clicker

A self-contained browser incremental/clicker game. Single static HTML file,
no build step, no dependencies, no server required.

## Features

- **Active forging** — the anvil isn't just a clicker. Heat the metal into a
  glowing **sweet zone**, then strike there for **PERFECT hits** (×2.6 + fast
  combo). Mash too fast and you **overheat**, losing your combo until it cools —
  so striking is a rhythm to manage, not a button to spam. The auto-striker only
  lands plain hits, so active perfect-striking always out-earns idling.
- **Forge Orders** — timed contracts ("forge X metal in 40s") that reward
  frenzies, bonus metal, or a recharged Overdrive. A reason to push hard.
- **Forge metal** by striking the anvil (mouse, tap, or Spacebar).
- **Passive income** — every building you buy produces metal/sec, even idle.
- **Offline earnings** — your forges keep working while the tab is closed; come
  back to a "Welcome back" payout (scaled by the Night Shift perk).
- **Forge Heat** — keep striking to heat the anvil for up to +60% click power.
- **Combos** — rapid clicks ramp a multiplier up to ×3.
- **Critical strikes** — random ×7 hits (raise the odds with Lucky Strikes).
- **Golden ingots** — appear at random; click for an instant payout, a ×7
  **Forge Frenzy**, or a ×77 **Click Frenzy**.
- **Power Drill** auto-striker that clicks for you.
- **Overdrive** — an active ability (button by the anvil) for a ×5 output surge
  on a cooldown.
- **Building milestones** — each building doubles its output at 10/25/50/100/
  150/200/250 owned.
- **Bulk buying** — ×1 / ×10 / Buy Max toggle in the shop.
- **Blueprints** — 19 one-time strategic upgrades (click/output multipliers,
  crits, heat, ingot luck, synergies) that unlock as you progress.
- **Reforge** for permanent output bonuses and **reputation**, spent in a
  **Reforge Tree** of 8 permanent perks.
- **Two blacksmiths** (Metal & Iron), 7 building tiers each.
- **24 achievements**, **9 anvil skins**, sound effects, reduced-motion option,
  and export/import save codes.
- **Saves automatically** to the browser (localStorage) and a local high-score
  board — works fully offline on GitHub Pages.

## What's here

- `index.html` — the entire game (HTML + CSS + JS in one file). This is the
  whole app. Open it in any browser to play.
- `DEPLOY-GUIDE.md` — plain-language, click-by-click guide for hosting on
  GitHub Pages.

## Run it locally

Just open `index.html` in a browser. Or serve the folder:

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

This is a static site, so Pages serves it directly. Because the entry file is
named `index.html`, the site loads at the repository root URL
(`https://USERNAME.github.io/REPO/`) with no extra path.

Manual steps are in `DEPLOY-GUIDE.md`. If using the GitHub CLI:

```
git init
git add .
git commit -m "Add Metal Clicker"
gh repo create metal-clicker --public --source=. --push
# then enable Pages: Settings > Pages > Source: Deploy from a branch > main / (root)
```

## Notes for anyone modifying the game

- Everything lives in `index.html`. The `<script>` is one IIFE; game state is
  the `S` object (save format `v:2`), persisted to **localStorage** and, when
  running inside Claude, also to the `window.storage` API. Old saves from the
  original version migrate automatically. Export/Import save codes are in
  Settings.
- Tuning constants live at the top of the script: `SHOPS` (buildings/costs),
  `PUPS` (reforge-tree perks), `ACHV` (achievements), `SKINS`, and the balance
  constants (`CRIT_MULT`, `HEAT_*`, `FRENZY_*`, etc.).
- The game loop is a single `requestAnimationFrame` tick handling production,
  the auto-striker, heat/combo decay, and live number display; heavier DOM
  updates (shop buttons, achievements) run on a 500ms interval.
- The **leaderboard** uses the `window.storage` shared API when the game runs
  inside Claude (a true shared board). On GitHub Pages or a local file that API
  is absent, so it falls back to a per-device **local high-score board** stored
  in localStorage — the panel stays useful everywhere.
- No external network calls, no third-party scripts except the Tabler Icons
  stylesheet loaded from a CDN for the UI icons.

## License / ownership

This is your project to use and modify however you like.
