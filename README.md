# YouTube Clone — Vue 3 + Tailwind CSS + Vite

A base project structure for a YouTube-style UI, built with Vue 3 (Composition API),
Tailwind CSS, and Vite. Fully modular — every part of the app is its own file.

## Project structure

```
youtube-clone/
├── index.html              # Vite entry HTML
├── package.json
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
├── public/
│   └── favicon.svg
└── src/
    ├── main.js              # App bootstrap
    ├── App.vue              # Root component (layout + state)
    ├── style.css            # Tailwind directives + global CSS
    ├── data/
    │   └── mockData.js      # Videos, categories, sidebar links, subscriptions
    └── components/
        ├── Header.vue       # Top bar: logo, search, sidebar toggle
        ├── Sidebar.vue      # Collapsible left nav
        ├── VideoCard.vue    # Single video thumbnail card
        └── Icon.vue         # Inline SVG icon set
```

## Getting started

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start the dev server (hot reload):
   ```bash
   npm run dev
   ```
   Opens at `http://localhost:5173`

3. Build for production:
   ```bash
   npm run build
   ```
   Output goes to `dist/`

4. Preview the production build:
   ```bash
   npm run preview
   ```

## Features in this build

- **Theme switching** — a sun/moon icon in the header (and "Appearance" in the
  profile menu) toggles light/dark mode app-wide, persisted to `localStorage` via
  `src/utils/theme.js`.
- **Reliable video playback** — the watch page and Shorts player explicitly
  `.load()` + `.play()` the `<video>` element whenever you switch videos (changing
  a `src` attribute alone doesn't reload media in most browsers — this was the
  root cause of "the video doesn't work" when clicking between videos). Both also
  fall back to a small, reliable CC0 clip if the primary source ever errors.
- **Every author has a profile** — click any channel name/avatar (on a card or the
  watch page) to open that channel's page (`src/data/mockData.js` → `CHANNELS`),
  showing their bio, subscriber count, and their videos.
- **Deletable playlists** — every custom playlist has a trash icon (in the
  Playlists library and on its detail page). The built-in "Saved" playlist can't
  be deleted, same as Watch Later in real YouTube.
- **Shorts** — a real vertical Shorts feed and player (`SHORTS` in mockData.js),
  with Like, Up/Down navigation between Shorts, and a fallback clip on error.
- **Upload videos** — the "+" Create menu, the "Your videos" empty state, and your
  profile's "Manage videos" button all open an upload modal. Publishing adds a
  real entry to the home feed, "Your videos", and your channel page.
- **Comments** — every watch page has a comment box and list
  (`src/components/CommentSection.vue`); posting adds a real comment as "you".
- **Category filtering** — buttons in the main section (`All`, `Music`, `Gaming`, etc.)
  filter the video grid by each video's `category` field.
- **Logo → homepage** — clicking the YouTube logo (or "Home" in the sidebar) clears
  search/category filters and reshuffles the feed.
- **Shuffled, "suggest something new" feed** — video order is randomized on load
  and via the **Shuffle** button (`src/utils/shuffle.js`).
- **Hover-to-play previews** — cards show a real, playable `<video>` on hover, with
  the video's description, Like, and Save-to-playlist controls.
- **Topic-matched thumbnails** — fetched by category keyword instead of a random
  unrelated stock photo, with an automatic fallback if a thumbnail fails to load.
- **A fully wired sidebar** — Home, Shorts, Subscriptions, History, Playlists, Your
  videos, Watch later, and Liked videos are all real navigation targets.
- **Header menus** — Create, Notifications, and Profile are all working dropdowns
  (click outside to close). The profile menu is styled dark, like the reference
  screenshot, and includes "View your channel."

## Where to make changes

- **Content / mock videos** → `src/data/mockData.js`
- **Layout & page state (sidebar toggle, search, filtering)** → `src/App.vue`
- **Top navigation bar** → `src/components/Header.vue`
- **Left sidebar / nav links** → `src/components/Sidebar.vue`
- **Individual video card design** → `src/components/VideoCard.vue`
- **Icons** → `src/components/Icon.vue`
- **Global styles / Tailwind config** → `src/style.css`, `tailwind.config.js`

## Next steps you might want

- Add Vue Router for a `/watch/:id` video page and a real navigation flow
- Replace mock data with a real API (YouTube Data API, or your own backend)
- Add a Pinia store if state grows beyond simple `ref`s
- Add dark mode via Tailwind's `dark:` variant
