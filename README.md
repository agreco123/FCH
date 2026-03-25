# WNY Land Development Command Center — V10

**V10-SUPABASE-EMPIRICAL** · 7-Town Residential Subdivision Tracker · Erie & Niagara Counties, NY

## What Changed from V9

V10 replaces the localStorage-only data layer with a Supabase PostgreSQL backend while preserving the complete V9 UI (TrackerView, DevManager, 9-tab dashboard, Gantt chart).

### New in V10 (Phase 2 — Supabase Data Foundation)
- **12-table Supabase schema** with Row Level Security, indexes, and auto-timestamps
- **265 task templates** across 7 municipalities loaded from database
- **Structured meeting rules** (JSON) for calendar-aware scheduling (Phase 4 prep)
- **Conditional task flags** (`is_conditional`, `condition_key`) for task wizard (Phase 5 prep)
- **Seasonal category tagging** (`Construction`, `Paving`, `Field_Survey`) for winter penalties
- **Board-dependent flags** for meeting-snap scheduling
- **Empirical duration columns** (`p10_days`, `p50_days`, `p90_days`) ready for Phase 3 calibration
- **Board meetings table** with 2024–2030 dates generated from structured rules
- **NYS/Federal holidays** 2024–2030 for business-day scheduling
- **Connection status indicator** (green = Supabase, yellow = offline/cached)
- **localStorage fallback** — app works offline, syncs when reconnected

### Preserved from V9
- All 265+ hardcoded task names, durations, dependencies, and regulatory references
- Dependency chains and phase ordering per town
- 6-state status system, risk flags, responsible parties
- Phase color definitions, dark theme, DM Sans / JetBrains Mono typography
- TrackerView Gantt chart, DevManager 9-tab dashboard
- InlineEdit, PhaseSelect, StatusButton, StatCard components

---

## Deployment: 4 Steps

### Step 1: Run SQL Migrations in Supabase SQL Editor

Go to your Supabase project → **SQL Editor** → run these files **in order**:

```
1. 01_schema.sql          — Creates all 12 tables, indexes, RLS policies, triggers
2. 02_seed_municipalities.sql  — Seeds 7 municipalities with structured meeting rules
3. 03_seed_task_templates.sql  — Seeds all 265 task templates with V10 flags
4. 04_seed_reference_data.sql  — Seeds holidays, costs, contacts, board meetings, doc checklist
```

### Step 2: Get Your Anon Key

In Supabase Dashboard → **Settings** → **API** → copy the `anon` / `public` key.

### Step 3: Set the Key in index.html

Open `index.html` and replace:
```js
const SUPABASE_ANON_KEY = "PASTE_YOUR_ANON_KEY_HERE";
```
with your actual anon key.

### Step 4: Deploy

**Option A: Local**
```bash
npm install && npm start
# Open http://localhost:3000
```

**Option B: Render**
Push to GitHub, connect to Render using the included `render.yaml`.

**Option C: Static hosting (Netlify, Vercel, etc.)**
Just deploy `index.html` — it's a single-file app with CDN dependencies.

---

## Verify Deployment

After deploying, you should see:
- Green connection dot → "Supabase" in the top bar
- All 7 towns loading in the TrackerView town selector
- Task counts matching V9 (Amherst: 39, Clarence: 42, Hamburg: 36, Lancaster: 36, Orchard Park: 37, Pendleton: 35, Wheatfield: 40)
- Cost estimates, contacts, and doc checklist loading in DevManager tabs

---

## Schema: 12 Tables

| Table | Purpose |
|-------|---------|
| `municipalities` | 7 towns with structured meeting rules |
| `task_templates` | 265 tasks with V10 conditional/seasonal/board flags |
| `developments` | User-created projects |
| `development_tasks` | Per-project task instances with actual tracking |
| `board_meetings` | 2024–2030 meeting dates from structured rules |
| `board_minutes_raw` | Raw board minutes (Phase 3) |
| `board_minutes_events` | Extracted events from minutes (Phase 3) |
| `empirical_durations` | Computed duration pairs (Phase 3) |
| `holidays` | NYS/Federal holidays 2024–2030 |
| `cost_estimates` | Development cost ranges |
| `contacts` | Regional agency contacts |
| `doc_checklist` | Document submission checklist |

---

## Remaining Phases

| Phase | Status | Description |
|-------|--------|-------------|
| Phase 1 | Pending | Internal Knowledge Refresh (regulatory research) |
| Phase 2 | ✅ Complete | Supabase Data Foundation |
| Phase 3 | Pending | Minutes Ingestion & Empirical Calibration |
| Phase 4 | Pending | Calendar-Aware Scheduling Engine |
| Phase 5 | Pending | Operational Intelligence Layer |

---

*V10 Engineering Directive · March 25, 2026 · Internal Use Only · Not Legal Advice*
