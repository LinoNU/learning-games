# Dr. Lino's Learning Games

Free, browser-based educational games for kids — no installs, no logins, no cost.

**Live site:** [games.linocoria.com](https://games.linocoria.com)

---

## About

This is a collection of educational games aimed at children (ages 6–14) as part of a **Broadening Participation in Computing (BPC)** initiative by Dr. Lino Coria Mendoza, Associate Teaching Professor & MSAI Program Director at Northeastern University (Khoury College of Computer Sciences, Vancouver campus).

The goal is to make computing, math, science, and general learning approachable and fun for kids from all backgrounds.

## Categories

| Category  | Emoji | Description |
|-----------|-------|-------------|
| Math      | ➕    | Numbers, arithmetic, and problem solving |
| Science   | 🔬    | Explore the natural world |
| Computing | 💻    | Algorithms, logic, and computational thinking |
| Fun       | 🎉    | Mixed topics and creative challenges |

## Repository Structure

```
learning-games/
├── index.html              ← Landing page (game directory)
├── CNAME                   ← Custom domain for GitHub Pages
├── favicon.svg
│
├── assets/
│   ├── css/main.css        ← Shared design tokens and styles
│   ├── js/main.js          ← Shared scripts (reserved)
│   └── images/
│       └── og-preview.png  ← Open Graph social sharing image
│
└── games/
    ├── math/
    ├── science/
    ├── computing/
    └── fun/
```

Each game lives in its own self-contained folder under `games/<category>/<game-slug>/` with an `index.html` entry point.

## Adding a Game

1. Create a folder: `games/<category>/<game-slug>/`
2. Add `index.html` (and any JS/CSS/images the game needs) inside that folder
3. Register the game in the `games` array in `index.html`:

```js
{
  title:    "Addition Adventure",
  desc:     "Race to solve addition problems!",
  category: "math",
  path:     "games/math/addition-adventure/",
  emoji:    "🔢"
}
```

The landing page renders cards automatically from this array.

## Development

No build step required. Open `index.html` directly in a browser, or serve locally:

```bash
npx serve .
# or
python3 -m http.server
```

## Deployment

Hosted on **GitHub Pages** from the `main` branch root. Pushes to `main` deploy automatically. The custom domain `games.linocoria.com` is configured via the `CNAME` file and a DNS CNAME record pointing to `LinoNU.github.io`.

## License

See [LICENSE](LICENSE).
