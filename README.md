# clinicapogany-lp

Static landing pages for Clinica Pogany, deployed on Vercel. **The entire
deployment is set to no-index** (see "No-indexing" below).

## Pages

| URL | File |
| --- | --- |
| `/clinicapogany-lp/bariatric-surgery` | `clinicapogany-lp/bariatric-surgery/index.html` |

## No-indexing (three layers)

1. **`<meta name="robots" content="noindex, nofollow">`** in each page `<head>`.
2. **`X-Robots-Tag: noindex, nofollow, noarchive, nosnippet, noimageindex`**
   HTTP response header on every path, set in `vercel.json`. Covers non-HTML
   assets too.
3. **`robots.txt`** with `Disallow: /` (weakest layer — stops crawling, not
   indexing — kept only as a belt-and-braces companion to layers 1 and 2).

When it's time to go live, remove layers 1 and 2 **first** and deploy, then
relax `robots.txt` — never the other order, or crawlers stay blocked from ever
seeing that the noindex is gone.

## Assets

The `bariatric-surgery` page is a faithful copy of the source page's markup with
all first-party asset URLs rewritten to root-relative paths (`/wp-content/...`).
Those asset files (images, CSS, fonts, the hero video — 119 files) are **not yet
in this repo**: the source origin serves them behind an anti-bot wall that blocks
automated download. See `ASSETS_NEEDED.txt` for the exact list of paths.

To finish the page: drop the matching files into the repo root preserving each
path (e.g. `./wp-content/uploads/2025/08/logo.png`). A WordPress media/`wp-content`
export from the source site contains all of them. Until then the page renders
unstyled.

Third-party embeds (Google Tag Manager, Trustindex reviews, the LeadConnector
booking form, WhatsApp widget, Google Maps) load live from their own origins and
need no local files.
