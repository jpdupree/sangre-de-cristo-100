# 100-Mile Race Dashboard

Live tracker for Jasmine and Oppenheimer during the 100-mile race at Pittsfield, VT.

**Race start:** Friday 2026-05-08, 7:00 AM EDT
**Cutoffs:** last lap must start by 6:00 PM Saturday (35h); final cutoff 9:00 PM Saturday (38h)

The dashboard reads from `data.json`. Every commit to the working branch updates the live site within ~30 seconds. Page auto-refreshes every 60 seconds.

## Updating during the race

Crew chief messages Claude Code with lap info:

> "Jasmine lap 3 done, 2:54, 240 cal, 28oz, 500mg sodium"

Claude Code edits `data.json`, commits, pushes. Done.

## Manual update fallback

If Claude Code is unavailable, edit `data.json` directly via:
- github.dev (open repo, press `.` in browser)
- GitHub mobile app
- `git` from any terminal

Schema is in the data.json file itself — copy a previous lap entry and edit values.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
