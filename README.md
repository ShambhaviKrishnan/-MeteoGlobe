# 🌍 MeteoGlobe — 3D Weather Intelligence Platform

> A cinematic, futuristic 3D globe-based weather intelligence platform built with Three.js, Chart.js and vanilla JavaScript. No build step. No npm. Just open and run.

<img width="959" height="470" alt="image" src="https://github.com/user-attachments/assets/88c6a5eb-fc17-49d6-9693-19a65d325a59" />

<img width="959" height="464" alt="image" src="https://github.com/user-attachments/assets/40fd15cd-fc8d-404a-8b4e-7d362d1a441d" />

<img width="959" height="470" alt="image" src="https://github.com/user-attachments/assets/09be5af6-74a9-45cd-8875-9c87ab518faa" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d8db75f7-ae70-46a5-8efc-3f8639951b59" />


---

## Preview

A fully interactive 3D Earth with:
- Glowing atmosphere shader
- Pulsing city markers color-coded by temperature
- Animated wind flow lines
- Real-time weather intelligence panels
- 30-day historical + AI-predicted trend charts
- Time Machine slider (±15 days)
- City comparison tool

---

## Project Structure

```
meteoglobe/
│
├── index.html       ← The entire application (single file)
├── README.md             ← This file
│
└── (optional future expansion)
    ├── assets/
    │   └── earth_8k.jpg  ← Drop in a real NASA texture here
    ├── data/
    │   └── cities.json   ← Extend the city database
    └── backend/
        └── server.js     ← API proxy (see Section 7)
```

---

## Quick Start (Zero Setup)

### Method 1 — Double Click (Simplest)
```
1. Download meteoglobe.html
2. Double-click the file
3. Opens in your browser instantly
```
> Some browsers block local file loading of external scripts (CORS). If the globe is blank, use Method 2.

---

### Method 2 — VS Code Live Server (Recommended for Development)

**Step 1 — Install VS Code extension**
```
Open VS Code
Go to Extensions (Ctrl+Shift+X)
Search: "Live Server" by Ritwick Dey
Click Install
```

**Step 2 — Open the project**
```
File → Open Folder → select your meteoglobe/ folder
```

**Step 3 — Launch**
```
Right-click meteoglobe.html in the sidebar
→ "Open with Live Server"

OR click "Go Live" button in the bottom-right status bar
```

Your browser opens at `http://127.0.0.1:5500/meteoglobe.html`

**Step 4 — Edit & see changes instantly**
```
Make any change in meteoglobe.html → Save (Ctrl+S)
Browser auto-refreshes immediately
```

---

### Method 3 — Python Local Server (No extensions needed)
```bash
# Navigate to your project folder
cd path/to/meteoglobe

# Python 3
python -m http.server 8080

# Then open browser at:
http://localhost:8080/meteoglobe.html
```

### Method 4 — Node.js Local Server
```bash
# Install once globally
npm install -g serve

# Run from project folder
serve .

# Open browser at the URL shown (usually http://localhost:3000)
```

---

## How to Use the Application

### Boot Sequence
When you open the app, a cinematic loading screen runs for ~3 seconds initializing all systems. The globe auto-selects **Nagpur, India** (detected as local city) after loading.

---

### 🌐 Globe Navigation

| Action | How |
|--------|-----|
| **Rotate globe** | Click and drag anywhere on the globe |
| **Zoom in/out** | Scroll wheel (mouse) or pinch (touchpad/mobile) |
| **Select a city** | Click any glowing dot on the globe |
| **Hover a city** | Move mouse near a dot → tooltip appears |
| **Auto-rotate** | Globe slowly spins when idle |
| **Reset view** | Click "Reset View" in the left Layers panel |

---

### 🔍 Search

```
Click the search bar at the top center
Type any city name or country (e.g. "Tokyo", "India", "New York")
Click a result → camera flies to that location
Weather panel opens automatically
```

**Available cities:** Tokyo, Mumbai, New York, London, Sydney, Dubai, Paris, São Paulo, Cairo, Moscow, Beijing, Nagpur, Los Angeles, Singapore, Toronto

---

### 🗂 Layer Panel (Left Side)

Click any layer to toggle it on:

| Layer | What it shows |
|-------|--------------|
| **Temperature** | Color-coded heatmap overlay on the globe surface |
| **Wind Flow** | 80 animated wind stream lines across the globe |
| **Rainfall** | Precipitation intensity overlay |
| **Humidity** | Moisture zone visualization |
| **Pressure** | Atmospheric pressure zones |
| **Reset View** | Snaps camera back to default position |
| **Atmosphere** | Toggles the glowing limb atmosphere effect |

---

### 📊 Weather Panel (Right Side)

Opens when you click a city. Contains:

**Top section**
- City name, flag, GPS coordinates
- Storm/heatwave alert banners (if conditions trigger)
- Current temperature, condition, weather icon

**Metrics grid**
- Humidity, Wind speed, Pressure, Feels Like, UV Index, Visibility

**30-Day Temperature Chart**
- Cyan line = past 15 days (historical)
- Purple dashed = next 15 days (AI predicted via linear regression)
- Amber dashed = overall trend line

**Humidity Chart**
- Bar chart showing past (cyan) vs predicted (purple) humidity

**Smart Insights**
- Auto-generated human-readable analysis (heatwave alerts, trend changes, precipitation probability)

**5-Day Forecast**
- Compact day-by-day cards with temperature and condition icon

Close the panel with the ✕ button in the top-right of the panel.

---

### ⏱ Time Machine Slider (Bottom Center)

```
Drag LEFT  → Travel up to 15 days into the past
Drag RIGHT → See AI predictions up to 15 days ahead
CENTER     → Today's data
```

The current date indicator updates as you drag. Temperature values update in real time on the weather panel.

---

### ⊞ City Comparison Tool

```
Click the ⊞ button (bottom left)
→ A panel opens on the right
→ Click up to 4 cities to select them
→ A temperature comparison chart appears automatically
→ Click selected cities again to deselect
```

---

### ☰ Legend

```
Click the ☰ button (bottom left)
→ Shows temperature color scale (-20°C to 40°C+)
→ Shows wind speed scale (0 to 150+ km/h)
```

---

### ⛶ Fullscreen

```
Click the ⛶ button (bottom left)
→ Enters fullscreen mode
→ Click again to exit
```

---

## 🔧 Customization Guide

### Adding More Cities

Find this section in `meteoglobe.html` (around line 100):

```javascript
const CITIES = [
  { name:'Tokyo', country:'Japan', lat:35.68, lon:139.69,
    temp:22, hum:68, wind:18, pres:1012, uv:5, vis:15,
    feels:20, cond:'Partly Cloudy', icon:'🌤', flag:'🇯🇵' },
  // ADD YOUR CITY HERE:
  { name:'Berlin', country:'Germany', lat:52.52, lon:13.40,
    temp:15, hum:65, wind:22, pres:1013, uv:3, vis:16,
    feels:13, cond:'Cloudy', icon:'🌥', flag:'🇩🇪' },
];
```

**Field reference:**

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | City display name |
| `country` | string | Country name |
| `lat` | number | Latitude (-90 to 90) |
| `lon` | number | Longitude (-180 to 180) |
| `temp` | number | Temperature in °C |
| `hum` | number | Humidity % (0–100) |
| `wind` | number | Wind speed km/h |
| `pres` | number | Pressure hPa (typical: 990–1030) |
| `uv` | number | UV Index (0–12) |
| `vis` | number | Visibility in km |
| `feels` | number | Feels-like temperature °C |
| `cond` | string | Weather condition text |
| `icon` | emoji | Weather emoji |
| `flag` | emoji | Country flag emoji |

---

### Connecting a Real Weather API

Replace the static city data with live API calls. Here's the pattern using **OpenWeatherMap** (free tier):

**Step 1 — Get a free API key**
```
https://openweathermap.org/api
Sign up → API Keys → copy your key
```

**Step 2 — Replace the data loader**

Find the `selectCity` function and add before it:

```javascript
const OWM_KEY = 'YOUR_API_KEY_HERE';

async function fetchLiveWeather(lat, lon) {
  const url = `https://api.openweathermap.org/data/2.5/weather`
    + `?lat=${lat}&lon=${lon}&appid=${OWM_KEY}&units=metric`;
  const res = await fetch(url);
  const d = await res.json();
  return {
    temp:    Math.round(d.main.temp),
    hum:     d.main.humidity,
    wind:    Math.round(d.wind.speed * 3.6), // m/s → km/h
    pres:    d.main.pressure,
    feels:   Math.round(d.main.feels_like),
    vis:     Math.round((d.visibility || 10000) / 1000),
    cond:    d.weather[0].description,
    uv:      0, // needs separate UV endpoint
  };
}
```

**Step 3 — Call it in selectCity**

```javascript
async function selectCity(city) {
  const live = await fetchLiveWeather(city.lat, city.lon);
  Object.assign(city, live); // merge live data in
  // ... rest of function unchanged
}
```

---

### Changing the Default City on Load

Find this block near the bottom:

```javascript
// Auto-select user's city (Nagpur)
setTimeout(()=>{
  const nagpur = CITIES.find(c=>c.name==='Nagpur');
  if(nagpur) selectCity(nagpur);
}, 1500);
```

Change `'Nagpur'` to any city name in your CITIES array.

---

### Changing Color Themes

The entire color system uses CSS variables at the top of the file:

```css
:root {
  --navy:   #020b18;    /* background base */
  --cyan:   #00f5ff;    /* primary accent */
  --purple: #7c3aed;    /* secondary accent */
  --blue:   #1d6bfa;    /* tertiary */
  /* change these to shift the entire theme */
}
```

**Green tech theme example:**
```css
--cyan:   #00ff88;
--purple: #00cc44;
```

**Red mars theme example:**
```css
--cyan:   #ff4444;
--purple: #ff8800;
--navy:   #180800;
```

---

## Architecture Overview

```
meteoglobe.html
│
├── <style>              CSS variables, glassmorphism, animations
│
├── HTML Structure
│   ├── #loader          Boot sequence screen
│   ├── #particles       Background particle canvas
│   ├── #globe-canvas    Three.js render target
│   ├── #header          Logo + clock + status
│   ├── #search-wrap     Search bar + dropdown
│   ├── #layer-panel     Left: layer toggles
│   ├── #weather-panel   Right: full weather data
│   ├── #timeline-panel  Bottom: time machine
│   ├── #mini-tools      Bottom-left: utility buttons
│   ├── #compare-panel   City comparison overlay
│   └── #legend          Color scale reference
│
└── <script>
    ├── DATA ENGINE       City data, time series generation,
    │                     moving average, linear regression,
    │                     insight generation, alert detection
    │
    ├── GLOBE ENGINE      Three.js scene setup, procedural
    │                     Earth texture, atmosphere shader,
    │                     star field, city markers, wind tubes
    │
    ├── INTERACTION       Mouse/touch drag, scroll zoom,
    │                     raycasting, hover tooltips, click-select
    │
    ├── WEATHER PANEL     City selection, data binding,
    │                     Chart.js rendering, forecast cards
    │
    ├── LAYER SYSTEM      Toggle visibility of globe overlays
    │
    ├── TIMELINE          Date slider, data adjustment
    │
    ├── SEARCH            Fuzzy match, camera fly-to
    │
    ├── COMPARE           Multi-city chart comparison
    │
    └── BOOT              Loading sequence, auto-select, clock
```

---

## Dependencies (All via CDN — no installation needed)

| Library | Version | Purpose |
|---------|---------|---------|
| [Three.js](https://threejs.org) | r128 | 3D globe rendering, shaders, raycasting |
| [Chart.js](https://chartjs.org) | 4.4.0 | Temperature, humidity, comparison charts |
| [Google Fonts](https://fonts.google.com) | — | Orbitron, Rajdhani, JetBrains Mono |

No npm. No webpack. No React. No build pipeline.

---

## Roadmap — What to Build Next

### Level 1 (Easy additions)
- [ ] Add 50+ more cities
- [ ] Download weather data as CSV
- [ ] Share button (copy city URL to clipboard)
- [ ] Keyboard shortcut: `R` to reset, `Esc` to close panel

### Level 2 (Moderate)
- [ ] Connect OpenWeatherMap API (see customization guide above)
- [ ] Real country boundary overlay from GeoJSON
- [ ] NASA 8K Earth texture (`earth_daymap.jpg`)
- [ ] Mobile-optimized touch gestures

### Level 3 (Advanced)
- [ ] Express.js backend to proxy and cache API calls
- [ ] MongoDB to store 30-day historical data
- [ ] Python FastAPI ML service for weather prediction
- [ ] WebSocket for live data push every 60 seconds
- [ ] User accounts to save favorite cities
- [ ] Export weather report as PDF

---

## Troubleshooting

**Globe is black / not showing**
```
→ Use Live Server or a local server (Methods 2–4 above)
→ Do NOT open the file directly via file:// in Chrome
```

**Charts not rendering**
```
→ Check browser console (F12 → Console tab)
→ Ensure you have internet (Chart.js loads from CDN)
```

**Fonts look wrong**
```
→ Fonts load from Google Fonts CDN
→ Needs internet connection
→ Fallbacks: system monospace fonts will appear offline
```

**Globe rotation is choppy**
```
→ Enable hardware acceleration in your browser
→ Chrome: Settings → System → "Use hardware acceleration when available" ✓
```

**Search not finding a city**
```
→ Only 15 cities are currently in the database
→ Add more cities following the customization guide above
```

---

## 📄 License

MIT License — free to use, modify, and deploy for personal and commercial projects.

---

## 👤 Author

Built with Three.js, Chart.js and pure obsession.  
Designed as a premium portfolio project.

---

## ⭐ If you found this useful

Star the repo on GitHub — it helps others find it!

```
https://github.com/ShambhaviKrishnan/-MeteoGlobe

```
