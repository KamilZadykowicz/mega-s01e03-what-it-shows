# How the groups were derived

Source: `reports-4471.json` (427 rows), `tenants/*.json`, `causes.ts`, `desk-notes.json`.

1. **Unique reports.** The export's pages overlap: 15 ids appear twice. One id, one report
   → 412 unique reports. This matches the desk's page ("412 reports"), so the duplicate
   rows are an export artifact, not a problem in #4471.

2. **Two date-parse causes, from the kb's own logic (`causes.ts`).**
   - `parser`: the shared parser reads dates month first; every tenant is day-first
     (en-GB, de-DE, es-ES, nl-NL, cs-CZ, it-IT, fr-FR, pl-PL, pt-PT, da-DK, en-IE).
   - `hint`: a form-channel report from a `booking-v3` tenant (hint says MM/DD/YYYY,
     the form parses day-first).
   Splitting on that: 374 parser, 33 hint (alder.physio 12, copper.studio 11,
   pale.harbour 10 — all form channel).

3. **One-day-move reports.** `desk-notes.json` lists five reports the desk read as one
   "one day move". Their bodies show three problems, none a date flip:
   - off by exactly one day: R-41202, R-41209, R-41620 → 3 reports;
   - invite timestamped before the booking: R-41236 → 1 report;
   - same meeting, different day per timezone (Lisbon vs Toronto): R-41344 → 1 report.

4. **Swap check.** Every remaining report body holds a date pair where day and month are
   exchanged (e.g. "5 August" → "8 May"), except four without a date pair: R-41290
   (feature request for a day-first setting), R-41417, R-41515 (wrong-day complaints /
   workaround), R-41615 (October bookings arriving as January — 1 October parsed as
   10 January). Each of the four is the parser bug as its reporter lived it, so they stay
   in the parser group: 374.

Counts: 374 + 33 + 3 + 1 + 1 = 412. Ids per group: `group-ids.json`.
