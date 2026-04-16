# Xero fixtures (canonical)

This directory holds the **authoritative master copies** of Xero vendor
artefacts referenced by every Ledgius repo. Consumer repositories keep
mirrors for local test access and synchronise with `make sync-fixtures`.

Per R-0061 FIX-001 / FIX-015, canonical reference fixtures live here so
non-engineer reviewers (CPAs, auditors) can browse them without clone
access to API code.

## Contents

| Path | Content | Status |
|---|---|---|
| `openapi/xero_accounting.yaml` | Xero Accounting API OpenAPI 3.0 spec | Vendored (v12.0.0 pinned) |
| `openapi/PROVENANCE.md` | Source, pinned commit, MD5, upgrade procedure | Current |
| `csv-templates/` | Xero CSV import templates (contacts, invoices, bills, credit notes) | Pending user capture — Xero UI-gated |

## Why authoritative lives here

- **Audit defensibility.** An auditor asking "what Xero version do you claim to conform to" finds one answer in one place. Mirrors are clearly identified as such.
- **Single version bump path.** A Xero spec bump is one PR against this directory; consumer repos follow with `make sync-fixtures` + any necessary mapping updates.
- **Symmetric structure.** Future target systems (MYOB spec files, QuickBooks OpenAPI) land under `domains/export/fixtures/{system}/` in the same shape.

## Consumer mirrors

| Repository | Mirror location | Sync command |
|---|---|---|
| `ledgius-api` | `internal/exporter/xero/testdata/canonical/xero_accounting.yaml` | `make sync-fixtures` |

CI in consumer repos runs the sync command and fails if the resulting
diff is non-empty — drift between master and mirror is caught
automatically, not silently.
