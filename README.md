# WNY Land Development Command Center — V9

Multi-town residential subdivision tracker for Western New York. Tracks 7 towns across Erie & Niagara counties through the full municipal approval process.

## V9 Changes (from V8 PRO)

- **68 duration corrections** across all 7 towns (best/expected/worst refined against municipal code)
- **4 missing tasks added:**
  - Pendleton: USACE Section 404 Permit (p10d) + Highway Access Permit (p10e) → now 35 tasks
  - Wheatfield: USACE Section 404 Permit (w13d) + Highway Access Permit (w13e) → now 40 tasks
- Version references updated throughout

## Task Counts by Town

| Town | Tasks |
|------|-------|
| Amherst | 39 |
| Clarence | 42 |
| Hamburg | 36 |
| Lancaster | 36 |
| Orchard Park | 37 |
| Pendleton | 35 |
| Wheatfield | 40 |
| **Total** | **265** |

## Architecture

```
FCH/
├── index.html       ← Single-file React app (all data + components)
├── server.js        ← Express static server
├── package.json     ← Node dependencies
├── render.yaml      ← Render deployment config
└── README.md
```

## Two-Page Design

### Page 1: Township Tracker (Base)
Select a town → see its Gantt chart, edit tasks inline, track completion, view risks. This is the **main landing page**.

### Page 2: Development Manager
Click "New Development" → create a named project from any town template → get a full project dashboard with:
- Overview stats, phase progress
- Timeline (Gantt) with status cycling
- Task list with 6-state status
- Risk register, milestones, contacts
- Cost estimates, document checklist
- Notes, export, settings
- Compare all 7 towns side-by-side

## Deploy

### GitHub Pages (Static)
Push the repo. Set Pages to deploy from the `main` branch root. The `index.html` serves directly — no build step needed.

### Render (Web Service)
1. Push to GitHub
2. Connect repo to Render as **Web Service**
3. Runtime: **Node**
4. Build command: `npm install`
5. Start command: `npm start`

### Local
```bash
npm install
npm start
# Open http://localhost:3000
```

Or just open `index.html` directly in a browser — no server required for local use.

## Tech Stack
- React 18 (CDN)
- Babel Standalone (CDN, JSX compilation)
- No build tools required
- localStorage for persistence

## Data Sources
Real municipal regulatory data from:
- Amherst: Ch. 204 Subdivision Regulations
- Clarence: Ch. 193 Subdivision of Land (Dual-Board)
- Hamburg: Planning Dept Major Subdivision Review
- Lancaster: §400-38 Subdivisions (Dual-Board, TB Final Authority)
- Orchard Park: Ch. 121 Subdivision of Land (Three 62-Day Clocks)
- Pendleton: Ch. 220 Subdivision of Land (Niagara County)
- Wheatfield: Ch. 169 + §200-45–47 Conservation/Cluster (Niagara County)
