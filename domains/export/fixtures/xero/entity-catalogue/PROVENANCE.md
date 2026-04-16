# Xero Accounting Entity Catalogue — vendor reference material

## `xero_accounting_entity_catalogue.md`

| Field | Value |
|---|---|
| **Source** | Xero Accounting API public documentation on https://developer.xero.com/documentation/api/accounting + the `xero-node` / `Xero-NetStandard` SDK OpenAPI spec (vendored at commit `ea736267`, API version `v12.0.0`). |
| **Method** | Manual catalogue assembled from the official endpoint pages and OpenAPI schemas. Each entity cites the specific Xero endpoint it was derived from. |
| **Scope** | Public, integration-facing Xero Accounting API entity catalogue. **NOT** a physical Xero database schema dump — Xero does not publish their physical schema; the API-exposed model is the closest public analog. |
| **Captured** | 2026-04-17 |
| **Captured by** | Ledgius engineering |
| **Modifications from original** | None — byte-for-byte copy. Source-internal field citations remain intact. |
| **Licence** | Xero API documentation is publicly available developer reference. Vendored here as reference material under fair-use / informational use; no derivative redistribution. |

## Why this file lives here

Two purposes:

1. **Comparison source** for the Ledgius domain-model gap analysis (see `../../domain-model-gap-analysis.md`). Used on a **case-by-case basis** when real import *or export* scenarios surface fields Ledgius's domain model lacks — not as a parity target. See *Guiding principle* below.
2. **Canonical reference** for Xero import + export work. The R-0057 Xero CSV export and future Xero API export consume field-shape information from this catalogue; the R-0017 Xero import pipeline (and its YAML mapping config) references it as the authoritative source for Xero-side field names, types, and required-ness.

Per R-0061 (Canonical Import/Export Test Fixtures, FIX-001), canonical vendor reference material lives in `ledgius-specs/domains/{domain}/fixtures/` so non-engineer reviewers (CPAs, auditors) can browse it without code-repo access.

## Guiding principle — read before making schema changes

This catalogue is a **reference**, not a **specification Ledgius must match**. The rule is:

- Fields that Ledgius lacks and that a **real import or export scenario** (or a compliance requirement) needs → candidates for a schema change, each justified individually in the gap analysis.
- Fields that Xero has but no import or export scenario surfaces → leave them out. Every optional field added to the domain model adds UX friction to the creation / edit UI and noise to the schema.
- Fields that Xero models in a vendor-idiosyncratic way (e.g. legacy flags, denormalised flat addresses) → deliberately *not* copied — Ledgius prefers the cleaner domain model.

The goal is a **superior hybrid** — smarter than Xero where Xero is bloated or idiosyncratic, richer than Xero only where real Ledgius requirements demand it.

## Consumer repositories

- `ledgius-api/internal/importer/mappings/v1/xero/` — once the Xero CSV import is migrated to the mapping engine (R-0059), the YAML mapping configs reference this document as the canonical source for Xero source-field shapes.
- `ledgius-api/internal/exporter/xero/mappings/v1/` — Xero export YAML configs reference this document for target field shapes (required-ness, data types, max lengths).
- `make sync-fixtures` mirrors this into consumer repos if a consumer needs local access.

## Update procedure

If Xero publishes an updated API version (e.g. `v13.0.0`), open a PR titled `chore(fixtures): bump xero entity catalogue to {version}`, replace this file, and refresh the `Captured` date + API version line above. The bump may trigger downstream work: check the Ledgius domain-model gap analysis and any active Xero YAML mapping configs (both import and export) for fields that changed shape upstream.
