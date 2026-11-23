# ambient-radio.alephvoid.com

[![Sponsor Aleph Void](https://img.shields.io/badge/Sponsor-Aleph%20Void-EA4AAA?logo=githubsponsors&logoColor=white)](https://github.com/sponsors/aleph-void)

Landing page for **Aleph Void Ambient Radio** — a 24/7 ambient music stream on YouTube, operated by Aleph Void, LLC.

Live at [ambient-radio.alephvoid.com](https://ambient-radio.alephvoid.com/). Sibling stations: [chiptune-radio.alephvoid.com](https://chiptune-radio.alephvoid.com/) and [glitch-radio.alephvoid.com](https://glitch-radio.alephvoid.com/).

## What it is

A single static HTML page. No build step, no dependencies, no framework — `index.html` contains the markup, styles, and the one script that mounts the YouTube embeds. Deployed via GitHub Pages; `CNAME` pins the custom domain.

```
index.html      markup + inline CSS + embed script
assets/         Aleph Void logo (SVG favicon, PNG for Open Graph)
CNAME           ambient-radio.alephvoid.com
```

## Local development

The YouTube embeds require a real HTTP origin, so opening `index.html` via `file://` will leave the player and chat blank. Serve it instead:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000/>.

The live chat embed builds its `embed_domain` parameter from `window.location.hostname`, which is what YouTube checks against — so `localhost` works in development and the custom domain works in production, with no config to switch between them.

## Changing the stream

The YouTube video ID is set once, in the script at the bottom of `index.html`:

```js
var video = 'lVLldjn5eQ8';
```

It also appears in the nav link, the player fallback note, and the Connect section. Update all four together.

## Design

The page deliberately mirrors chiptune-radio and glitch-radio — same layout skeleton, same section rhythm, same embed approach — so the stations read as siblings.

- **Palette** — the standard Aleph Void tokens, identical to `alephvoid.com`, `chiptune-radio`, `glitch-radio`, `morphix`, and `virux`. Do not substitute per-site colors here; change them upstream and propagate.

  | Token | Value |
  | --- | --- |
  | `--bg-primary` / `--bg-secondary` / `--bg-card` | `#0a0a0f` / `#12121a` / `#16161f` |
  | `--border` | `#1e1e2e` |
  | `--text-primary` / `--text-secondary` / `--text-muted` | `#e4e4e7` / `#a1a1aa` / `#71717a` |
  | `--accent` / `--accent-light` / `--accent-lighter` | `#6d28d9` / `#8b5cf6` / `#a78bfa` |

- **Type** — Inter for body and JetBrains Mono for labels are shared brand faces. Fraunces (light, high optical size) for display headings is specific to this site; headings stay in sentence case rather than the siblings' uppercase.
- **Motion** — two blurred fields of accent light drift behind the hero on a 48-second cycle, and the italic "Ambient" in the wordmark slowly widens and brightens over a 12-second breath. Those plus the live-status dot are the only animations, and all respect `prefers-reduced-motion`.

The design commits to a single dark theme, matching the siblings.

## License

[MIT](LICENSE) © 2026 Aleph Void, LLC.
