# MYOB Entity Catalogue — vendor reference material

## `myob_entity_catalogue.md`

| Field | Value |
|---|---|
| **Source** | Official MYOB Business API endpoint documentation on https://apisupport.myob.com |
| **Method** | Manual catalogue assembled from the official endpoint pages (see citation list at the end of the document itself — each entity cites its own MYOB `S1`..`S10` source references with the page's `Date Released` + `Date Updated` values). |
| **Scope** | Public, integration-facing MYOB Business API entity catalogue. **NOT** a physical MYOB database schema dump. MYOB does not publish its physical schema; the API-exposed model is the closest public analog. |
| **Captured** | 2026-04-17 |
| **Captured by** | Ledgius engineering |
| **Modifications from original** | None — byte-for-byte copy. Source-internal `S1`..`S10` citations remain intact. |
| **Licence** | MYOB documentation is publicly available developer reference. Vendored here as reference material under fair-use / informational use; no derivative redistribution. |

## Why this file lives here

Two purposes:

1. **Comparison source** for the Ledgius domain-model gap analysis (see `../../domain-model-gap-analysis.md`). Used on a **case-by-case basis** when real import *or export* scenarios surface fields Ledgius's domain model lacks — not as a parity target. See *Guiding principle* below.
2. **Canonical reference** for future MYOB import + export work. When the MYOB importer is migrated to the mapping engine (R-0017 FR-028), the YAML mapping configs reference this catalogue as the authoritative field-level source.

## Guiding principle — read before making schema changes

This catalogue is a **reference**, not a **specification Ledgius must match**. The rule is:

- Fields that Ledgius lacks and that a **real import or export scenario** (or a compliance requirement) needs → candidates for a schema change, each justified individually in the gap analysis.
- Fields that MYOB has but no import or export scenario surfaces → leave them out. Every optional field added to the domain model adds UX friction to the creation / edit UI and noise to the schema.
- Fields that MYOB models in a vendor-idiosyncratic way (e.g. denormalised address slots, embedded Selling/BuyingDetails) → deliberately *not* copied — Ledgius prefers the cleaner domain model.

The goal is a **superior hybrid** — smarter than MYOB where MYOB is bloated or idiosyncratic, richer than MYOB only where real Ledgius requirements demand it.

Per R-0061 (Canonical Import/Export Test Fixtures, FIX-001), canonical vendor reference material lives in `ledgius-specs/domains/{domain}/fixtures/` so non-engineer reviewers (CPAs, auditors) can browse it without code-repo access.

## Consumer repositories

None yet. When the MYOB import YAML migration lands, `ledgius-api/internal/importer/mappings/v1/myob-ao/` will reference this document as the canonical source for MYOB field shapes. `make sync-fixtures` would mirror it into consumer repos if ever needed.

## Update procedure

If MYOB publishes an updated entity catalogue, open a PR titled `chore(fixtures): bump myob entity catalogue to {date}`, replace this file, and refresh the `Captured` date above. Any entity whose `Date Updated` advances in the upstream document may trigger downstream work: check the Ledgius domain-model gap analysis and any active MYOB YAML import configs.
