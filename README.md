# Paul Marvin: portfolio

My personal portfolio, built as a small desktop-style interface in plain HTML, CSS and JavaScript.
There is no framework and no build step: open `index.html` through any static server.

    python -m http.server 8000      # then visit http://localhost:8000

## What's in it

| File | Purpose |
|---|---|
| `index.html` | Page structure: menu bar, windows (About, Journey, Projects, Terminal, Safari, Reach out, Calendar, Calculator, Preferences), dock |
| `style.css` | All styling: theme variables, glass finish, dark theme, responsive layout |
| `script.js` | Window manager, dock, terminal, Safari search, booking and contact forms, preferences |
| `intro-bg.html` | Animated wallpaper, loaded in an iframe after the page has settled |
| `search-api/` | Azure Function (Python) that returns Google web and image results for the Safari window |

## How it works

- **Windows:** each window is a `<section>` that `script.js` opens, drags, resizes, minimises into the dock,
  and snaps to half or full screen. Below 900px wide, windows are shown full screen instead.
- **Terminal:** a small simulated shell written in JavaScript. It has an in-memory file system, command history,
  tab completion and desktop commands (`open`, `theme`, `snap`).
- **Safari:** searches Wikipedia, Stack Exchange, GitHub and Wikimedia Commons directly from the browser, and
  uses the Azure Function in `search-api/` for Google results.
- **Contact form:** sends through Formspree.
- **Preferences:** wallpaper, clock, dock and theme choices are kept in `localStorage`.

## Performance notes

The wallpaper starts only when the browser is idle and runs a lighter version on small or slow devices.
The profile photo ships as WebP with a JPEG fallback, and fonts load without blocking the first paint.
