# HR Data Intelligence Workbench -- deployment

This folder (`index.html` + `assets/`) is the complete, self-contained static
application. It is 100% client-side: once the page loads in a browser, no
further network requests are made, and no HR data is ever transmitted
anywhere. Everything -- parsing, normalization, validation, metrics, the
local metric library, and data storage -- happens in the browser using
IndexedDB.

## How to deploy

Any static file host works. A few common options:

- **Netlify / Vercel**: drag-and-drop this folder (or connect a repo and
  point the build output at it).
- **GitHub Pages**: push this folder's contents to a `gh-pages` branch (or
  the `docs/` folder of a repo) and enable Pages in repo settings.
- **Internal web server / S3 + static hosting**: copy `index.html` and
  `assets/` to the web root as-is. No server-side code, database, or
  environment variables are required.

Because the app uses client-side routing only within a single page (no
routes to configure) and relative asset paths, it should work unmodified
from any subdirectory or root path.

## Browser support

Built and tested against current Chrome. Should also work in current Edge
and Firefox (per the spec's requirement) since it uses only standard
IndexedDB, File, and Canvas APIs -- but it's worth a quick smoke test in
whichever browsers your HR team actually uses before wide rollout.

## Data lifecycle note for IT / support

Loaded data lives in each person's browser's IndexedDB storage under this
site's origin. Clearing browser data/history for the site will also clear
their loaded HR data (this is expected and documented in-app). There is no
server-side data to back up, migrate, or worry about -- each person's
browser is an independent instance of the tool.
