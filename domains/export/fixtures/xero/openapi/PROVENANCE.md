# Xero Accounting API OpenAPI — vendored spec

This directory is the **authoritative location** for the Xero Accounting API
OpenAPI specification per R-0061 FIX-001 / FIX-015.

Consumer repositories (e.g. `ledgius-api`) keep a mirror for local test
access; the mirror is kept in sync via a `make sync-fixtures` target in the
consumer repo. When a Xero spec bump is required, it lands here first via a
`chore(fixtures): bump xero spec to {version}` PR; consumer-repo PRs then
refresh their mirrors and adapt any dependent mapping configs.

## `xero_accounting.yaml`

| Field | Value |
|---|---|
| **Source** | `https://github.com/XeroAPI/Xero-OpenAPI` |
| **Raw URL** | `https://raw.githubusercontent.com/XeroAPI/Xero-OpenAPI/ea736267aadf4dce69ea3be3fd25cd6355f6d2df/xero_accounting.yaml` |
| **Pinned commit** | `ea736267aadf4dce69ea3be3fd25cd6355f6d2df` (2026-04-02) |
| **Vendor version** | Xero Accounting API v12.0.0 |
| **Licence** | MIT (per `LICENSE` in the upstream repo) |
| **Captured** | 2026-04-16 |
| **Captured by** | Ledgius engineering (feat/xero-contract-harness) |
| **MD5** | `0b98ae6b8b3b3017abcef6a59d739ac0` |
| **Modifications from original** | None — byte-for-byte copy |

## Why this file

OpenAPI 3.0 definition of Xero's Accounting API — the authoritative source
for field names, types, enumerations, required/optional flags, and maximum
lengths on every resource the Ledgius Xero export touches:
`Invoice`, `Contact`, `CreditNote`, `Account`, `TaxRate`, `LineItem`, `Address`.

This file is what catches format drift between Ledgius's assumptions and
what Xero actually accepts. The `ledgius-api` contract test suite loads
the mirrored copy and validates every mapping config against schemas
defined here.

## Upgrade procedure

1. Check the upstream repo (`XeroAPI/Xero-OpenAPI`) for a new release tag.
2. Open a PR here titled `chore(fixtures): bump xero spec to {version}`.
3. Refresh this file:

   ```bash
   curl -sfL "https://raw.githubusercontent.com/XeroAPI/Xero-OpenAPI/{new-sha}/xero_accounting.yaml" \
     -o domains/export/fixtures/xero/openapi/xero_accounting.yaml
   ```

4. Update the **Pinned commit**, **Vendor version**, **Captured** date,
   and **MD5** rows above.
5. Request review from someone with accounting-domain knowledge per
   R-0061 FIX-020. Spec diffs carry semantic weight — not rubber-stamp.
6. After merge, open a matching PR in each consumer repo:

   ```bash
   cd ledgius-api
   make sync-fixtures
   go test ./...    # fix any contract failures the bump reveals
   ```

## Known limitations in Ledgius v1 conformance

These are documented in consumer repos but re-stated here so the
spec-side reader has the full picture:

- **Address shape mismatch between CSV and API channels.** The Xero API
  (per this spec) uses a nested `Address` object with `AddressLine1..4`,
  `AddressType`, etc. The CSV import convention uses flat `POAddressLine1`
  / `SAAddressLine1` prefixes. Ledgius v1 Xero export configs target the
  CSV shape; the contract harness validates only non-address fields
  against the OpenAPI schema. Phase F (Xero API channel) will add
  API-shape configs and the harness will run full validation on them.
- **CSV templates are a sibling directory.** CSV import templates are
  not OpenAPI-describable; they live at `../csv-templates/` and require
  a Xero account login to capture. See that directory's README.
