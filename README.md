# Nexus

Home for my systems — [nexus.harithkavish.com](https://nexus.harithkavish.com).

```
NEXUS
 ├── VM   vm.harithkavish.com
 └── VR   vr.harithkavish.com
```

One static `index.html`. No build step, no dependencies. Styling comes from the
Harith Design System hosted on the main site, so Nexus stays in sync with
harithkavish.com automatically.

GitHub Pages serves it straight from the branch root (Settings → Pages → Deploy
from a branch → `main` / `/`). `CNAME` pins the domain.

## Adding a system

Copy one link in `index.html` and point it at its subdomain:

```html
<a href="https://ai.harithkavish.com" class="footer-btn" title="What it is">
    <span class="status-dot unknown" data-system="ai"></span>
    AI
</a>
```

## Status dots

Grey by default — nothing is assumed to be online. When a system exposes a status
endpoint that returns `{"status": "online"}` (CORS-readable from this domain), add
it to that system's dot and it goes live:

```html
<span class="status-dot unknown" data-status="https://vm.harithkavish.com/api/status"></span>
```

Anything else — offline, a timeout, a bad response — leaves the dot grey. Same
contract the main site uses for SkinNet Analyzer.
