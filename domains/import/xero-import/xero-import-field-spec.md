# Xero Import — CSV Field Specification

This document describes the CSV column structure for importing data from Xero into Ledgius. Each entity type has a dedicated CSV file with specific column headers matching Xero's CSV import/export template format.

**Import order:** Accounts → Tax Codes → Contacts → Invoices → Bills → Credit Notes

---

## 1. Contacts

**File type:** `contacts`
**Direction:** Xero → Ledgius

| # | CSV Column | Required | Data Type | Ledgius Staging Field | Description | Example |
|---|---|---|---|---|---|---|
| 1 | `Name` | Yes | string (255) | `source_name` | Contact display name. Must be unique within the Xero org. | `Acme Supplies Pty Ltd` |
| 2 | `FirstName` | No | string | _(raw data only)_ | First name of a person contact. | `Jane` |
| 3 | `LastName` | No | string | _(raw data only)_ | Last name of a person contact. | `Smith` |
| 4 | `EmailAddress` | No | string | `source_email` | Primary email address. | `jane@acme.com.au` |
| 5 | `IsCustomer` | No | boolean | `source_type` | Whether this contact appears on sales invoices. | `TRUE` |
| 6 | `IsSupplier` | No | boolean | `source_type` | Whether this contact appears on bills. Both can be true. | `FALSE` |
| 7 | `TaxNumber` | No | string | `source_abn` | Australian Business Number (ABN) or equivalent. | `51 824 753 556` |
| 8 | `POAddressLine1` | No | string | _(raw data)_ | Postal address line 1. | `123 George St` |
| 9 | `POAddressLine2` | No | string | _(raw data)_ | Postal address line 2. | `Level 5` |
| 10 | `POAddressCity` | No | string | _(raw data)_ | City or suburb. | `Sydney` |
| 11 | `POAddressRegion` | No | string | _(raw data)_ | State or region. | `NSW` |
| 12 | `POAddressPostalCode` | No | string | _(raw data)_ | Postal code. | `2000` |
| 13 | `POAddressCountry` | No | string | _(raw data)_ | Country. Defaults to "Australia" if blank. | `Australia` |

**Notes:**
- A contact can be both a customer AND a supplier (both flags true).
- Duplicate detection uses Name + TaxNumber.

---

## 2. Invoices (Sales)

**File type:** `invoices`
**Direction:** Xero → Ledgius
**Row level:** One row per **line item**. Multiple rows with the same `InvoiceNumber` belong to the same invoice.

| # | CSV Column | Required | Data Type | Ledgius Staging Field | Description | Example |
|---|---|---|---|---|---|---|
| 1 | `Type` | Yes | enum | `source_type` | Always `ACCREC` for sales invoices. | `ACCREC` |
| 2 | `Status` | No | enum | `source_status` | Document status. See status mapping below. | `AUTHORISED` |
| 3 | `ContactName` | Yes | string (255) | `source_contact` | Customer display name. Must match an existing contact. | `Acme Supplies Pty Ltd` |
| 4 | `InvoiceNumber` | Yes | string (255) | `source_number` | Unique invoice number. Repeated across lines of the same invoice. | `INV-0042` |
| 5 | `Reference` | No | string | `source_reference` | Customer PO number or free-form reference. | `PO-2026-115` |
| 6 | `InvoiceDate` | No | date | `source_date` | Issue date in `DD/MM/YYYY` format. | `25/04/2026` |
| 7 | `DueDate` | No | date | `source_due_date` | Payment due date in `DD/MM/YYYY` format. | `25/05/2026` |
| 8 | `Currency` | No | string (3) | `source_currency` | Three-letter ISO currency code. | `AUD` |
| 9 | `LineDescription` | No | string (4000) | `source_description` | Description for this line item. | `Consulting services — April` |
| 10 | `Quantity` | No | number | `source_quantity` | Line quantity. Defaults to 1 if blank. | `2` |
| 11 | `UnitAmount` | No | number (2dp) | `source_unit_amount` | Unit price for this line. | `150.00` |
| 12 | `AccountCode` | No | string (10) | `source_account_code` | Xero account code this line posts to. | `200` |
| 13 | `TaxType` | No | string | `source_tax_type` | Xero tax display name. See tax mapping below. | `GST on Income` |
| 14 | `InventoryItemCode` | No | string | `source_inventory_item` | Optional Xero inventory item code. | `CONSULT-HR` |

---

## 3. Bills (Purchases)

**File type:** `bills`
**Direction:** Xero → Ledgius
**Row level:** One row per **line item**. Multiple rows with the same `InvoiceNumber` belong to the same bill.

| # | CSV Column | Required | Data Type | Ledgius Staging Field | Description | Example |
|---|---|---|---|---|---|---|
| 1 | `Type` | Yes | enum | `source_type` | Always `ACCPAY` for purchase bills. | `ACCPAY` |
| 2 | `Status` | No | enum | `source_status` | Document status. See status mapping below. | `DRAFT` |
| 3 | `ContactName` | Yes | string (255) | `source_contact` | Supplier display name. Must match an existing contact. | `Office Warehouse` |
| 4 | `InvoiceNumber` | Yes | string (255) | `source_number` | Supplier's invoice/bill number. | `BILL-0017` |
| 5 | `Reference` | No | string | `source_reference` | Internal reference or supplier quote number. | `Q-4421` |
| 6 | `Date` | No | date | `source_date` | Bill date in `DD/MM/YYYY` format. | `20/04/2026` |
| 7 | `DueDate` | No | date | `source_due_date` | Payment due date in `DD/MM/YYYY` format. | `20/05/2026` |
| 8 | `Currency` | No | string (3) | `source_currency` | Three-letter ISO currency code. | `AUD` |
| 9 | `Description` | No | string (4000) | `source_description` | Description for this line item. | `Printer paper A4 — 10 reams` |
| 10 | `Quantity` | No | number | `source_quantity` | Line quantity. Defaults to 1 if blank. | `10` |
| 11 | `UnitAmount` | No | number (2dp) | `source_unit_amount` | Unit price for this line. | `8.50` |
| 12 | `AccountCode` | No | string (10) | `source_account_code` | Xero expense account code. | `400` |
| 13 | `TaxType` | No | string | `source_tax_type` | Xero tax display name. See tax mapping below. | `GST on Expenses` |

**Note:** The date column for bills is `Date` (not `InvoiceDate` as used for sales invoices). This matches Xero's own CSV template convention.

---

## 4. Credit Notes

**File type:** `credit_notes`
**Direction:** Xero → Ledgius
**Row level:** One row per **line item**. Multiple rows with the same `CreditNoteNumber` belong to the same credit note.

| # | CSV Column | Required | Data Type | Ledgius Staging Field | Description | Example |
|---|---|---|---|---|---|---|
| 1 | `Type` | Yes | enum | `source_type` | `ACCRECCREDIT` (sales credit note) or `ACCPAYCREDIT` (purchase credit note). | `ACCRECCREDIT` |
| 2 | `Status` | No | enum | `source_status` | Document status. See status mapping below. | `AUTHORISED` |
| 3 | `ContactName` | Yes | string (255) | `source_contact` | Contact display name (customer or supplier depending on type). | `Acme Supplies Pty Ltd` |
| 4 | `CreditNoteNumber` | Yes | string (255) | `source_number` | Unique credit note number. Separate namespace from invoices/bills. | `CN-0005` |
| 5 | `Reference` | No | string | `source_reference` | Internal or external reference. | `Ref invoice INV-0042` |
| 6 | `Date` | No | date | `source_date` | Issue date in `DD/MM/YYYY` format. | `26/04/2026` |
| 7 | `Currency` | No | string (3) | `source_currency` | Three-letter ISO currency code. | `AUD` |
| 8 | `LineDescription` | No | string (4000) | `source_description` | Description for this line item. | `Returned goods — damaged` |
| 9 | `Quantity` | No | number | `source_quantity` | Line quantity. Defaults to 1 if blank. | `1` |
| 10 | `UnitAmount` | No | number (2dp) | `source_unit_amount` | Unit amount for this line. | `50.00` |
| 11 | `AccountCode` | No | string (10) | `source_account_code` | Xero account code this line posts to. | `200` |
| 12 | `TaxType` | No | string | `source_tax_type` | Xero tax display name. See tax mapping below. | `GST on Income` |

**Note:** Credit notes do NOT have a `DueDate` column — only a single `Date`.

---

## Tax Type Mapping (All Entities)

Xero uses display names for tax types. These are mapped to Ledgius tax codes during import:

| Xero TaxType | Ledgius Tax Code | GST Rate | BAS Reporting |
|---|---|---|---|
| `GST on Income` | GST | 10% | G1 — Total sales |
| `GST on Expenses` | GST | 10% | G11 — Non-capital purchases |
| `GST on Capital` | GST | 10% | G10 — Capital acquisitions |
| `GST Free Income` | FRE | 0% | G3 — GST-free sales |
| `GST Free Expenses` | FRE | 0% | G3 |
| `Input Taxed` | INP | 0% | G4 — Input taxed sales |
| `BAS Excluded` | N-T | 0% | Not reported on BAS |
| _(empty)_ | N-T | 0% | Not reported on BAS |

**Fallback:** Any unrecognised tax type defaults to `N-T` (BAS Excluded).

---

## Status Mapping (Invoices, Bills, Credit Notes)

| Xero Status | Ledgius Status | Meaning |
|---|---|---|
| `DRAFT` | draft | Editable, not posted to ledger |
| `SUBMITTED` | draft | Xero approval workflow — treated as draft |
| `AUTHORISED` | posted | Posted to ledger, not yet paid |
| `PAID` | paid | Fully settled |
| `VOIDED` | voided | Cancelled (invoices only) |

**Fallback:** Any unrecognised status defaults to `draft`.

---

## Type Codes Reference

| Type Code | Entity | Direction |
|---|---|---|
| `ACCREC` | Sales Invoice | Accounts Receivable |
| `ACCPAY` | Purchase Bill | Accounts Payable |
| `ACCRECCREDIT` | Sales Credit Note | Credit against customer |
| `ACCPAYCREDIT` | Purchase Credit Note | Credit against supplier |
