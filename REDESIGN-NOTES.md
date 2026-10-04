# Redesign notes

## Design
- New `assets/style.css` (all pages share it). Tokens at the top: change colors, borders and shadows in `:root`.
- Tool-first layout: the tool box sits directly under the title; the first ad slot moved below the tool and a second sits above "Related tools".
- One loud element: the yellow action button, hard-edged tool box and result tray. Everything else stays quiet.
- Homepage: live Yes/No decider, real category tabs with counts, colour-coded tool cards.
- Dark mode, visible keyboard focus, reduced-motion support, no horizontal scroll down to 320px wide.

## Bugs fixed (present in the original upload)
- None of the 134 tool pages set `data-kind` on `<body>`, so every tool returned a random "activity". Each page now has the correct kind, and the list tools use what the visitor typed.
- Homepage categories were assigned in a repeating cycle (e.g. Coin Flip = "Generators", Yes/No = "People"). They now come from the real category pages.
- Shuffles used `sort(() => Math.random() - .5)` (biased). Replaced with Fisher-Yates.
- Randomness now uses `crypto.getRandomValues` (password generator and PIN included). The FAQ text on each page was updated to match.
- Teams: number of teams is capped at the number of names; empty list shows a message.
- Placeholder copy on the homepage ("ready for expansion and SEO content") replaced with visitor-facing text.

## Added to app.js
Data and logic for tools that had none: month, day, season, planet, flower, tree, instrument, dog/cat breed, movie genre, would-you-rather, usernames/gamertags, word pairs, coordinates, lottery numbers.

## Still to do
- Replace https://example.com (see DEPLOYMENT.md).
- Idea/prompt tools still draw from very short lists (2-11 entries). Expand them before applying for ads.
- "Generators" holds 79 of 134 tools (dice, ideas, names, etc.). Splitting it into smaller categories would help browsing and SEO.
- Paths start with `/` so the site must be served from a domain root (not a GitHub Pages project subfolder).
