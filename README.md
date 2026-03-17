# ZamWboys — Africa & Europe Trip Planner 🌍

An interactive trip planning map for Europe and Africa. Add cities, draw routes, and plan your adventure.

## Features

- **Search** for any city or location (powered by OpenStreetMap)
- **Double-click** anywhere on the map to drop a pin
- **Ordered route** with numbered markers and connecting lines
- **Distance estimates** between stops
- **Drag to reorder** stops in the sidebar
- **Share** your trip via URL — anyone with the link sees the same route
- **Live collaboration** — multiple people can add/remove stops in real-time (requires Firebase setup)
- **Export** — print to PDF for a saved map image

---

## Using without setup (local-only)

Just open `index.html` in a browser or deploy to GitHub Pages. Works immediately — routes are saved in browser local storage per trip code.

> The trip code in the URL (`#abc1234`) is what separates different trips.

---

## Setting up Firebase (for real-time collaboration)

This lets your friends open the same URL and edit the route together live.

### 1. Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → name it `zamwboys` → Create
3. In the left panel: **Build → Realtime Database**
4. Click **Create Database** → choose a region → **Start in test mode** → Enable

### 2. Get your web app credentials

1. Go to **Project Settings** (gear icon) → **Your apps** tab
2. Click **Add app** → choose **Web** (`</>`)
3. Register the app → copy the `firebaseConfig` object

### 3. Paste config into index.html

Open `index.html` and find this section near the bottom:

```js
const FIREBASE_CONFIG = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  databaseURL:       "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
  ...
};
```

Replace the placeholder values with your actual config. Save the file.

### 4. Deploy to GitHub Pages

1. Push to GitHub
2. Go to repo **Settings → Pages**
3. Source: `main` branch, `/ (root)`
4. Your map is live at `https://yourusername.github.io/zamwboys/`

Share the URL (including the `#tripcode`) with your friends — everyone on the same URL edits the same route in real-time.

---

## How to use

| Action | How |
|--------|-----|
| Add a stop | Type in the search bar and click a result |
| Add by clicking | Double-click anywhere on the map |
| Remove a stop | Click `×` on any stop card |
| Reorder stops | Drag stop cards up/down |
| Pan to a stop | Click the stop card |
| Share trip | Click **Share** — copies URL to clipboard |
| Save as image | Click **Export** → Print → Save as PDF |

---

## Tech stack

- [Leaflet.js](https://leafletjs.com/) — map rendering
- [CartoDB Dark Matter](https://carto.com/basemaps/) — map tiles
- [OpenStreetMap Nominatim](https://nominatim.org/) — location search
- [Firebase Realtime Database](https://firebase.google.com/) — collaboration (optional)
- [SortableJS](https://sortablejs.github.io/Sortable/) — drag-and-drop
