**Reports covered: 33** (of the 412 unique reports merged into #4471)

The booking-v3 form prints `MM/DD/YYYY` under its date field. People at day-first tenants type the month first because the form tells them to, and the form then reads the date the tenant's way. The shared parser is not the cause, so the parser fix does not fix this.

- Where: booking-v3 form only (33)
- Tenants: alder.physio 12, copper.studio 11, pale.harbour 10
- First seen 2026-04-17, last seen 2026-09-22
- Report ids: `tickets/report-ids-hint.txt`
- Intake tagged only 18 of these `hint`; 15 were tagged `parser`.

Page: `src/routes/kb/incidents/4471-split/+page.svx`
