# #4471 — split into its real problems

MEGA.dev S01E03 · Challenge "what it shows".

The support desk merged 412 reports about dates into one ticket, #4471, and marked it known
as "dates parse mm/dd in eu locales". The merged ticket actually holds **five distinct
problems**. This repo files one ticket (GitHub issue) per problem, each with how many
reports it covers, and adds a signed page about them to the kb.

## Tickets

| # | Problem | Reports |
|---|---------|---------|
| 1 | Parser reads day-first dates as month-first (the mm/dd flip) | 379 |
| 2 | booking-v3 form hint says MM/DD/YYYY but the form parses day-first | 33 |
| 3 | Bookings land one day off (DST suspected) | 3 |
| 4 | Invite timestamped before the booking was made | 1 |
| 5 | Same meeting renders on different days in different timezones | 1 |

Total: 412 reports. The desk's page counted 412 unique reports; the export has 427 rows
because 15 ids appear twice (the kb already documents overlapping export pages — one id,
one report).

## The page

- `src/routes/kb/incidents/4471-split/+page.svx` — the kb page, signed, as it goes into the kb.
- `4471-split.html` — the same page rendered, as the desk will see it.

## Grouping

`data/group-ids.json` lists every report id per problem; `data/grouping.md` explains how the
groups were derived.
