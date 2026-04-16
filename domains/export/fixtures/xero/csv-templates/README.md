# Xero CSV import templates — pending user capture

This directory is reserved for the four v1 Xero CSV import templates
per R-0061 FIX-016:

- `contacts.csv`
- `invoices.csv`
- `bills.csv`
- `credit-notes.csv`

## Why it's empty

Xero serves CSV import templates only through its authenticated Xero
Central UI ("Download sample file" on each import article). They are
not available as a public URL, so neither CI nor a contributor working
from a fresh clone can fetch them.

## How to supply them

1. Sign into a Xero demo company (free developer account via
   [developer.xero.com](https://developer.xero.com)).
2. From the main menu: **Business → Invoices → Import → Download
   sample file**. Repeat for Bills, Contacts, and Credit notes.
3. Drop the four files into this directory **without modification**.
4. Add a `PROVENANCE.md` entry recording capture date, demo-company
   identifier, and a statement confirming no data edits.
5. The consumer-side contract test harness (ledgius-api) will
   auto-detect via `make sync-fixtures` and upgrade from
   "header-subset check against third-party sources" to
   "strict header match against vendor templates."

## Interim behaviour

Until supplied, header contracts in the consumer repos fall back to
minimum header sets publicly quoted in third-party documentation.
That covers ~80% of the signal a full template provides but leaves
gaps for optional and region-specific columns. Tests surface the
gap explicitly so it doesn't silently persist.
