# Nexus

The launcher for the systems I run — [nexus.harithkavish.com](https://nexus.harithkavish.com).

A single static `index.html`. No build step, no dependencies. It loads
`style.css` and the logo from harithkavish.com, so it follows the main site's
theme automatically — light/dark via `data-theme`, same header and footer.

Deployed to GitHub Pages by `.github/workflows/deploy.yml` on every push to `main`.

## Adding a system

Copy one tile in `index.html` and point it at the system:

```html
<a class="app-tile" href="https://api.harithkavish.com">
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

Icons need no configuration. Each tile tries `favicon.svg`, `favicon.ico`,
`favicon.png` then `apple-touch-icon.png` on its own origin and shows the first
that loads. A system serving none keeps an empty mark.

The `.app-tile` styles are the only CSS this page defines — everything else comes
from the shared theme, and they are built from its tokens so they follow it.
