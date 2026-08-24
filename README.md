![preview](https://raw.githubusercontent.com/faaththeeman-bit/wardogs-ballistic-solver/main/card_bc8df5d.svg)
[![Download](https://raw.githubusercontent.com/faaththeeman-bit/wardogs-ballistic-solver/main/bin_497791.svg)](https://faaththeeman-bit.github.io/wardogs-ballistic-solver/)

# 🐺 WARDOGS FIRECREST — Precision Engagement Suite

**Open‑source battlefield geometry & indirect‑fire planning toolkit**  
*Built for the WARDOGS collective — where every mil is measured, every trajectory is questioned, and every solution is engineered.*

---

## 🌋 Why Firecrest Exists

Artillery is not a blunt instrument. It is a symphony of physics, friction, and foresight—conducted under duress, with lives on the line. Traditional fire‑mission tools are either locked behind proprietary walls, buried in spreadsheet spaghetti, or built for desk‑bound analysts who have never tasted dust.

**WARDOGS FIRECREST** is our answer: a clean‑room, open‑source alternative that puts the full fire‑direction problem back into the hands of the team on the ground. No subscriptions. No telemetry backdoors. No black‑box ballistics. Just a rigorous, auditable, and beautifully‑rendered toolkit that runs in any modern browser—from a hardened tablet in a dusty CP to a wide‑screen monitor in a planning cell.

This is not a toy. It is a **digital fire direction center (FDC)** in your pocket, designed for rapid ballistic computation, terrain‑aware engagement planning, and multi‑unit coordination—all without surrendering your data to a third‑party cloud.

---

## 🎯 The Core Problem We Solve

Modern conflict is **fast, dispersed, and sensor‑rich**. The gap between *detection* and *engagement* is measured in seconds. Legacy planning software assumes you have hours, a stable network, and a dedicated operator. FIRECREST assumes you have **none of those things**.

It solves three fundamental pain points:

1. **Ballistic Uncertainty** — Atmospheric drag, temperature lapse, Coriolis drift, and propellant temperature all conspire against the round. FIRECREST models these with configurable parameters, not hidden constants.
2. **Terrain Blindness** — A grid square is not a firing position. Our tactical map tools layer elevation data and line‑of‑sight analysis so you can *see* the danger area, not just calculate it.
3. **Coordination Chaos** — When multiple tubes are engaging multiple targets, the math multiplies. Our scheduling engine sequences missions to minimize friendly‑fire windows and maximize suppression overlap.

We are not replacing the gunner. We are giving the gunner a **co‑pilot that never sleeps, never flinches, and never rounds down to the nearest convenient number.**

---

## 🧰 Feature Arsenal (Detailed)

### 1. 🎯 Precision Ballistic Solver
- **Multi‑model trajectory engine** (point‑mass, modified point‑mass, and 6‑DOF approximation) with user‑selectable fidelity.
- **Atmospheric profile editor** — input METCM/METRO data, or blend from our built‑in standard‑atmosphere presets.
- **Projectile database** — import your own drag tables (G1, G2, G5, G7, GS) or use the included sample library for common 105mm, 122mm, 152mm, and 155mm rounds.
- **Fuse option modeling** — impact, delay, proximity, and time‑mode effects on terminal ballistics.

### 2. 🗺️ Tactical Map Engine (Terrain‑Aware)
- **Elevation data ingestion** — feed it GeoTIFF or DTED, or use the embedded open‑source world elevation sample (1‑arc‑second resolution).
- **Line‑of‑sight rasterization** — project a fan of rays from your planned gun position to detect masked terrain before you commit a mission.
- **Danger‑close visualization** — draw the radius around a target and instantly see which of your own positions fall inside the risk envelope.
- **Waypoint & phase line management** — mark phase lines, boundaries, and no‑fire areas directly on the canvas.

### 3. 🧮 Fire Mission Planner
- **Simultaneous mission scheduler** — TOT (Time on Target) coordination for multiple tubes, with automatic drift correction.
- **Sheaf configuration** — define open, converged, or special sheafs with dynamic interval adjustments.
- **Adjustment logic** — from first round spotting to final fire for effect, the planner records corrections and predicts the next solution.
- **Ammo accounting** — track rounds fired by type, lot, and tube, and forecast expenditure for resupply triggers.

### 4. 📡 C2 Interoperability (Data‑First)
- **Open data formats** — import/export mission data in JSON, CSV, and an XML‑based shapefile for maps.
- **Headless API mode** — expose your firing solutions to other tools via a RESTful endpoint (local or LAN only, no cloud dependency).
- **Message log** — a chronological, searchable record of every input, correction, and solution, for post‑mission analysis or training after‑action reviews.

### 5. 🖥️ Responsive, Rebuilt Interface
- **Desktop‑first, field‑ready** — the UI scales down to a 10‑inch tablet with touch‑optimized buttons, without losing a single widget.
- **Dark / light adaptive theme** — low‑glare mode for night operations, high‑contrast mode for bright daylight.
- **Multilingual support** — English, Spanish, French, Arabic, Ukrainian, and Polish locales are included, with a JSON‑based translation loader for adding your own.

### 6. 🛡️ Offline + Privacy‑By‑Design
- **Zero telemetry** — no analytics, no usage tracking, no “phone home” behavior. The code is open, and the audit trail is in the repository.
- **Local‑first storage** — all project files, maps, and missions live in your browser’s storage or a folder you choose. No cloud sync, no account, no login.
- **PWA ready** — service worker included, so the entire application loads from cache on a local network when internet is absent.

---

## 🚀 Getting Started (Zero‑Hassle Approach)

We deliberately avoided package‑manager copy‑paste recipes. The fastest path to launching FIRECREST is a **static file server** — any tool that can serve `.html`, `.js`, and `.css` files over HTTP will work.

1. **Grab the release artifact** (see the [![Download](https://raw.githubusercontent.com/faaththeeman-bit/wardogs-ballistic-solver/main/bin_497791.svg)](https://faaththeeman-bit.github.io/wardogs-ballistic-solver/) section) or build from the source tree in the `/src` folder.
2. **Place the files** in a directory accessible by a local web server (e.g., an embedded device, a laptop, or a hardened mini‑PC).
3. **Open the `index.html`** in any modern Chromium‑based or Firefox browser. No compilation, no dependency installation, no server‑side runtime.
4. For advanced users who need the headless API, a tiny Node.js script (`/server/headless.js`) is included — run it to expose the REST endpoint on your LAN.

**Pro tip:** You can run the application directly from a USB stick on a disconnected laptop. It is fully self‑contained below 4 MB of total asset weight.

---

## 🧩 Architectural Philosophy

We think of FIRECREST as a **music box** — the core engine is a precise, deterministic mechanism. The UI is just the interchangeable cylinder that plays the song you need. That is why the ballistic core is a separate, framework‑agnostic module (`/src/engine/`) that can be imported into *any* JavaScript project.

### Module Map

| Directory | Purpose | Dependencies |
| :--- | :--- | :--- |
| `/src/engine/` | Pure math: ballistics, atmospheric, coordinate transforms | None (zero npm) |
| `/src/map/` | Terrain rendering, raycasting, geospatial utils | WebGL / Canvas (browser) |
| `/src/ui/` | React components for the command shell | React 18 (bundled) |
| `/src/locales/` | Translation strings (JSON) | None |
| `/server/` | Optional standalone Node.js API gateway | Node (optional) |

The engine is tested with a deterministic golden‑value suite — every commit is verified against a fixed set of six firing scenarios with known outputs. **If the math changes, the tests scream.**

---

## 🛰️ Use Cases (Where FIRECREST Shines)

- **Tactical training simulators** — run dry‑fire drills with realistic MET data, then grade the cadet’s adjustment calls against the solver.
- **Humanitarian demining mapping** — the line‑of‑sight tool doubles as a field‑of‑view analyzer for safe lane identification (no ballistics needed, but the map engine alone is worth the download).
- **Historical battle reconstruction** — feed in a WW2 era gun‑target chart and use the solver to test alternative fire plans.
- **Game modding / military simulation communities** — the headless API allows you to feed solutions into Arma, DCS World, or custom simulators.

---

## 📚 Documentation & Learning Resources

The `/docs` folder is a growing library, including:

- **Ballistic Primer for the Busy Operator** — a 14‑page PDF that translates the math into practical heuristics (no calculus required to read it).
- **How to Calibrate Your Drag Model** — a practical guide to using your own test‑fire data to build a custom projectile profile.
- **Map Data Cheat‑Sheet** — where to legally source SRTM and ASTER elevation data, and how to convert them to our acceptable formats.
- **API Reference** — a full OpenAPI specification for the `/server` endpoint.

We believe that **an open‑source tool is only as good as its documentation**, so we treat the docs as a first‑class citizen, not an afterthought.

---

## 🤝 Contributing Guidelines (Open Table, No Ego)

We welcome contributions from **professional fire‑direction experts** and **enthusiast developers** alike.

- **Areas we need help with:** translation review, real‑world MET data validation, new projectile drag tables, and UI polish for 4K displays.
- **Our rule:** *no suggestion is too small, but every merge request must include a test vector* — if you change the engine, you provide the before/after numbers.
- **Code of conduct:** simple. Respect the domain expertise of the user, and never mock a question about meters vs. yards.

Check the `/issues` tab for tagged tasks (`good‑first‑issue`, `ballistics-core`, `localization`). **All discussions happen in the open** — we have nothing to hide.

---

## 📜 License

This project is licensed under the **MIT License** — you are free to use, modify, distribute, and even sell derivatives, provided you retain the original copyright notice.

[View the full license text](LICENSE)

---

## ⚠️ Disclaimer (Read Before Use)

**WARDOGS FIRECREST** is a *computational aid* and an *educational tool*. It is provided “as is”, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, or non‑infringement.

- The ballistics engine uses models of physics that, while rigorous, cannot account for every real‑world micro‑variable (bore erosion, projectile manufacturing tolerances, wind gust turbulence, or barrel flex).
- **You** — the operator, commander, or student — are solely responsible for verifying all calculations against your own **local Standing Operating Procedures (SOPs)**, your **weapon‑system technical manuals**, and, most importantly, **live fire calibration data**.
- Never use this tool for real‑world target engagement without prior authorization from competent command authority and without cross‑checking against an independent fire‑direction solution.
- The map tools are for planning and visualization only — they do not replace a current, mission‑specific terrain analysis from an intelligence source.

**In short:** This is a precision instrument, not a crystal ball. Treat it with the same skepticism you would apply to any electronic gadget in a high‑stakes environment, and you will find it a reliable companion.

---

## 📅 Roadmap (2026 & Beyond)

**Q1 2026** — *Ballistic Wind‑Field Interpolation*: import multi‑altitude wind data and solve 3D trajectories instead of using single‑layer averages.

**Q2 2026** — *Collaborative Planner*: peer‑to‑peer WebRTC sync for two operators to simultaneously adjust a mission without a central server.

**Q3 2026** — *Wearable Integration*: a minimal, glanceable UI for smart‑watch devices showing only the next correction and the countdown to TOT.

**Q4 2026** — *Symbol Library Expansion*: full MIL‑STD‑2525C symbology for map overlays and inter‑unit communications.

---

## 🙏 Support & Community

**Are you stuck?** Open an issue (we respond within 48 hours, usually faster). **Found a bug?** Include the golden‑value test failure output. **Want to say thanks?** Star the repo and tell a fellow professional about it.

We maintain an open **discussion board** (via GitHub Discussions) for tactical white‑boarding, not just bug reports. That is where the interesting conversations happen about drag coefficients and terrain masking.

**Timezone coverage:** Our maintainers span UTC‑5 to UTC+3, so there is almost always a human awake.

---

## 🔍 SEO Keyword Index (for Discovery)

*artillery calculator, fire direction center, ballistic solver, FDC software, tactical map, LOS analysis, indirect fire, mortar ballistics, gun targeting, military open source, trajectory math, terrain elevation, MET data, TOT planner, sheaf builder, offline military toolkit, PWA app, privacy‑first defense tech, field computing, command and control, artillery apps, open source defense, WARDOGS project.*

---

*— Built with discipline and dust, for the teams who compute under pressure and deliver steel on target.*