# Navixy Account Overview Dashboard

A single-page dashboard that provides a comprehensive overview of a Navixy account — tracking objects, tasks, fleet, maintenance, and mileage — designed to be embedded via the **User Applications** feature.

## Features

- **Tracking** — Total objects, online/offline/idle/moving/parked counts (live, batched `get_states`)
- **Today's Tasks** — Counts by status: assigned, in-progress, done, failed, delayed, unassigned
- **Fleet** — Vehicle totals, tracker linkage, fuel type breakdown
- **Maintenance** — Service tasks by status (expired / due soon / scheduled / done) with overdue highlights
- **Mileage Chart** — Last 7 days total fleet mileage as a bar chart (Chart.js)
- **Top Objects by Mileage** — Horizontal bar chart of top 10 objects by 7-day mileage
- **Recent Events** — Last 30 tracker events from the past 24h with clickable map coordinates
- **Auto-refresh** every 60 seconds

## Authentication

This app uses the Navixy **User Session** authorization mode. When opened via User Applications, Navixy automatically appends the user's session `hash` to the URL.

No backend required — all API calls are made directly from the browser to the Navixy Backend API.

## Setup as a User Application

1. Go to **Account Settings → User Applications** in your Navixy account.
2. Click **Add Application** and fill in:
   - **Label**: Account Overview (or any name)
   - **URL**: The URL where this `index.html` is hosted
   - **Display as**: Embedded
   - **Authorization**: User session
3. Save and open the app from the Navixy sidebar.

## Manual / Development Use

Open the file directly with your session hash as a URL parameter:

```
index.html?hash=YOUR_SESSION_HASH&server=https://api.eu.navixy.com
```

| Parameter | Default | Description |
|-----------|---------|-------------|
| `hash` | — | Navixy session hash (required) |
| `server` | `https://api.eu.navixy.com` | API base URL (`https://api.us.navixy.com` for US accounts) |

To obtain a session hash for testing:

```bash
curl -X POST https://api.eu.navixy.com/v2/user/auth \
  -H 'Content-Type: application/json' \
  -d '{"login":"your@email.com","password":"yourpassword"}'
```

## Files

```
index.html   — Self-contained dashboard (no build step, no local dependencies)
```

Chart.js is loaded from CDN at runtime.