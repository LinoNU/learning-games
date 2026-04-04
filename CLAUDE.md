# Project Brief: games.linocoria.com

> **Purpose of this document:** Provide full context to Claude Code so it can assist in building,
> maintaining, and extending the Dr. Lino's Learning Games website without requiring repeated
> explanations of the project.

---

## 1. Project Overview

**Site:** `games.linocoria.com`
**Repository name (suggested):** `games.linocoria.com` (or `lino-learning-games`)
**Hosted via:** GitHub Pages (static site, no backend)
**Owner:** Dr. Lino Coria Mendoza — Associate Teaching Professor & MSAI Program Director,
Northeastern University (Khoury College of Computer Sciences, Vancouver campus)

### Purpose

This is a collection of free, browser-based educational games aimed at **children**. It is part of a
**Broadening Participation in Computing (BPC)** initiative. The goal is to make computing, math,
science, and general learning approachable and fun for kids from all backgrounds — no installations,
no logins, no cost.

### Audience

- Primary: Children (approximately ages 6–14)
- Secondary: Teachers and parents who share links with children
- All content must be age-appropriate, inclusive, and accessible.

---

## 2. Repository Structure

```
games.linocoria.com/
│
├── index.html                  ← Landing page (game directory, organized by category)
├── README.md                   ← Public-facing repo description
├── CLAUDE.md                   ← This file (context for Claude Code)
├── favicon.ico
│
├── assets/                     ← Shared across all pages
│   ├── css/
│   │   └── main.css            ← Shared styles (tokens, header, footer, card grid)
│   ├── js/
│   │   └── main.js             ← Shared scripts (none yet — reserved)
│   └── images/
│       └── og-preview.png      ← Open Graph image for social sharing
│
└── games/
    ├── math/
    │   └── <game-slug>/
    │       ├── index.html
    │       └── ...             ← All assets the game needs (js, css, images)
    ├── science/
    │   └── <game-slug>/
    ├── computing/
    │   └── <game-slug>/
    └── fun/
        └── <game-slug>/
```

### Key rules

- Every game lives in its own self-contained folder under `games/<category>/<game-slug>/`.
- Each game's entry point is `index.html` inside that folder.
- Games must not depend on files outside their own folder, except for fonts loaded from Google Fonts
  CDN.
- The folder name becomes the URL slug (use lowercase kebab-case, e.g. `addition-adventure`).

---

## 3. Categories

| Category ID | Label      | Emoji | Accent colour |
|-------------|------------|-------|---------------|
| `math`      | Math       | ➕     | `#ff6b6b`     |
| `science`   | Science    | 🔬    | `#4ecdc4`     |
| `computing` | Computing  | 💻    | `#6c63ff`     |
| `fun`       | Fun        | 🎉    | `#ffd166`     |

To add a new category in the future: (1) add a new `<section>` block in `index.html`, (2) create the
corresponding folder under `games/`, (3) add the design tokens for the new accent colour.

---

## 4. Design System

### Fonts (loaded from Google Fonts)

| Role         | Font family | Weights used |
|--------------|-------------|--------------|
| Display/headings | Fredoka   | 400, 600, 700 |
| Body/UI      | Nunito      | 400, 600, 700 |

### CSS Custom Properties (design tokens)

Defined in the `<style>` block of `index.html` (and should be moved to `assets/css/main.css` once
shared styles grow):

```css
--clr-bg:          #f5f0e8   /* warm off-white page background */
--clr-surface:     #ffffff   /* card backgrounds */
--clr-text:        #2c2c3a   /* primary text */
--clr-muted:       #7a7a8c   /* secondary/description text */
--clr-header-bg:   #2c2c3a   /* header and footer background */
--clr-header-txt:  #f5f0e8   /* header text */

/* Per-category pairs: full saturation + soft tint */
--clr-math:        #ff6b6b
--clr-math-soft:   #fff0f0
--clr-sci:         #4ecdc4
--clr-sci-soft:    #f0fdfb
--clr-comp:        #6c63ff
--clr-comp-soft:   #f3f2ff
--clr-fun:         #ffd166
--clr-fun-soft:    #fffbf0
```

When creating individual game pages, reuse these tokens by either:
- Repeating the `:root {}` block in the game's own `<style>`, or
- Linking to `../../assets/css/main.css` (adjust the relative path based on nesting depth).

### Component: Game Card

A game card consists of:

```
.game-card (anchor tag)
  └── .card-thumb   (emoji thumbnail, coloured soft background)
  └── .card-body
        ├── .card-title
        ├── .card-desc
        └── .card-play  (coloured CTA button)
```

Cards with `soon: true` in the game registry get the `.coming-soon` class (dimmed, non-clickable)
and a "Coming Soon" badge.

---

## 5. Game Registry (how to add a game)

All games are registered in a single JavaScript array inside `index.html`. To add a game, append
an object to the `games` array:

```js
{
  title:    "Addition Adventure",       // Display name on the card
  desc:     "Race to solve problems!",  // One-sentence description
  category: "math",                     // "math" | "science" | "computing" | "fun"
  path:     "games/math/addition-adventure/",  // Relative path to the game folder
  emoji:    "🔢",                       // Emoji shown as card thumbnail
  soon:     false                       // Optional. true = Coming Soon badge
}
```

The landing page renders cards dynamically from this array. No other changes to `index.html` are
needed when adding a game (only the registry entry + the actual game files).

---

## 6. Individual Game Pages

### Requirements for every game

- **Self-contained:** All JS, CSS, and image assets must live inside the game's own folder.
- **No external dependencies** beyond Google Fonts CDN (no npm, no build step).
- **Mobile-friendly:** Must work on tablets and phones (many children use these devices).
- **Accessible:** Use semantic HTML, ARIA labels where appropriate, sufficient colour contrast.
- **Back navigation:** Every game must include a clearly visible link back to the landing page
  (`../../index.html` or the full URL `https://games.linocoria.com`).
- **Age-appropriate:** Friendly language, simple instructions, no violent or inappropriate content.

### Suggested game page structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Game Title – Dr. Lino's Learning Games</title>
  <!-- reuse Google Fonts from landing page -->
</head>
<body>
  <header>
    <a href="../../index.html">← Back to all games</a>
    <h1>Game Title</h1>
  </header>

  <main>
    <!-- Game content here -->
  </main>

  <footer>
    <p>Dr. Lino's Learning Games · <a href="https://linocoria.com">linocoria.com</a></p>
  </footer>
</body>
</html>
```

---

## 7. GitHub Pages Setup

1. Push the repo to GitHub (e.g. `github.com/LinoNU/learning-games`).
2. Go to **Settings → Pages**.
3. Set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. GitHub will publish the site at `https://LinoNU.github.io/learning-games/`.

---

## 8. Custom Domain Setup (games.linocoria.com)

### In GoDaddy DNS (for linocoria.com)

Add a **CNAME record**:

| Type  | Name  | Value                                        | TTL  |
|-------|-------|----------------------------------------------|------|
| CNAME | games | LinoNU.github.io.                            | 1hr  |

### In the GitHub repo

Create a file named `CNAME` in the repo root with exactly one line:

```
games.linocoria.com
```

GitHub Pages will then serve the site at `games.linocoria.com` automatically (HTTPS included).

---

## 9. Content & Tone Guidelines

- Write all on-screen text at a **reading level appropriate for ages 6–12** (short sentences,
  simple vocabulary).
- Instructions should be **immediately clear** — avoid paragraphs of rules before the game starts.
- Use **positive reinforcement** ("Great job!", "Keep going!"), not negative messages.
- Avoid scoring systems that shame low performance; focus on encouragement and progress.
- The site serves a **diverse audience** — avoid cultural assumptions; keep content inclusive.

---

## 10. Future Considerations

- **Leaderboards / progress tracking** — not planned yet; would require a backend or third-party
  service. Keep games stateless for now.
- **Translations** — a Spanish version may be added later (Dr. Coria is bilingual; the site
  supports a BPC audience that includes Spanish-speaking families).
- **Accessibility audit** — run Lighthouse and axe before each public launch.
- **New categories** — e.g. `language`, `art`, `social-studies` — the structure supports this
  trivially.