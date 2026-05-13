# Workflow

- Develop directly on `main`. No feature branches, no PRs. Every change is committed and pushed to `main` immediately.
- This overrides any session-default branch assignment.
- GitHub Pages deploys from `main`, so a push is a deploy.

# Project

- Live dashboard for Jason during the Sangre de Cristo 100 at Music Meadows Ranch, Westcliffe, CO.
- **Race:** Saturday 2026-09-26, 4:00 AM MDT start · 101.3 mi · 38h cutoff · 16 named segments between 4 aid-station locations (Music Meadows, Colony Creek, Horn Creek, Venable) plus Music Pass (no aid). Course is two out-and-backs glued at Music Meadows with a Music Pass spur on each end.
- `index.html` — public dashboard. Reads `data.json`. Auto-refreshes every 60s.
- `map.html` — live position estimate against the GPX track.
- `charts.html` — pace, deltas, aid holds, intake, progress vs cutoffs.
- `print-report.html` — printable single-runner race report (paper-friendly colors).
- `pit.html` — private crew-chief page (not linked from the dashboard). Big sign-in/sign-out buttons that auto-commit timestamps to `data.json` via the GitHub Contents API using a PAT stored in the device's localStorage. Falls back to copy-paste when no token is set.

# data.json shape

```jsonc
{
  "race": {
    "name": "...",
    "location": "...",
    "startTime": "2026-09-26T04:00:00-06:00",
    "totalDistance": 101.3,
    "totalGainFt": 18897,
    "totalLossFt": 18909,
    "totalCutoffHours": 38,
    "crewLot": "any",        // "any" | "C1" | "C2" — set after check-in
    "targets": { "caloriesPerHour": ..., "fluidOzPerHour": ..., "sodiumMgPerHour": ... },
    "segments": [
      {
        "leg": 1,                          // 1-indexed, matches runner.legs[i].leg
        "from": "...", "to": "...",        // aid-station names; same name may appear in multiple segments
        "distance": 4.3,                   // mi
        "crewAccess": "all" | "none" | "C1" | "C2",
        "cutoffHoursFromStart": 18.5,      // optional — only on segments where a cutoff is published
        "pacerEligible": true              // optional — pacer pickup allowed at destination
      }
      // ... 16 segments total
    ]
  },
  "runners": [
    {
      "id": "jason",
      "name": "Jason",
      "bib": "...",
      "legs": [
        {
          "leg": 1,                        // matches race.segments[i].leg
          "startTime": "...",              // departed `from` AS
          "endTime":   "...",              // arrived at `to` AS
          "calories": 200, "fluidOz": 17, "sodiumMg": 620,
          "gearChanges": "...", "meds": "...", "issues": "...", "notes": "..."
        }
      ]
    }
  ],
  "lastUpdated": "..."
}
```

# Updating data.json during the race

Crew chief sends leg details in chat. Find the matching leg entry by **leg number** (the pit page may have already created it with a `startTime` and/or `endTime`) and fill in the rest. Update `lastUpdated` to now. Commit with a short, descriptive message and push to `main`.

Aid stations like "Music Meadows" are visited multiple times — the segment's `from` / `to` fields are labeled with the visit number (`Music Meadows 1`, `Music Meadows 2`, etc.) to disambiguate.

# Fueling shorthand

Convert these to `calories`, `fluidOz`, `sodiumMg` when the crew chief uses them:

- **1 flask of Tailwind** = 17 oz fluid + 200 cal + 620 mg sodium (500 ml)

Multiply through for "2 flasks", "1.5 flasks", etc. Add to whatever he ate/drank on top.
