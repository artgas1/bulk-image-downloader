# Product site

Live: **https://artgas1.github.io/bulk-image-downloader/**

| Page | URL | Used as |
|---|---|---|
| Landing | `/` | Homepage URL in the store listing |
| Welcome | `/welcome.html` | opened once on install by the service worker (`WELCOME_URL` in `src/background.js`), course 3.2 |
| Privacy | `/privacy.html` | mirror of the gist that the listing points at |

`welcome.html` is **generated** — do not edit it by hand:

```bash
python3 tools/build_site_welcome.py     # inlines all 52 locales from src/_locales
node test/run-site-welcome.mjs          # renders every locale in a real browser
```

The page picks the visitor's language client-side from `navigator.languages`
(exact tag -> base language -> English), so the onboarding is localized the same
way the in-extension copy is.

Deploying an update:

```bash
cd /tmp && rm -rf bid-site && cp -R <repo>/launch/bulk-image-downloader/site bid-site
cd bid-site && git init -q -b main && git add -A && git commit -qm "site update"
git remote add origin https://github.com/artgas1/bulk-image-downloader.git
git push -f origin main
```

No analytics and no cookies on any page — the store description promises the
extension tracks nothing, and the site keeps that promise too.
