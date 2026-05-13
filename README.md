# Sangre de Cristo 100 · Race Dashboard

Live tracker for Jason during the Sangre de Cristo 100 at Music Meadows Ranch, Westcliffe, CO.

**Race start:** Saturday 2026-09-26, 4:00 AM MDT
**Cutoff:** 38 hours (Sunday 6:00 PM MDT)
**Course:** 101.3 mi · +18,897 ft · 4 aid locations × 13 stops, plus Music Pass (no aid) at start and end of each "loop"

The dashboard reads from `data.json`. Every commit to `main` updates the live site within ~30 seconds. Page auto-refreshes every 60 seconds.

## Pages

- `index.html` — public dashboard. Auto-refreshes.
- `map.html` — live position estimate on the course.
- `charts.html` — pace, deltas, aid holds, intake, progress vs cutoffs.
- `print-report.html` — printable single-runner race report.
- `pit.html` — private crew-chief sign-in/out page (not linked from the dashboard).

## Updating during the race

Crew chief messages Claude Code with leg info:

> "Jason leg 4 done (Horn Creek 1), 1:48, 300 cal, 34oz, 1240mg sodium"

Claude Code finds the matching leg in `data.json`, fills it in, commits, pushes. Done.

The pit.html page can also auto-commit sign-in/sign-out timestamps via the GitHub Contents API using a PAT stored in the device's localStorage. Falls back to copy-paste when no token is set.

## Manual update fallback

If Claude Code is unavailable, edit `data.json` directly via:
- github.dev (open repo, press `.` in browser)
- GitHub mobile app
- `git` from any terminal

Schema is in the data.json file itself — copy a previous leg entry and edit values.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
