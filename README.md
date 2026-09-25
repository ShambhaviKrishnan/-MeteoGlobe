# 🌍 MeteoGlobe — 3D Weather Intelligence Platform

A 3D globe-based weather visualization platform built with Three.js, Chart.js and vanilla JavaScript. No build step, no npm — just open and run.

## Screenshots

<img width="959" height="470" alt="image" src="https://github.com/user-attachments/assets/88c6a5eb-fc17-49d6-9693-19a65d325a59" />

<img width="959" height="464" alt="image" src="https://github.com/user-attachments/assets/40fd15cd-fc8d-404a-8b4e-7d362d1a441d" />

<img width="959" height="470" alt="image" src="https://github.com/user-attachments/assets/09be5af6-74a9-45cd-8875-9c87ab518faa" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d8db75f7-ae70-46a5-8efc-3f8639951b59" />

---

## Overview

An interactive 3D Earth with city-wise weather data, including:

Pulsing city markers color-coded by temperature
Animated wind flow lines
Weather detail panels per city
30-day historical trend charts with a short-term forecast (linear regression)
Time Machine slider (±15 days)
City comparison tool (up to 4 cities)

Note on data: The app ships with a static dataset of 15 cities for demo purposes. It's built so a real weather API (e.g. OpenWeatherMap) can be plugged in — see Connecting a Real Weather API below. The trend forecast uses linear regression and a moving average on the sample data, not a trained ML model.

---

## Project Structure

```
meteoglobe/
│
├── index.html       ← The entire application (single file)
├── README.md             ← This file
└── 
```

---

## Quick Start (Zero Setup)

### Method 1 — Double Click 

```
1. Download meteoglobe.html
2. Double-click to open in your browser
```

Some browsers block local file loading of external scripts (CORS). If the globe is blank, use Method 2.

---

### Method 2 — Python Local Server

```bash
cd path/to/meteoglobe
python -m http.server 8080
```

Then open:

```
http://localhost:8080/meteoglobe.html
```

---

## How to Use the Application

Globe navigation: click-drag to rotate, scroll/pinch to zoom, click a city marker to select it, globe auto-rotates when idle.

Search: search bar at top center — type a city or country name, click a result to fly there. 15 cities available (Tokyo, Mumbai, New York, London, Sydney, Dubai, Paris, São Paulo, Cairo, Moscow, Beijing, Nagpur, Los Angeles, Singapore, Toronto).

Layer panel (left): toggle Temperature, Wind Flow, Rainfall, Humidity, Pressure, and Atmosphere overlays.

Weather panel (right): opens on city click — current conditions, metrics (humidity, wind, pressure, UV, visibility), 30-day temperature/humidity charts, auto-generated insights, and a 5-day forecast.

Time Machine (bottom center): drag to view ±15 days of data relative to today.

Compare tool: select up to 4 cities to see a temperature comparison chart.

---

# Architecture

Single self-contained HTML file, organized into:

Data engine — city data, time-series generation, moving average, linear regression forecast, insight/alert generation
Globe engine — Three.js scene, procedural Earth texture, atmosphere shader, star field, city markers, wind lines
Interaction layer — drag/zoom, raycasting for click-select, hover tooltips
Weather panel — city data binding, Chart.js rendering, forecast cards
Layer system, timeline, search, compare — supporting UI modules

---

# Customization

## Adding a city

Edit the CITIES array (near the top of meteoglobe.html):

```javascript
{ name:'Berlin', country:'Germany', lat:52.52, lon:13.40,
  temp:15, hum:65, wind:22, pres:1013, uv:3, vis:16,
  feels:13, cond:'Cloudy', icon:'🌥', flag:'🇩🇪' }
```

---
## Connecting a Real Weather API

Replace static data with live calls, e.g. using OpenWeatherMap:

```javascript
const OWM_KEY = 'YOUR_API_KEY_HERE';

async function fetchLiveWeather(lat, lon) {
  const url = `https://api.openweathermap.org/data/2.5/weather`
    + `?lat=${lat}&lon=${lon}&appid=${OWM_KEY}&units=metric`;
  const res = await fetch(url);
  const d = await res.json();
  return {
    temp: Math.round(d.main.temp),
    hum: d.main.humidity,
    wind: Math.round(d.wind.speed * 3.6),
    pres: d.main.pressure,
    feels: Math.round(d.main.feels_like),
    vis: Math.round((d.visibility || 10000) / 1000),
    cond: d.weather[0].description,
  };
}
```

Call this inside selectCity() and merge the result into the city object before rendering.

---

# Color theme

Edit the CSS variables at the top of the file (--navy, --cyan, --purple, --blue) to change the entire theme.

---

# Dependencies (via CDN, no installation)
Library	Version	Purpose
Three.js	r128	3D globe rendering, shaders, raycasting
Chart.js	4.4.0	Charts
Google Fonts	—	Orbitron, Rajdhani, JetBrains Mono

---

# Roadmap
- [ ] Connect OpenWeatherMap API
- [ ] Add more cities
- [ ] Express.js backend
- [ ] MongoDB historical storage
- [ ] Mobile optimization

---

# Troubleshooting

### Globe is black

Use a local server instead of opening with `file://`.

### Charts are missing

Check that:

- Internet connection is available
- Chart.js CDN loads successfully

### Search returns nothing

Only 15 cities are included by default.

---

# License

MIT License.

---

# Author

**Shambhavi Krishnan**

github.com/ShambhaviKrishnan/-MeteoGlobe

---










#
