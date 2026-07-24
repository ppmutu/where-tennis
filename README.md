# Where to — Tennis Finder

A tiny static webapp for you and your friend to find tennis **courts** and
**simulators**: search/filter them, see them on a map, and add new ones.

## Files

- `index.html` — the whole app (Find / Map / Add tabs)
- `tokens.css` — design tokens (colour, type, spacing, motion) used by `index.html`
- `places.json` — the single source of data (edit this to change what everyone sees)
- `config.js` — your Google Maps API key and default map center
- `README.md` — this file

## Run it locally

The app loads `places.json` with `fetch`, so it must be served over HTTP —
double-clicking `index.html` won't work (browsers block local file reads).

From this folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000 . (Any static server works — e.g. `npx serve`.)

## Add your Google Maps key

1. In Google Cloud Console, enable **Maps JavaScript API** and **Geocoding API**, and turn on billing.
2. Open `config.js` and replace `YOUR_GOOGLE_MAPS_API_KEY` with your key.

The **Find** list works without a key; only the **Map** tab and the address
"Locate" button need it. Restrict the key to your site's domain in the console.

## How data works (important)

This is a **static app** — there's no server. `places.json` is the shared truth.

- The **Add** tab lets you fill in a place, set its location (type an address →
  **Locate**, or click the map, or drag the pin), and **Add to list**. That adds
  it in your browser only.
- To share it with your friend, click **Download places.json** and replace the
  `places.json` in your shared copy (e.g. commit it to the repo / re-upload to
  your host). Next load, you both see it.
- **Copy this entry** copies just the one new record's JSON if you'd rather paste
  it into `places.json` by hand.

## Editing places.json by hand

Each record:

```json
{
  "id": "unique-id",
  "name": "Venue name",
  "type": "court",            // "court" or "simulator"
  "surface": "hard",          // optional
  "indoor": false,
  "area": "District, City",
  "address": "Full address",
  "lat": 13.7563,
  "lng": 100.5018,
  "booking": {
    "channel": "line",        // line | phone | website | app | facebook | other
    "label": "Book via LINE",
    "value": "https://line.me/..."   // URL, or phone number for channel "phone"
  },
  "notes": "Price, hours, tips"
}
```

The two entries currently in `places.json` are clearly-labeled **EXAMPLES** —
replace them with real venues.

## Deploying (optional)

Push the folder to any static host (GitHub Pages, Netlify, Cloudflare Pages).
Both of you open the same URL; whoever updates `places.json` on the host updates
it for both.

## Known limits

- No live shared writes (by design — it's static). Sharing new entries means
  replacing `places.json`.
- The Map tab requires a valid Google Maps API key.
