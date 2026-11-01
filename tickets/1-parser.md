**Reports covered: 374** (of the 412 unique reports merged into #4471)

The shared date parser reads every date month first (MM/DD). Tenants whose locale writes the day first get flipped dates.

- Where: app (202), email (147), booking-v2 form (25)
- Tenants: all 11 day-first tenants (harbour.dental 52, kettle.books 46, nine.lanterns 43, morrow.tax 40, long.table 39, ridge.clinic 36, stone.and.sons 30, lantern.row 27, alder.physio 22, pale.harbour 20, copper.studio 19)
- First seen 2026-04-01, last seen 2026-10-04
- Report ids: `tickets/report-ids-parser.txt`

This is the bug #4471 describes. The queued parser fix closes this ticket and no other.

Page: `src/routes/kb/incidents/4471-split/+page.svx`
