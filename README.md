# Navixy Account Overview Dashboard

A single-page, fully interactive dashboard providing a comprehensive overview of a Navixy account — tracking objects, tasks, fleet, maintenance, and mileage — designed to be embedded via the **User Applications** feature.

## Features

- **Tracker Status** — Total objects with online/moving/parked/idle/offline counts (live, batched `get_states`)
- **Connection Trend** — Rolling time-series line chart of connection states across page sessions
- **Status Distribution** — Doughnut chart of tracker states
- **Today's Tasks** — Counts by status: assigned, in-progress, done, failed, delayed, unassigned
- **Tasks Distribution** — Doughnut chart of task statuses
- **Fleet Overview** — Vehicle totals, tracker linkage, fuel type breakdown
- **Maintenance** — Service tasks by status (expired / due soon / scheduled / done) with overdue highlights
- **Fleet Mileage (7d)** — Last 7 days total fleet mileage as a bar chart
- **Mileage Trend** — 7-day mileage as a line chart
- **Top Objects by Mileage** — Horizontal bar chart of top 10 objects by 7-day mileage
- **Recent Events** — Last 30 tracker events from the past 24h with clickable map coordinates
- **Auto-refresh** every 60 seconds

## Interactive Layout

- **Drag-and-drop** tile reordering via Sortable.js
- **Add / remove** tiles from a slide-up drawer
- **Resize** tiles (small / medium / large)
- Layout persisted in `localStorage` — survives page reloads

## Authentication

This app uses the Navixy **User Session** authorization mode. When opened via User Applications, Navixy automatically appends the user's session `session_key` to the URL.

No backend required — all API calls are made directly from the browser to the Navixy Backend API.

The app **auto-detects** whether your account is on the EU (`api.eu.navixy.com`) or US (`api.us.navixy.com`) server by probing both in parallel and using whichever responds successfully first.

## Setup as a User Application

1. Go to **Account Settings → User Applications** in your Navixy account.
2. Click **Add Application** and fill in:
   - **Label**: Account Overview (or any name)
   - **URL**: `https://amasyunin.github.io/basic-dashboard/`
   - **Display as**: Embedded
   - **Authorization**: User session
3. Save and open the app from the Navixy sidebar.

## Manual / Development Use

Open the file directly with your session key as a URL parameter:

```
index.html?session_key=YOUR_SESSION_KEY
```

To obtain a session key for testing:

```bash
curl -X POST https://api.eu.navixy.com/v2/user/auth \
  -H 'Content-Type: application/json' \
  -d '{"login":"your@email.com","password":"yourpassword"}'
```

*(use `api.us.navixy.com` for US accounts)*

## Files

```
index.html   — Self-contained dashboard (no build step, no local dependencies)
```

## Dependencies (CDN)

- [Chart.js 4.4.4](https://www.chartjs.org/) — bar, line, and doughnut charts
- [Sortable.js 1.15.3](https://sortablejs.github.io/Sortable/) — drag-and-drop tile reordering
