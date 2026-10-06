# Building Energy Bills

A single-page tool that turns the monthly gas and electric meter readings into four bills: the whole building, Victor (gas), Banner Place (electric) and Holly's share.

Plain HTML, CSS and JavaScript. No build step and no dependencies.

## Files

- `index.html` - the app (all logic is in the inline script)
- `manifest.webmanifest`, `icon*.png`, `apple-touch-icon.png` - home-screen install
- `sw.js` - service worker for offline use

## Deploy on GitHub Pages

1. Create a repository and push these files to the root of `main`.
2. Repository Settings > Pages > Build and deployment > Deploy from a branch > `main` / `(root)`.
3. The site appears at `https://<user>.github.io/<repo>/` after a minute.

Pages sites are public. For a private URL, use a private repo on a paid plan, or host on Cloudflare Pages behind Cloudflare Access.

## Install on a phone

- iPhone (Safari): Share > Add to Home Screen
- Android (Chrome): menu > Install app

Open it from the same URL every time. Saved months and rates live in that browser's `localStorage`, so they are per device and per address.

## Changing rates

Rates, VAT, gas conversion factors and the standing-charge split are editable in the page under "Rates and settings". Defaults are in `DEF_RATES` at the top of the script.

## Updating

Push a change, then bump `CACHE` in `sw.js` (for example `energy-bills-v2`) so installed copies pick it up.

## Calculation

- Gas kWh = units x 1.022264 x 39.2 / 3.6, rounded to a whole number
- Each bill line is rounded to the penny: usage, standing charge (days x daily rate), climate change levy (kWh x 0.775p), then VAT on the subtotal
- Victor and Banner Place pay the full usage and levy on their sub-meter plus half the standing charge
- Holly's share is the main bill minus the sub bills, line by line
