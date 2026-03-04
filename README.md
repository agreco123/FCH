# WNY Land Development Command Center — V8 PRO

Multi-town residential subdivision tracker for Western New York. Tracks 7 towns across Erie & Niagara counties through the full municipal approval process.

## Architecture

```
wny-v8-pro/
├── public/
│   └── index.html          ← Deployed HTML (built by build.sh)
├── src/
│   ├── data/
│   │   ├── phases.js       ← Phase colors, statuses (~1KB)
│   │   ├── amherst.js      ← 39 tasks (~5KB)
│   │   ├── clarence.js     ← 42 tasks (~7KB)
│   │   ├── hamburg.js      ← 36 tasks (~6KB)
│   │   ├── lancaster.js    ← 36 tasks (~6KB)
│   │   ├── orchardpark.js  ← 37 tasks (~7KB)
│   │   ├── pendleton.js    ← 33 tasks (~6KB)
│   │   ├── wheatfield.js   ← 38 tasks (~6KB)
│   │   ├── towns.js        ← TOWNS config object (~3KB)
│   │   └── reference.js    ← Costs, docs, contacts (~4KB)
│   ├── components/
│   │   └── shared.js       ← InlineEdit, PhaseSelect, StatusButton (~4KB)
│   ├── views/
│   │   ├── tracker.js      ← BASE: Township tracker (V6 core) (~15KB)
│   │   └── dev-manager.js  ← NEW: Development management dashboard (~12KB)
│   ├── utils.js            ← computeSchedule, storage, dates (~2KB)
│   └── app.js              ← Root App component, routing (~5KB)
├── scripts/
│   └── build.sh            ← Concatenates src/ into public/index.html
├── render.yaml             ← Render deployment config
└── README.md
```

## Two-Page Design

### Page 1: Township Tracker (Base)
The original V6 tracker. Select a town → see its Gantt chart, edit tasks inline, track completion, view risks. This is the **main landing page**.

### Page 2: Development Manager (New)  
Click "New Development" → create a named project from any town template → get a full project dashboard with:
- Overview stats, phase progress
- Timeline (Gantt) with status cycling
- Task list with 6-state status
- Risk register, milestones, contacts
- Cost estimates, document checklist
- Notes, export, settings
- Compare all 7 towns side-by-side

## Build & Deploy

### Local Development
```bash
npm install
npm run build
npm start
# Open http://localhost:3000
```

### Deploy to Render (Web Service)
1. Push to GitHub
2. Connect repo to Render as **Web Service**
3. Runtime: **Node**
4. Build command: `npm install && npm run build`
5. Start command: `npm start`
6. Publish directory: *(leave blank)*

### Deploy to GitHub Pages
1. Run `npm run build` locally
2. Push the `public/` folder to GitHub Pages

## Tech Stack
- React 18 (CDN)
- Babel Standalone (CDN, JSX compilation)
- No build tools required beyond `cat`
- localStorage for persistence
- Opens directly in any browser

## Data Sources
Real municipal regulatory data from:
- Amherst: Ch. 204 Subdivision Regulations
- Clarence: Ch. 193 Subdivision of Land (Dual-Board)
- Hamburg: Planning Dept Major Subdivision Review
- Lancaster: §400-38 Subdivisions (Dual-Board, TB Final Authority)
- Orchard Park: Ch. 121 Subdivision of Land (Three 62-Day Clocks)
- Pendleton: Ch. 220 Subdivision of Land (Niagara County)
- Wheatfield: Ch. 169 + §200-45–47 Conservation/Cluster (Niagara County)