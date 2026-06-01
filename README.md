# Metal Clicker

A self-contained browser incremental/clicker game. Single static HTML file,
no build step, no dependencies, no server required.

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
  the `S` object, persisted via the artifact storage API when available and
  via Export/Import save codes (Settings) otherwise.
- The **shared leaderboard** relies on a `window.storage` shared-storage API
  that only exists when the game runs inside Claude. On GitHub Pages or a
  local file, that API is absent, so the leaderboard simply shows an
  "unavailable" message and the rest of the game works normally
  (clicking, upgrades, anvil skins, achievements, single-player saves).
- No external network calls, no third-party scripts except the Tabler Icons
  stylesheet loaded from a CDN for the UI icons.

## License / ownership

This is your project to use and modify however you like.
