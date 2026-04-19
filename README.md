# Muse — a Jellyfin theme

Modern, minimalist custom CSS for Jellyfin Web. Deep charcoal canvas, violet accent, white pill CTAs, generous radii, restrained motion.

Inspired by the visual language of Netflix, Prime Video (Vision Pro), and modern streaming dashboards — but tuned to keep your library the focus, not the chrome.

## Preview (what changes)

- **Canvas** — near-black (`#0a0a0d`) with a soft radial violet glow for depth
- **Header** — translucent with backdrop blur, pill-shaped tabs
- **Sidebar** — rounded nav items, violet-tinted selected state
- **Cards** — 14px radii, subtle lift on hover, thin accent progress bars
- **Buttons** — white pill primary (Play), circular glass icon buttons for secondaries
- **Detail pages** — smooth backdrop gradient fade, large poster with elevation
- **Player OSD** — blurred gradient, minimal transport, violet scrubber
- **Dialogs / menus** — 20px radii, 1px hairline borders, soft shadow

## Install

Two ways. Pick one.

### Option A — Paste (fastest, no hosting)

1. Open `theme.css`, copy the entire contents.
2. In Jellyfin: **Dashboard → General → Custom CSS code**.
3. Paste → **Save**.
4. Hard-refresh the browser (`Cmd/Ctrl + Shift + R`).

### Option B — `@import` from GitHub (recommended)

Paste a single line into the Custom CSS field:

```css
@import url("https://cdn.jsdelivr.net/gh/iamngoni/jellyfin-next@master/theme.css");
```

**Why jsDelivr and not `raw.githubusercontent.com`?** GitHub serves raw files as `Content-Type: text/plain` with `X-Content-Type-Options: nosniff`, which tells browsers to reject the file as CSS. The `@import` silently fails. jsDelivr proxies the same file with `Content-Type: text/css`, plus CDN caching and no rate limits.

**Cache busting while iterating.** `@master` is cached for ~12 hours. Two options:

1. Pin to a specific commit (immutable, no cache issues):
   ```css
   @import url("https://cdn.jsdelivr.net/gh/iamngoni/jellyfin-next@<commit-sha>/theme.css");
   ```
2. Or hit the purge endpoint after each push:
   ```
   https://purge.jsdelivr.net/gh/iamngoni/jellyfin-next@master/theme.css
   ```

### Option C — Local dev server (fastest feedback)

For live editing on the same machine:

```bash
# from this repo root
python3 -m http.server 8787
```

Then in Jellyfin Custom CSS:

```css
@import url("http://127.0.0.1:8787/theme.css");
```

Save, hard-refresh Jellyfin, and every edit to `theme.css` is one refresh away. Note: if you access Jellyfin over HTTPS, browsers will block the `http://` import — use Option A or B instead.

## Customizing

All colors live as CSS variables at the top of `theme.css` under `:root`. Change a few lines to reskin:

```css
--muse-accent:    #8b7cf8;  /* primary accent — try #2dd4bf for teal, #f59e0b for amber */
--muse-accent-hi: #a89cff;
--muse-bg:        #0a0a0d;  /* canvas */
```

Radii and motion tokens sit right below. No need to touch the rest unless you're overriding specific components.

## Covered surfaces

- Home, Library, Genre, Collections
- Item detail (movie, series, season, episode)
- Video player OSD (transport, scrubber, title)
- Login screen, user select
- Dashboard settings (tables, forms)
- Dialogs, menus, toasts, popovers
- Scrollbars, focus rings, loading spinners

## Notes

- Tested against Jellyfin Web 10.9+. Older versions may have different class names for a handful of selectors — report anything that looks off and we'll add overrides.
- Theme uses `!important` sparingly, only where Jellyfin's own styles also use it.
- Backdrop-filter requires a modern browser (Chrome 76+, Safari 9+, Firefox 103+). Older browsers fall back to flat colors.

## License

MIT.
