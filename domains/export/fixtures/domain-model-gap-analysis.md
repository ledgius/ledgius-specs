# Ledgius Domain Model Gap Analysis — MYOB + Xero vs Ledgius

**Purpose:** Record, on a per-entity basis, where the MYOB and Xero public data models surface fields that Ledgius's domain model lacks, and — **only when a concrete import or export scenario justifies it** — propose a schema change to close the gap.

**This document is NOT a parity checklist.** The vendored vendor catalogues at `myob/entity-catalogue/myob_entity_catalogue.md` and `xero/entity-catalogue/xero_accounting_entity_catalogue.md` are references, not specifications Ledgius must match. See the **Guiding principle** below before adding anything here.

---

## Guiding principle (mantra)

> Use MYOB/Xero catalogues **on a case-by-case justification basis only**. We want to avoid database bloat, which creates creation UX/UI friction because there are too many optional fields.

Every row in the *Proposed action* column of the entity tables below must carry one of these justifications:

- **J-IMP** — a real import scenario (Xero CSV, MYOB AO, MYOB AE MAS, CeeData, generic CSV) produces records that carry this field with non-null data, and the current Ledgius schema has nowhere to put it without loss.
- **J-EXP** — a required field in a Xero or MYOB export target has no Ledgius source, so we'd have to default/infer it (which R-0017 FR-027 forbids).
- **J-COMPLIANCE** — Australian Privacy Act, ATO record-keeping, BAS, STP, or Super Guarantee requires Ledgius to hold this information regardless of third-party integration.
- **J-DOMAIN** — a first-class Ledgius business feature (reconciliation, reporting, dashboards) depends on the field.

If the only justification for adding a field is "MYOB has it" or "Xero has it", the answer is **no** — leave it out.

---

## Reading the entity tables

Each entity section contains one table with columns:

| Column | Meaning |
|---|---|
| **Field (vendor name)** | The field as it appears in the vendor catalogue |
| **MYOB / Xero has it** | `Y` if the vendor exposes it, `—` if not |
| **Ledgius has it** | `Y` if the current Ledgius schema stores it, `partial` if stored but incomplete, `—` if absent |
| **Scenario evidence** | Concrete import or export scenario (or compliance citation) that touches this field. Empty ⇒ no scenario yet ⇒ **no action**. |
| **Proposed action** | One of: `none (deferred)` / `add column via VN.NN migration` / `extend existing table` / `deliberately skip (reason)` — with a justification code `J-IMP` / `J-EXP` / `J-COMPLIANCE` / `J-DOMAIN`. |

A blank **Scenario evidence** cell is a signal to **stop** — no action without a scenario.

---

## Entity: Contact (MYOB: Customer / Supplier, Xero: Contact)

Contacts were the first entity analysed because they drive every downstream AR/AP record — incomplete contacts silently corrupt exports (R-0057 validator rule C-003 fails). V1.33 already landed the core fix (structured addresses via `location` + `location_class`, phones, email). The question here is: what's left, and is any of it justified?

| Field (vendor name) | MYOB has it | Xero has it | Ledgius has it | Scenario evidence | Proposed action |
|---|---|---|---|---|---|
| DisplayName / CompanyName | Y | Y | Y (`entity.name`, `contact.name`) | — | **none** — already have |
| FirstName / LastName | Y (via IsIndividual + Names) | Y | Y (`contact.first_name`, `contact.last_name`, post V1.33) | — | **none** — already have |
| Email | Y | Y (`EmailAddress`) | Y (`contact.email`, post V1.33) | — | **none** — already have |
| ABN / tax_number | Y (`TaxNumber`) | Y (`TaxNumber`) | Y (`entity_credit_account.tax_number`) | — | **none** — already have |
| Primary postal address (structured) | Y (`Addresses[0..4]` — 5 slots) | Y (`Addresses[]` with `AddressType`) | Y (via `location` + `location_class`, post V1.33) | — | **none** — Ledgius's structured multi-address model is **superior** to MYOB's fixed 5 slots. |
| Shipping address (distinct from postal) | Y (flat, inferred by slot) | Y (`AddressType=DELIVERY` vs `STREET`) | Y (post V1.33, via `location_class.name='shipping'`) | — | **none** — already first-class. |
| Phone (multiple, typed) | Y (`Phone1..Phone3`) | Y (`Phones[]` with `PhoneType`) | Y (`contact` phones, post V1.33) | — | **none** — already have. |
| **Default sales account** (selling revenue account for this customer) | Y (`SellingDetails.IncomeAccount`) | Y (`SalesDetails.AccountCode`) | — | **J-IMP**: MYOB AO customer exports carry this; without it the invoice-line `account_id` has no per-customer default and every invoice needs manual mapping. | **add column**: `entity_credit_account.default_sales_account_id` FK → `account(id)`, nullable. V1.36 candidate. |
| **Default purchase account** (for suppliers) | Y (`BuyingDetails.ExpenseAccount`) | Y (`PurchasesDetails.AccountCode`) | — | **J-IMP**: MYOB AO supplier exports carry this. | **add column**: `entity_credit_account.default_purchase_account_id` FK → `account(id)`, nullable. V1.36 candidate (same migration). |
| **Default tax code** (per contact) | Y (`SellingDetails.TaxCode` + `BuyingDetails.TaxCode`) | Y (`SalesDetails.TaxType` + `PurchasesDetails.TaxType`) | — | **J-IMP + J-EXP**: MYOB/Xero imports carry it; Xero exports require it if the Ledgius contact has one set. Also reduces invoice-line mapping burden. | **add column**: `entity_credit_account.default_sales_tax_code_id` + `..._purchase_tax_code_id`, both nullable FK → `tax_code(id)`. V1.36 candidate. |
| **Payment terms** (structured: days/EOM/EOM+N) | Y (`SellingDetails.Terms` with `PaymentIsDue`/`BalanceDueDate`/`DiscountDate`) | Y (`PaymentTerms.{Bills,Sales}` with `Day`+`Type`) | partial (`entity_credit_account.payment_terms` is an int) | **J-IMP**: MYOB's structured terms (`EOMOfMonth` + `DiscountPercentage`) don't fit in a single int. Without structure, "due 30 days from end of month" becomes lossy. | **extend**: add `entity_credit_account.payment_terms_type` (enum: `days_after_invoice_date`, `days_after_eom`, `day_of_next_month`, `immediate`) alongside existing int. Keep int as the `N`. Justified by two real import scenarios. |
| Credit limit (monetary) | Y (`SellingDetails.Credit.Limit`) | Y (`SalesDefaults.CreditLimit` — undocumented) | — | — (no scenario in v1 — credit-limit reporting is a v2+ feature per R-0017 scope) | **none (deferred)** — parking until a credit-control feature surfaces. |
| Credit available / past due / on hold | Y (MYOB computes these) | — | — | — | **deliberately skip** — these are **computed**, not stored. MYOB exposes them as denormalised reads; Ledgius computes on demand (J-DOMAIN: no duplication of derived state). |
| IsIndividual flag | Y (MYOB boolean) | — (Xero infers from Name fields) | — | — | **deliberately skip** — Ledgius derives from `first_name IS NOT NULL` — no new column. |
| Notes (free-text) | Y | Y | Y (`entity.description`) | — | **none** — already have. |
| Website URL | Y | Y | — | — (no scenario surfaced yet) | **none (deferred)** — no import/export scenario has flagged this as lossy yet. |
| Industry / BusinessSegment | — | Y (custom field) | — | — | **deliberately skip** — Xero-specific, not load-bearing. |
| RowVersion (optimistic concurrency) | Y | — (Xero uses ETag instead) | — | **J-DOMAIN** (candidate): when Ledgius adds concurrent multi-user edit protection. | **none (deferred)** — concurrency control is a platform-wide concern, not a contact-specific one. Pull into a later architecture ADR. |

### Contact summary — what the analysis recommends

One **V1.36 migration** adds four justified nullable columns to `entity_credit_account`:
- `default_sales_account_id` — J-IMP
- `default_purchase_account_id` — J-IMP
- `default_sales_tax_code_id` — J-IMP + J-EXP
- `default_purchase_tax_code_id` — J-IMP

Plus the `payment_terms_type` enum extension — J-IMP.

Everything else in the MYOB / Xero contact shape either (a) already exists in Ledgius, (b) is deliberately skipped as vendor-idiosyncratic, or (c) is deferred until a real scenario surfaces.

---

## Entities awaiting analysis

The same table structure will be filled in for each of the entities below as import and export work progresses. **Do not pre-fill** rows without scenario evidence — leaving a table empty is a deliberate signal.

| Entity | MYOB catalogue section | Xero catalogue section | Analysis status |
|---|---|---|---|
| Chart of Account | `Account` | `Account` | **pending** — queue after V1.33-V1.35 imports start landing real data. |
| Invoice (AR) | `Sale/Invoice/Item` and friends | `Invoice` + `LineItem` | **partial** — R-0017 FR-025 + V1.34 landed `invoice.account_id` + `invoice.tax_id` driven by J-EXP (Xero export blocker). Remaining line-level fields TBD when an import scenario hits. |
| Bill (AP) | `Purchase/Bill/Item` | (same `Invoice` type, `Type=ACCPAY`) | **pending** — mirror of Invoice analysis. |
| CreditNote | `Sale/CreditNote/*` | `CreditNote` | **partial** — R-0017 FR-026 + V1.35 landed `document_type` via J-EXP. Remaining fields TBD. |
| Payment | `Sale/Payment` + `Purchase/Payment` | `Payment` | **pending** |
| Journal | `GeneralJournal` | `ManualJournal` | **pending** |
| BankTransaction / Transfer | `Banking/SpendMoney` + `ReceiveMoney` + `TransferMoney` | `BankTransaction` + `BankTransfer` | **pending** |
| TaxRate / TaxCode | `GeneralLedger/TaxCode` | `TaxRate` | **pending** |
| Item (inventory / service) | `Inventory/Item` | `Item` | **pending** — out of scope per R-0017 "Inventory on-hand quantity import" exclusion, but structure TBD. |
| Employee / Payroll | `Contact/Employee` + `PayrollDetails` | `Employee` | **pending** — R-0017 scopes payroll to "basic employee records only". |

### How to fill in a pending entity

1. Wait for a real import or export scenario that touches the entity.
2. Identify the specific field(s) that are lossy or blocked.
3. Add a row with J-* justification code.
4. Only *then* propose the schema change.

No pre-emptive filling. No parity-driven columns. If in doubt, leave it out.

---

## Related documents

- `myob/entity-catalogue/PROVENANCE.md` — MYOB catalogue provenance
- `xero/entity-catalogue/PROVENANCE.md` — Xero catalogue provenance
- `../../../import/data-import/import-pipeline/R-0017.md` §*Domain Model Completeness* — the rule this analysis is applied under
- `../../../export/feeds/xero-export/R-0057.md` — Xero export feature that triggered the first batch of completeness migrations
- V1.33 / V1.34 / V1.35 migrations in `ledgius-db/migrations/tenant/` — the schema changes this analysis has already produced
