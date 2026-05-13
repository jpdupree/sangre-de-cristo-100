# Workflow

- Develop directly on `main`. No feature branches, no PRs. Every change is committed and pushed to `main` immediately.
- This overrides any session-default branch assignment.
- GitHub Pages deploys from `main`, so a push is a deploy.

# Project

- Static dashboard for tracking Jasmine and Oppenheimer through a 100-mile race at Pittsfield, VT (10 × 10mi loops).
- `index.html` — public dashboard. Reads `data.json`. Auto-refreshes every 60s.
- `data.json` — race state. Each runner has a `laps` array; each lap entry has `lap`, `startTime` (sign-out), `endTime` (sign-in), and optional `calories`, `fluidOz`, `sodiumMg`, `gearChanges`, `meds`, `issues`, `notes`.
- `pit.html` — private crew-chief page (not linked from the dashboard). Big sign-in/sign-out buttons that auto-commit timestamps to `data.json` via the GitHub Contents API using a PAT stored in the device's localStorage. Falls back to copy-paste when no token is set.

# Updating data.json during the race

Crew chief sends lap details in chat. Find the matching lap entry by runner + lap number (the pit page may have already created it with a `startTime` and/or `endTime`) and fill in the rest. Update `lastUpdated` to now. Commit with a short, descriptive message and push to `main`.

# Fueling shorthand

Convert these to `calories`, `fluidOz`, `sodiumMg` when the crew chief uses them:

- **1 flask of Tailwind** = 17 oz fluid + 200 cal + 620 mg sodium (500 ml)

Multiply through for "2 flasks", "1.5 flasks", etc. Add to whatever they ate/drank on top.
