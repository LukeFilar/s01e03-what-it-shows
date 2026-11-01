**Reports covered: 5** (of the 412 unique reports merged into #4471)

These reports describe a date that is one day off, not a swapped day and month. One mentions a client in Lisbon and a client in Toronto getting different days for the same meeting, which points at a time zone problem. The bodies are short, so the cause is a guess and needs its own investigation.

- Reports: R-41202, R-41209, R-41236, R-41344, R-41620
- Tenants: kettle.books, alder.physio, nine.lanterns, pale.harbour, lantern.row
- The kb code (`causes.ts`) files them under the parser problem; `desk-notes.json` footnotes them as "read as a one-day move".
- Report ids: `tickets/report-ids-one-day-move.txt`

Page: `src/routes/kb/incidents/4471-split/+page.svx`
