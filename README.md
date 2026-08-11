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

Copy one tile in `index.html` and point it at the system:

```html
<a class="app-tile" href="https://api.harithkavish.com" target="_blank" rel="noopener noreferrer">
    <span class="app-tile__icon" aria-hidden="true">
        <img class="app-tile__favicon" data-origin="https://api.harithkavish.com" alt="" decoding="async">
    </span>
    <span class="app-tile__text">
        <span class="app-tile__name">API</span>
        <span class="app-tile__meta">api.harithkavish.com</span>
    </span>
</a>
```

The grid fills itself, so tiles reflow on their own as more are added.

Icons need no configuration. Each tile walks a list of conventional icon paths on
its own origin — vector first, then the large PNGs, with `favicon.ico` last — and
shows the first that loads. A system serving none keeps an empty mark.

Logos are then measured in a canvas and scaled so the artwork fills the tile,
since most icons ship with blank margin baked into the image. A logo that is
already edge to edge is left alone, and one whose pixels cannot be read
cross-origin is shown exactly as served.

The `.app-tile` styles are the only CSS this page defines — everything else comes
from the shared theme, and they are built from its tokens so they follow it.
