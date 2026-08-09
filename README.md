# Nexus

One way into the systems I run — [nexus.harithkavish.com](https://nexus.harithkavish.com).

A single static `index.html`. No build step, no dependencies. It loads
`style.css` and the logo from harithkavish.com, so it follows the main site's
theme automatically — light/dark via `data-theme`, same header, cards and pills.

Deployed to GitHub Pages by `.github/workflows/deploy.yml` on every push to `main`.

## Adding a system

Copy one card in `index.html` and change five things — pill, route, title,
summary, link:

```html
<article class="card ecosystem-card">
    <div class="card__topline">
        <span class="pill pill--live">Live</span>
        <span class="card__route">api.harithkavish.com</span>
    </div>
    <h3 class="card__title">API</h3>
    <p class="card__body">What it does.</p>
    <a class="card__link" href="https://api.harithkavish.com">Visit api.harithkavish.com</a>
</article>
```

Pill classes: `pill--live`, `pill--progress`, `pill--planned`, `pill--neutral`.

Statuses and summaries here mirror the `ecosystem` list in the main site's
`site-data.js`. Keep the two in step when a system's status changes.
