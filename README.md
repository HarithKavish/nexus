# Nexus

The launcher for the systems I run — [nexus.harithkavish.com](https://nexus.harithkavish.com).

A single static `index.html`. No build step, no dependencies. It loads
`style.css` from harithkavish.com, so it follows the main site's theme
automatically — light/dark via `data-theme`, same header and footer.

`HK Nexus.png` (1024px) is the source artwork. `logo.png` (256px),
`apple-touch-icon.png` (180px) and `favicon.png` (96px) are generated from it:

```bash
ffmpeg -y -i "HK Nexus.png" -vf "scale=256:256:flags=lanczos" -pix_fmt rgba logo.png
```

Deployed to GitHub Pages by `.github/workflows/deploy.yml` on every push to `main`.

## Adding a system

Tiles are generated from data, not markup. There are two sources and Nexus shows
the union of both.

**The main site.** Nexus loads `site-data.js` from harithkavish.com and reads its
`ecosystem` array, so a subdomain added there appears here with no edit to this
repo. That file is the one worth keeping current.

**A local list**, in the script at the bottom of `index.html`, so Nexus still
renders if that file is unreachable or restructured:

```js
var LOCAL_APPS = [
    { slug: "vm", name: "VM" },
    { slug: "forge", name: "Forge" }
];
```

A slug is all that is needed — the link, origin and host label are derived as
`https://<slug>.harithkavish.com`. Entries are merged by slug with the local one
winning, sorted by name, and anything in `EXCLUDED` is dropped (Nexus itself).

Because tiles are built in the browser, the grid is empty with JavaScript off.
The main site renders the same way.

## Icons

Icons need no configuration. Each tile walks a list of conventional icon paths on
its own origin — vector first, then the large PNGs, with `favicon.ico` last — and
shows the first that loads. A system serving none keeps an empty mark.

A system whose icon lives elsewhere gets an entry in `ICON_OVERRIDES`, keyed by
slug. Blog needs one because it declares the main site favicon rather than
serving its own.

Logos are then measured in a canvas and scaled so the artwork fills the tile,
since most icons ship with blank margin baked into the image. A logo that is
already edge to edge is left alone, and one whose pixels cannot be read
cross-origin is shown exactly as served.

The `.app-tile` styles are the only CSS this page defines — everything else comes
from the shared theme, and they are built from its tokens so they follow it.
