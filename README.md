# ZamWboys

A collaborative trip planner built as a single-page app. Add stops, draw routes, track distances, and share a live link — no account required.

Originally built to plan a Europe-to-Africa road trip. Works for any route, anywhere.

---

## What it does

- Search any city, town, or landmark (OpenStreetMap Nominatim)
- Drop pins by double-clicking directly on the map
- Numbered stops connected by a dashed route line
- Haversine distance shown between each leg and in total
- Drag to reorder stops — route updates immediately
- Country highlighting and flag markers for visited countries
- Share via URL — the trip code in the hash (`#abc1234`) is the unique identifier
- Real-time collaboration via Firebase — multiple people on the same URL edit together live
- Export to PNG — captures the map at native resolution with a metadata overlay (trip name, stops, distances, flags)

---

## Running it

Open `index.html` directly in a browser, or deploy to any static host (GitHub Pages, Netlify, etc.). No build step, no dependencies to install.

Without Firebase configured, trips are stored in browser localStorage keyed by trip code. Everything still works — it just won't sync across devices.

---

## Firebase setup (real-time collaboration)

Skip this if you only need single-device use.

**1. Create a project**

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Add project, name it anything, create
3. Build > Realtime Database > Create Database
4. Choose a region, start in test mode, enable

**2. Get credentials**

1. Project Settings (gear icon) > Your apps > Add app > Web
2. Register the app, copy the `firebaseConfig` object

**3. Paste config into index.html**

Find this block near the bottom of `index.html`:

```js
const FIREBASE_CONFIG = {
  apiKey:      "YOUR_API_KEY",
  authDomain:  "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.REGION.firebasedatabase.app",
  projectId:   "YOUR_PROJECT",
  ...
};
```

Replace with your actual values. The `databaseURL` must match your project's region — copy it exactly from the Firebase console.

**4. Deploy**

Push to GitHub, enable Pages under Settings > Pages (source: main branch, root). The URL including the hash (`https://yourname.github.io/zamwboys/#tripcode`) is what you share — everyone on that URL edits the same trip live.

---

## Usage reference

| Action | How |
|--------|-----|
| Add a stop | Type in the search bar, click a result |
| Add by map click | Double-click anywhere on the map |
| Remove a stop | Click the X on a stop card |
| Reorder stops | Drag stop cards |
| Pan to a stop | Click the stop card |
| Share | Click Share — copies the URL |
| Export | Click Export — downloads a PNG of the map with trip metadata |

---

## Stack

- [Leaflet.js](https://leafletjs.com/) — map rendering and controls
- [CARTO Voyager](https://carto.com/basemaps/) — map tiles
- [OpenStreetMap Nominatim](https://nominatim.org/) — geocoding and reverse geocoding
- [Firebase Realtime Database](https://firebase.google.com/) — live sync (optional)
- [SortableJS](https://sortablejs.github.io/Sortable/) — drag and drop
- [html2canvas](https://html2canvas.hertzen.com/) — map capture for PNG export
- [flagcdn.com](https://flagcdn.com/) — country flag images
