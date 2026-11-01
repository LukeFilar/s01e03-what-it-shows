**Reports covered: 379** (of the 412 unique reports merged into #4471)

The shared date parser reads every date month first (MM/DD). Tenants whose locale writes the day first get flipped dates.

- Where: app (204), email (150), booking-v2 form (25)
- Tenants: all 11 day-first tenants
- First seen 2026-04-01, last seen 2026-10-04
- Report ids: `tickets/report-ids-parser.txt`
- 5 of these 379 (R-41202, R-41209, R-41236, R-41344, R-41620) read as a one-day move, not a day/month flip. The desk files them here by tenant and footnotes them. One mentions Lisbon and Toronto, so a time zone problem is possible and worth a look.

This is the bug #4471 describes. The queued parser fix covers this ticket and not the form hint.

Page: `src/routes/kb/incidents/4471-split/+page.svx`
