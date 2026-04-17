# MYOB AccountRight Import/Export Field Reference — vendor reference material

## `myob_import_field_reference.md`

| Field | Value |
|---|---|
| **Source** | Official MYOB AccountRight Help Centre — Import and Export Fields page |
| **URL** | https://myob.com/au/support/myob-business/import-export/myob-business-importing-and-exporting-data-import-and-export-fields?productview=Desktop |
| **Method** | Automated extraction via web fetch of the official MYOB help page |
| **Scope** | Complete list of import/export fields for all MYOB AccountRight entity types: Accounts, Activities, Budgets, Customer Cards, Supplier Cards, Items, Jobs, Transactions (Sales, Purchases, General Journal) |
| **Captured** | 2026-04-17 |
| **Captured by** | Ledgius engineering |
| **Modifications from original** | Reformatted from HTML to markdown table. Field names, types, and constraints are verbatim from the source. |
| **Licence** | MYOB documentation is publicly available help content. Vendored here as reference material under fair-use / informational use. |

## Why this file lives here

Used as the target field reference for the Ledgius → MYOB export YAML mapping configs (`ledgius-api/internal/exporter/myob/mappings/v1/*.yaml`). The YAML config target field names must match these import field names exactly for MYOB's Import/Export Assistant to accept the file.

## Update procedure

If MYOB updates their import field specifications, re-fetch the page and replace this file. Check the YAML export configs for any field name changes.
