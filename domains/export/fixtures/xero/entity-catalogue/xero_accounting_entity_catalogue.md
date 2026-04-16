# Xero Accounting Software Entity Catalogue

**Prepared for:** Matt Bush  
**Prepared on:** 2026-04-17 (Australia/Melbourne)  
**Scope:** Public, integration-facing Xero Accounting API entity catalogue. This is **not** a physical database schema dump. Xero exposes an API/domain model rather than a published underlying database design.

## Method and source handling

This catalogue was assembled from:

1. **Official Xero Accounting API endpoint documentation** on developer.xero.com.
2. **Official Xero SDK-generated model sources** from the `XeroAPI/xero-node` repository, which Xero describes as generated from `XeroAPI/Xero-OpenAPI`.

### Important note on source dates

Xero's developer endpoint pages do **not** consistently expose a visible publication/update date in the page body as surfaced here.  
Accordingly:

- where an endpoint page did not expose a publication/update date, this document records **Accessed: 2026-04-17**
- SDK model sources are also recorded as **Accessed: 2026-04-17**
- the broader SDK provenance is current to the public Xero SDK/repository materials surfaced on 2026-04-17

## Coverage

Included below are the Xero Accounting API entities for which I had directly sourced field descriptions from official Xero materials.

---

## Account

**Category:** Settings / General Ledger  
**Entity description:** Chart of accounts record used to represent ledger and bank accounts in Xero.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/accounts  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/account.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `code` | `string` | Customer-defined alphanumeric account code, e.g. 200 or SALES. |
| `name` | `string` | Name of account. |
| `accountID` | `string` | Xero identifier for the account. |
| `type` | `AccountType enum` | Account type. |
| `bankAccountNumber` | `string` | Bank account number for bank accounts only. |
| `status` | `enum` | Account status; ACTIVE accounts can be updated to ARCHIVED. |
| `description` | `string` | Account description; valid for all types except bank accounts. |
| `bankAccountType` | `enum` | Bank account subtype for bank accounts. |
| `currencyCode` | `CurrencyCode enum` | Currency for the account. |
| `taxType` | `string` | Default tax type from tax rates. |
| `enablePaymentsToAccount` | `boolean` | Whether payments can be applied to this account. |
| `showInExpenseClaims` | `boolean` | Whether the account code is available for expense claims. |
| `class` | `enum` | Account class type. |
| `systemAccount` | `enum` | System account type when the account is system-defined. |
| `reportingCode` | `string` | Reporting code, if set. |
| `reportingCodeName` | `string` | Reporting code name, if set. |
| `hasAttachments` | `boolean` | Whether the account has attachments. |
| `updatedDateUTC` | `Date` | Last modified date in UTC. |
| `addToWatchlist` | `boolean` | Whether the account appears in the dashboard watchlist widget. |

---

## Contact

**Category:** Contacts  
**Entity description:** Customer, supplier, or general contact master record used across receivables and payables.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/contacts  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/contact.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `contactID` | `string` | Xero identifier. |
| `mergedToContactID` | `string` | Destination contact when a contact has been merged. |
| `contactNumber` | `string` | External-system identifier shown as Contact Code in the Xero UI. |
| `accountNumber` | `string` | User-defined account number. |
| `contactStatus` | `enum` | Current contact status. |
| `name` | `string` | Full contact or organisation name. |
| `firstName` | `string` | First name of contact person. |
| `lastName` | `string` | Last name of contact person. |
| `companyNumber` | `string` | Company registration number. |
| `emailAddress` | `string` | Email address of the contact person. |
| `contactPersons` | `ContactPerson[]` | Associated contact people. |
| `bankAccountDetails` | `string` | Bank account number/details for the contact. |
| `taxNumber` | `string` | Regional tax number such as ABN, GST, VAT, or Tax ID. |
| `taxNumberType` | `enum` | Regional type of the tax number. |
| `accountsReceivableTaxType` | `string` | Default receivables tax type from TaxRates. |
| `accountsPayableTaxType` | `string` | Default payables tax type from TaxRates. |
| `addresses` | `Address[]` | Stored addresses for the contact. |
| `phones` | `Phone[]` | Stored phone numbers for the contact. |
| `isSupplier` | `boolean` | Automatically indicates whether AP invoices exist for the contact. |
| `isCustomer` | `boolean` | Automatically indicates whether AR invoices exist for the contact. |

---

## Organisation

**Category:** Settings / Tenant  
**Entity description:** Top-level Xero organisation metadata and configuration record.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/organisation  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/organisation.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `organisationID` | `string` | Unique Xero organisation identifier. |
| `APIKey` | `string` | Unique key used for Xero-to-Xero transactions. |
| `name` | `string` | Display name shown in Xero. |
| `legalName` | `string` | Organisation name shown on reports. |
| `paysTax` | `boolean` | Whether the organisation is registered with a local tax authority. |
| `version` | `enum` | Organisation version type. |
| `organisationType` | `enum` | Organisation type. |
| `baseCurrency` | `CurrencyCode enum` | Base currency. |
| `countryCode` | `CountryCode enum` | Country code. |
| `isDemoCompany` | `boolean` | Whether the organisation is a demo company. |
| `organisationStatus` | `string` | ACTIVE when the organisation can be connected via the API. |
| `registrationNumber` | `string` | Registration number for NZ, AU, and UK orgs. |
| `employerIdentificationNumber` | `string` | US EIN when set. |
| `taxNumber` | `string` | Displayed as regional tax number in the Xero UI. |
| `financialYearEndDay` | `number` | Calendar day of financial year end. |
| `financialYearEndMonth` | `number` | Calendar month of financial year end. |
| `salesTaxBasis` | `enum` | Tax-return accounting basis. |
| `salesTaxPeriod` | `enum` | Tax-return filing period/frequency. |
| `defaultSalesTax` | `string` | Default line amount tax behaviour for sales. |
| `defaultPurchasesTax` | `string` | Default line amount tax behaviour for purchases. |
| `periodLockDate` | `string` | Period lock date. |
| `endOfYearLockDate` | `string` | End-of-year lock date. |
| `createdDateUTC` | `Date` | Timestamp when the organisation was created in Xero. |
| `timezone` | `TimeZone enum` | Organisation timezone. |
| `shortCode` | `string` | Short unique identifier for the organisation. |
| `class` | `enum` | Organisation class such as DEMO, TRIAL, PREMIUM. |
| `edition` | `enum` | BUSINESS or PARTNER edition. |
| `lineOfBusiness` | `string` | Business type description from organisation settings. |
| `addresses` | `AddressForOrganisation[]` | Organisation addresses. |
| `phones` | `Phone[]` | Organisation phone details. |

---

## Invoice

**Category:** Sales / Purchases  
**Entity description:** Sales invoice, purchase bill, prepayment, or overpayment transaction depending on the invoice type.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/invoices  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/invoice.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `type` | `enum` | Invoice type, such as ACCREC or ACCPAY. |
| `contact` | `Contact` | Associated contact. |
| `lineItems` | `LineItem[]` | Invoice lines. |
| `date` | `string (YYYY-MM-DD)` | Issue date; defaults to current organisation date when omitted. |
| `dueDate` | `string (YYYY-MM-DD)` | Due date. |
| `lineAmountTypes` | `LineAmountTypes enum` | Tax-inclusive/exclusive line amount behaviour. |
| `invoiceNumber` | `string` | Alpha-numeric invoice number; auto-generated when omitted for ACCREC. |
| `reference` | `string` | Additional reference number. |
| `brandingThemeID` | `string` | Branding theme reference. |
| `url` | `string` | Source document URL shown in Xero as a deep link. |
| `currencyCode` | `CurrencyCode enum` | Invoice currency. |
| `currencyRate` | `number` | Currency rate for multicurrency invoices. |
| `status` | `enum` | Invoice status. |
| `sentToContact` | `boolean` | Whether the invoice is marked as sent in Xero. |
| `expectedPaymentDate` | `string` | Expected payment date for sales invoices. |
| `plannedPaymentDate` | `string` | Planned payment date for bills. |
| `subTotal` | `number` | Total excluding tax. |
| `totalTax` | `number` | Tax total. |
| `total` | `number` | Tax-inclusive total. |
| `totalDiscount` | `number` | Total discounts across invoice lines. |
| `invoiceID` | `string` | Xero-generated invoice identifier. |
| `repeatingInvoiceID` | `string` | Xero identifier for linked repeating invoice. |
| `hasAttachments` | `boolean` | Whether the invoice has attachments. |
| `isDiscounted` | `boolean` | Whether any discount is present. |
| `amountDue` | `number` | Outstanding amount. |
| `amountPaid` | `number` | Payments received. |
| `fullyPaidOnDate` | `string` | Date the invoice was fully paid, when applicable. |
| `amountCredited` | `number` | Total credit, overpayment, and prepayment applied. |
| `updatedDateUTC` | `Date` | Last modified date in UTC. |

---

## LineItem

**Category:** Shared transaction component  
**Entity description:** Reusable transaction line used by invoices, credit notes, purchase orders, and bank transactions.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/invoices  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/lineItem.ts  
- Source date handling: Invoice endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `lineItemID` | `string` | Line item unique ID. |
| `description` | `string` | Line description; at least one character if present alone. |
| `quantity` | `number` | Quantity. |
| `unitAmount` | `number` | Unit amount. |
| `itemCode` | `string` | Referenced inventory item code. |
| `accountCode` | `string` | Referenced chart-of-accounts code. |
| `accountID` | `string` | Associated account ID. |
| `taxType` | `string` | Tax type from TaxRates. |
| `taxAmount` | `number` | Tax amount; normally auto-calculated but may be overridden. |
| `item` | `LineItemItem` | Nested item object. |
| `lineAmount` | `number` | Extended line amount after discounts. |
| `tracking` | `LineItemTracking[]` | Up to two tracking category assignments. |
| `discountRate` | `number` | Percentage discount; supported on ACCREC invoices. |
| `discountAmount` | `number` | Discount amount; supported on ACCREC invoices and quotes. |

---

## Payment

**Category:** Receipts / Settlements  
**Entity description:** Payment or refund allocation applied to an invoice, credit note, prepayment, or overpayment.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/payments  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/payment.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `invoice` | `Invoice` | Invoice the payment applies to. |
| `creditNote` | `CreditNote` | Credit note the payment applies to. |
| `prepayment` | `Prepayment` | Prepayment the payment applies to. |
| `overpayment` | `Overpayment` | Overpayment the payment applies to. |
| `invoiceNumber` | `string` | Invoice number being paid. |
| `creditNoteNumber` | `string` | Credit note number being paid. |
| `batchPayment` | `BatchPayment` | Associated batch payment, if any. |
| `account` | `Account` | Bank or ledger account used for the payment. |
| `code` | `string` | Account code used to make the payment. |
| `date` | `string (YYYY-MM-DD)` | Payment date. |
| `currencyRate` | `number` | Exchange rate for non-base-currency payments. |
| `amount` | `number` | Payment amount; must not exceed the outstanding amount. |
| `bankAmount` | `number` | Payment amount in the bank-account currency. |
| `reference` | `string` | Optional description/reference. |
| `isReconciled` | `boolean` | Whether the payment is or should be reconciled. |
| `status` | `enum` | Payment status. |
| `paymentType` | `enum` | Payment type. |
| `updatedDateUTC` | `Date` | Last update timestamp in UTC. |
| `paymentID` | `string` | Xero payment identifier. |
| `batchPaymentID` | `string` | Batch payment identifier when created in a batch. |

---

## BankTransaction

**Category:** Banking  
**Entity description:** Spend-money, receive-money, transfer, prepayment, or overpayment bank transaction.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/banktransactions  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/bankTransaction.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `type` | `enum` | Bank transaction type. |
| `contact` | `Contact` | Associated contact. |
| `lineItems` | `LineItem[]` | Transaction lines. |
| `bankAccount` | `Account` | Bank account against which the transaction is booked. |
| `isReconciled` | `boolean` | Whether the transaction is reconciled. |
| `date` | `string (YYYY-MM-DD)` | Transaction date. |
| `reference` | `string` | Reference; supported for SPEND and RECEIVE transactions. |
| `currencyCode` | `CurrencyCode enum` | Currency code. |
| `currencyRate` | `number` | Exchange rate to base currency for non-base-currency transactions. |
| `url` | `string` | Source document URL displayed in Xero. |
| `status` | `enum` | Bank transaction status. |
| `lineAmountTypes` | `LineAmountTypes enum` | Line amount tax behaviour. |
| `subTotal` | `number` | Total excluding tax. |
| `totalTax` | `number` | Tax total. |
| `total` | `number` | Tax-inclusive total. |
| `bankTransactionID` | `string` | Xero bank transaction identifier. |
| `prepaymentID` | `string` | Related prepayment ID for prepayment transaction types. |
| `overpaymentID` | `string` | Related overpayment ID for overpayment transaction types. |
| `updatedDateUTC` | `Date` | Last modified date in UTC. |
| `hasAttachments` | `boolean` | Whether the bank transaction has attachments. |

---

## BankTransfer

**Category:** Banking  
**Entity description:** Movement of funds between two bank accounts in Xero.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/banktransfers  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/bankTransfer.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `fromBankAccount` | `Account` | Source bank account. |
| `toBankAccount` | `Account` | Destination bank account. |
| `amount` | `number` | Transfer amount. |
| `date` | `string (YYYY-MM-DD)` | Transfer date. |
| `bankTransferID` | `string` | Bank transfer identifier. |
| `currencyRate` | `number` | Currency rate. |
| `fromBankTransactionID` | `string` | Source-side bank transaction ID. |
| `toBankTransactionID` | `string` | Destination-side bank transaction ID. |
| `fromIsReconciled` | `boolean` | Whether the source-side transaction is reconciled. |
| `toIsReconciled` | `boolean` | Whether the destination-side transaction is reconciled. |
| `reference` | `string` | Reference for the transfer. |
| `hasAttachments` | `boolean` | Whether the bank transfer has attachments. |
| `createdDateUTC` | `Date` | Creation timestamp in UTC. |

---

## Item

**Category:** Inventory / Catalogue  
**Entity description:** Inventory or service item used on sales and purchase transactions.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/items  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/item.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `code` | `string` | User-defined item code. |
| `inventoryAssetAccountCode` | `string` | Inventory asset account code; required for tracked inventory. |
| `name` | `string` | Item name. |
| `isSold` | `boolean` | Whether the item is available on sales transactions. |
| `isPurchased` | `boolean` | Whether the item is available on purchase transactions. |
| `description` | `string` | Sales description. |
| `purchaseDescription` | `string` | Purchase description. |
| `purchaseDetails` | `Purchase` | Purchase defaults/details. |
| `salesDetails` | `Purchase` | Sales defaults/details. |
| `isTrackedAsInventory` | `boolean` | Whether the item is tracked as inventory. |
| `totalCostPool` | `number` | Value of item on hand using average cost. |
| `quantityOnHand` | `number` | Current quantity on hand. |
| `updatedDateUTC` | `Date` | Last modified date in UTC. |
| `itemID` | `string` | Xero item identifier. |
| `statusAttributeString` | `string` | Object status string. |

---

## TrackingCategory

**Category:** Analysis / Dimensions  
**Entity description:** User-defined analysis dimension such as Department or Region.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/trackingcategories  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/trackingCategory.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `trackingCategoryID` | `string` | Tracking category identifier. |
| `trackingOptionID` | `string` | Tracking option identifier. |
| `name` | `string` | Tracking category name, e.g. Department or Region. |
| `option` | `string` | Option name, e.g. East or West. |
| `status` | `enum` | Tracking category status. |
| `options` | `TrackingOption[]` | Tracking options within the category. |

---

## TrackingOption

**Category:** Analysis / Dimensions  
**Entity description:** Selectable option within a tracking category.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/trackingcategories  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/trackingOption.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `trackingOptionID` | `string` | Tracking option identifier. |
| `name` | `string` | Tracking option name. |
| `status` | `enum` | Tracking option status. |
| `trackingCategoryID` | `string` | Parent tracking category identifier. |

---

## TaxRate

**Category:** Tax settings  
**Entity description:** Tax code/rate definition used on accounts and transaction lines.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/taxrates  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/taxRate.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `name` | `string` | Name of tax rate. |
| `taxType` | `string` | Tax type code. |
| `taxComponents` | `TaxComponent[]` | Constituent tax components. |
| `status` | `enum` | Tax rate status. |
| `reportTaxType` | `enum` | Reporting tax type. |
| `canApplyToAssets` | `boolean` | Whether the rate can be used on asset accounts. |
| `canApplyToEquity` | `boolean` | Whether the rate can be used on equity accounts. |
| `canApplyToExpenses` | `boolean` | Whether the rate can be used on expense accounts. |
| `canApplyToLiabilities` | `boolean` | Whether the rate can be used on liability accounts. |
| `canApplyToRevenue` | `boolean` | Whether the rate can be used on revenue accounts. |
| `displayTaxRate` | `number` | Display tax rate to 4 decimal places. |
| `effectiveRate` | `number` | Effective tax rate to 4 decimal places. |

---

## Journal

**Category:** General Ledger  
**Entity description:** Posted journal entry generated by source transactions or manual journals.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/journals  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/journal.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `journalID` | `string` | Xero journal identifier. |
| `journalDate` | `string` | Date the journal was posted. |
| `journalNumber` | `number` | Xero-generated journal number. |
| `createdDateUTC` | `Date` | Created date in UTC. |
| `reference` | `string` | Additional identifying reference. |
| `sourceID` | `string` | Identifier for the source transaction, such as InvoiceID. |
| `sourceType` | `enum` | Type of source transaction that created the journal. |
| `journalLines` | `JournalLine[]` | Journal lines. |

---

## ManualJournal

**Category:** General Ledger  
**Entity description:** User-authored journal posted directly through the manual journals endpoint.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/manualjournals  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/manualJournal.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `narration` | `string` | Description of the journal being posted. |
| `journalLines` | `ManualJournalLine[]` | Manual journal lines. |
| `date` | `string (YYYY-MM-DD)` | Posting date. |
| `lineAmountTypes` | `LineAmountTypes enum` | Line amount tax behaviour. |
| `status` | `enum` | Manual journal status. |
| `url` | `string` | Source document deep link displayed in Xero. |
| `showOnCashBasisReports` | `boolean` | Whether the journal appears on cash-basis reports. |
| `hasAttachments` | `boolean` | Whether the journal has attachments. |
| `updatedDateUTC` | `Date` | Last modified date in UTC. |
| `manualJournalID` | `string` | Manual journal identifier. |
| `statusAttributeString` | `string` | Status string. |
| `warnings` | `Warning[]` | Warnings returned by the API. |
| `validationErrors` | `ValidationError[]` | Validation errors returned by the API. |
| `attachments` | `Attachment[]` | Attachments returned by the API. |

---

## CreditNote

**Category:** Sales / Purchases  
**Entity description:** Receivable or payable credit note that can be allocated against invoices and settled by payments.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/creditnotes  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/creditNote.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `type` | `enum` | Credit note type, e.g. ACCRECCREDIT or ACCPAYCREDIT. |
| `contact` | `Contact` | Associated contact. |
| `date` | `string (YYYY-MM-DD)` | Issue date; defaults to current organisation date when omitted. |
| `dueDate` | `string (YYYY-MM-DD)` | Due date. |
| `status` | `enum` | Credit note status. |
| `lineAmountTypes` | `LineAmountTypes enum` | Line amount tax behaviour. |
| `lineItems` | `LineItem[]` | Credit note lines. |
| `subTotal` | `number` | Total excluding tax. |
| `totalTax` | `number` | Tax total. |
| `total` | `number` | Tax-inclusive total. |
| `updatedDateUTC` | `Date` | Last update timestamp in UTC. |
| `currencyCode` | `CurrencyCode enum` | Currency code. |
| `fullyPaidOnDate` | `string` | Date the credit note was fully paid. |
| `creditNoteID` | `string` | Xero credit note identifier. |
| `creditNoteNumber` | `string` | Credit note number. |
| `reference` | `string` | Additional reference number. |
| `sentToContact` | `boolean` | Whether the credit note is marked as sent. |
| `currencyRate` | `number` | Currency rate for multicurrency credit notes. |
| `remainingCredit` | `number` | Remaining available credit. |
| `allocations` | `Allocation[]` | Allocations against invoices. |
| `appliedAmount` | `number` | Amount applied to invoices. |
| `payments` | `Payment[]` | Payments recorded against the credit note. |
| `brandingThemeID` | `string` | Branding theme reference. |
| `hasAttachments` | `boolean` | Whether the credit note has attachments. |

---

## PurchaseOrder

**Category:** Purchasing  
**Entity description:** Procurement document issued to a supplier before billing.  
**Sources:**  
- Endpoint: https://developer.xero.com/documentation/api/accounting/purchaseorders  
- SDK model: https://raw.githubusercontent.com/XeroAPI/xero-node/refs/heads/master/src/gen/model/accounting/purchaseOrder.ts  
- Source date handling: Endpoint page date not exposed in page body; accessed 2026-04-17. SDK model accessed 2026-04-17.

| Field | Type | Description |
|---|---|---|
| `contact` | `Contact` | Supplier/contact. |
| `lineItems` | `LineItem[]` | Purchase order lines. |
| `date` | `string (YYYY-MM-DD)` | Issue date; defaults to current organisation date when omitted. |
| `deliveryDate` | `string (YYYY-MM-DD)` | Requested delivery date. |
| `lineAmountTypes` | `LineAmountTypes enum` | Line amount tax behaviour. |
| `purchaseOrderNumber` | `string` | Unique alphanumeric purchase order number. |
| `reference` | `string` | Additional reference number. |
| `brandingThemeID` | `string` | Branding theme reference. |
| `currencyCode` | `CurrencyCode enum` | Currency code. |
| `status` | `enum` | Purchase order status. |
| `sentToContact` | `boolean` | Whether the purchase order is marked as sent. |
| `deliveryAddress` | `string` | Delivery address. |
| `attentionTo` | `string` | Delivery addressee. |
| `telephone` | `string` | Telephone number for delivery contact. |
| `deliveryInstructions` | `string` | Free-text delivery instructions. |

---

## Consolidated source provenance

- Xero Accounting API overview: https://developer.xero.com/documentation/api/accounting/overview
- Xero Developer platform home: https://developer.xero.com/
- Official Node SDK repository: https://github.com/XeroAPI/xero-node
- SDK-generated Accounting API docs: https://xeroapi.github.io/xero-node/accounting/index.html

## Practical interpretation

This document is best treated as:

- an **integration schema catalogue**
- a **Go-struct mapping aid**
- an **ERD starting point** for an application that synchronises with Xero

It should **not** be treated as proof of Xero's internal relational database layout.
