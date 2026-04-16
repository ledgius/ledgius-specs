# MYOB Business API Entity Catalogue
_A public, integration-facing schema catalogue derived from official MYOB Business API endpoint documentation._

**Prepared for:** Matt Bush  
**Prepared on:** 2026-04-17 (Australia/Melbourne)  
**Scope:** This is **not** a physical MYOB database schema dump. It is a catalogue of **public MYOB Business API entities and fields** that were explicitly described in the official source materials retrieved for this document.  
**Method note:** For very large entities, nested structures are shown with dot notation (for example `Addresses[].Street` or `SellingDetails.TaxCode.Code`).

---

## Citation and source-date convention

Each entity section includes:

- the official endpoint page used as source
- the page’s own **Date Released** and **Date Updated** values as published by MYOB
- a source reference code such as **[S1]**

A consolidated source list appears at the end.

---

## 1) Customer [S1]

**Entity summary:** Customer contact entity used for sales/contact management.  
**Source material date:** Released **Aug 2013**; Updated **Jan 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique customer contact identifier. Required for updates; not required for create. |
| CompanyName | String (50) | Company name of the customer contact. Required when creating a company contact where `IsIndividual=false`. |
| LastName | String (30) | Last name for an individual contact. |
| FirstName | String (20) | First name for an individual contact. |
| IsIndividual | Boolean | `true` for an individual customer; `false` for a company. |
| DisplayID | String (15) | Customer contact card ID. |
| IsActive | Boolean | Whether the customer contact is active. |
| Addresses[].Location | Integer | Address location slot; one contact can have up to five address records. |
| Addresses[].Street | String (255) | Full content of address field. |
| Addresses[].City | String (255) | City of address record. |
| Addresses[].State | String (255) | State of address record. |
| Addresses[].PostCode | String (11) | Postcode of address record. |
| Addresses[].Country | String (255) | Country of address record. |
| Addresses[].Phone1 | String (21) | Phone number 1 for the address. |
| Addresses[].Phone2 | String (21) | Phone number 2 for the address. |
| Addresses[].Phone3 | String (21) | Phone number 3 for the address. |
| Addresses[].Fax | String (21) | Fax number for the address. |
| Addresses[].Email | String (255) | Email address for the address record. |
| Addresses[].Website | String (255) | Website for the contact. |
| Addresses[].ContactName | String (25) | Contact name on the address record. |
| Addresses[].Salutation | String (15) | Salutation text for the address record. |
| Notes | String (255) | Notes for the customer contact. |
| Identifiers[].Label | String (30) | AccountRight-only identifier label. |
| Identifiers[].Value | String | AccountRight-only identifier value. |
| CustomList1..3.Label | String (30) | AccountRight-only custom list label. |
| CustomList1..3.Value | String (30) | AccountRight-only custom list value. |
| CustomField1..3.Label | String (30) | AccountRight-only custom field label. |
| CustomField1..3.Value | String (30) | AccountRight-only custom field value. |
| CurrentBalance | Decimal (13.6) | Customer contact balance. |
| SellingDetails.SaleLayout | SaleLayoutType | Default sale layout: `NoDefault`, `Service`, `Item`, `Professional`, `TimeBilling`, `Miscellaneous`. |
| SellingDetails.PrintedForm | String (255) | Default printed form. |
| SellingDetails.InvoiceDelivery | String (255) | Default invoice delivery status. |
| SellingDetails.ItemPriceLevel | String | Item price level: `Level A` .. `Level F`. |
| SellingDetails.IncomeAccount.UID | Guid (36) | Linked income account identifier. |
| SellingDetails.IncomeAccount.Name | String (30) | Linked income account name. |
| SellingDetails.IncomeAccount.DisplayID | String (6) | Linked income account code. |
| SellingDetails.IncomeAccount.URI | String | Linked income account URI. |
| SellingDetails.ReceiptMemo | String (255) | Default receipt memo. |
| SellingDetails.SalesPerson.UID | Guid (36) | Linked employee contact identifier. |
| SellingDetails.SalesPerson.Name | String (30) | Selected employee contact name. |
| SellingDetails.SalesPerson.DisplayID | String (15) | Employee contact card ID. |
| SellingDetails.SalesPerson.URI | String | Employee contact URI. |
| SellingDetails.SaleComment | String (255) | Default sale comment. |
| SellingDetails.ShippingMethod | String (255) | Shipping method text. |
| SellingDetails.HourlyBillingRate | Decimal (10.6) | Customer hourly billing rate. |
| SellingDetails.ABN | String (14) | AU only. ABN number. |
| SellingDetails.ABNBranch | String (11) | AU only. ABN branch number. |
| SellingDetails.TaxCode.UID | Guid (36) | Linked tax code identifier. |
| SellingDetails.TaxCode.Code | String (3) | Linked tax code. |
| SellingDetails.TaxCode.URI | String | Linked tax code URI. |
| SellingDetails.FreightTaxCode.UID | Guid (36) | Linked freight tax code identifier. |
| SellingDetails.FreightTaxCode.Code | String (3) | Linked freight tax code. |
| SellingDetails.FreightTaxCode.URI | String | Linked freight tax code URI. |
| SellingDetails.UseCustomerTaxCode | Boolean | Whether to use the customer tax code. |
| SellingDetails.Terms.PaymentIsDue | String | Payment term mode: `CashOnDelivery`, `PrePaid`, `InAGivenNumberOfDays`, `OnADayOfTheMonth`, `NumberOfDaysAfterEOM`, `DayOfMonthAfterEOM`. |
| SellingDetails.Terms.DiscountDate | Integer | Discount date/day depending on `PaymentIsDue`. |
| SellingDetails.Terms.BalanceDueDate | Integer | Balance due date/day depending on `PaymentIsDue`. |
| SellingDetails.Terms.DiscountForEarlyPayment | Double (99.99%) | Early payment discount percentage. |
| SellingDetails.Terms.MonthlyChargeForLatePayment | Double (99.99%) | Monthly late-payment charge percentage. |
| SellingDetails.Terms.VolumeDiscount | Double (99.99%) | Volume discount percentage. |
| SellingDetails.Credit.Limit | Decimal (13.6) | Customer credit limit. |
| SellingDetails.Credit.Available | Decimal (13.6) | Available customer credit. |
| SellingDetails.Credit.PastDue | Decimal (13.6) | Customer past-due balance. |
| SellingDetails.Credit.OnHold | Boolean | Whether the customer is on credit hold. |
| SellingDetails.TaxIdNumber | String (19) | Tax ID number. |
| SellingDetails.Memo | String (255) | Default memo text. |
| PaymentDetails.Method | PaymentMethod | Default payment method. |
| PaymentDetails.CardNumber | String (4) | Last 4 digits only. |
| PaymentDetails.NameOnCard | String (50) | Default name on card. |
| PaymentDetails.BSBNumber | String (7) | AU only. Default bank account BSB number. |
| PaymentDetails.BankAccountNumber | String (9) | Default bank account number. |
| PaymentDetails.BankAccountName | String (32) | Default bank account name. |
| PaymentDetails.Notes | String (255) | Default payment notes. |
| ForeignCurrency.UID | Guid (36) | AccountRight-only linked currency identifier. |
| ForeignCurrency.Code | String (3) | AccountRight-only currency code. |
| ForeignCurrency.CurrencyName | String | AccountRight-only currency name. |
| ForeignCurrency.URI | String | AccountRight-only currency URI. |
| LastModified | DateTime | Last modification date for the customer resource. |
| PhotoURI | String | AccountRight-only photo URI. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 2) Supplier [S2]

**Entity summary:** Supplier contact entity used for purchases/contact management.  
**Source material date:** Released **Dec 2013**; Updated **Apr 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique supplier contact identifier. Required for updates; not required for create. |
| CompanyName | String (50) | Company name of the supplier contact. |
| LastName | String (30) | Last name for an individual contact. |
| FirstName | String (20) | First name for an individual contact. |
| IsIndividual | Boolean | `true` for an individual supplier; `false` for a company. |
| DisplayID | String (15) | Supplier contact card ID. |
| IsActive | Boolean | Whether the supplier contact is active. |
| Addresses[].Location | Integer | Address location slot; one contact can have up to five address records. |
| Addresses[].Street | String (255) | Full content of address field. |
| Addresses[].City | String (255) | City of address record. |
| Addresses[].State | String (255) | State of address record. |
| Addresses[].PostCode | String (11) | Postcode of address record. |
| Addresses[].Country | String (255) | Country of address record. |
| Addresses[].Phone1 | String (21) | Phone number 1 for the address. |
| Addresses[].Phone2 | String (21) | Phone number 2 for the address. |
| Addresses[].Phone3 | String (21) | Phone number 3 for the address. |
| Addresses[].Fax | String (21) | Fax number for the address. |
| Addresses[].Email | String (255) | Email for the address record. |
| Addresses[].Website | String (255) | Website for the contact. |
| Addresses[].ContactName | String (25) | Contact name on the address record. |
| Addresses[].Salutation | String (15) | Salutation text for the address record. |
| Notes | String (255) | Notes for the supplier contact. |
| CurrentBalance | Decimal (13.6) | Supplier contact balance. |
| BuyingDetails.PurchaseLayout | PurchaseLayoutType | Default purchase layout: `NoDefault`, `Service`, `Item`, `Professional`, `Miscellaneous`. |
| BuyingDetails.PrintedForm | String (255) | Default printed form. |
| BuyingDetails.PurchaseOrderDelivery | String (20) | Default purchase order delivery status. |
| BuyingDetails.ExpenseAccount.UID | Guid (36) | Linked expense account identifier. |
| BuyingDetails.ExpenseAccount.Name | String (60) | Linked expense account name. |
| BuyingDetails.ExpenseAccount.DisplayID | String (6) | Linked expense account code. |
| BuyingDetails.ExpenseAccount.URI | String | Linked expense account URI. |
| BuyingDetails.PaymentMemo | String (255) | Default payment memo. |
| BuyingDetails.PurchaseComment | String (255) | Default purchase comment. |
| BuyingDetails.SupplierBillingRate | Decimal (10.6) | Supplier hourly billing rate exclusive of tax. |
| BuyingDetails.ShippingMethod | String (255) | Shipping method text. |
| BuyingDetails.IsReportable | Boolean | AU only. Indicates reportable taxable payment setup. |
| BuyingDetails.CostPerHour | Decimal (13.6) | Supplier service cost per hour. |
| BuyingDetails.Credit.Limit | Decimal (13.6) | Supplier credit limit. |
| BuyingDetails.Credit.Available | Decimal (13.6) | Supplier credit available. |
| BuyingDetails.Credit.PastDue | Decimal (13.6) | Supplier past-due balance. |
| BuyingDetails.ABN | String (14) | AU only. ABN number. |
| BuyingDetails.ABNBranch | String (11) | AU only. ABN branch number. |
| BuyingDetails.TaxIdNumber | String (19) | Tax ID number. |
| BuyingDetails.TaxCode.UID | Guid (36) | Linked tax code identifier. |
| BuyingDetails.TaxCode.Code | String (3) | Linked tax code. |
| BuyingDetails.TaxCode.URI | String | Linked tax code URI. |
| BuyingDetails.FreightTaxCode.UID | Guid (36) | Linked freight tax code identifier. |
| BuyingDetails.FreightTaxCode.Code | String (3) | Linked freight tax code. |
| BuyingDetails.FreightTaxCode.URI | String | Linked freight tax code URI. |
| BuyingDetails.UseSupplierTaxCode | Boolean | Whether to use the supplier tax code. |
| BuyingDetails.Terms.PaymentIsDue | String | Payment term mode. |
| BuyingDetails.Terms.DiscountDate | Integer | Discount date/day depending on `PaymentIsDue`. |
| BuyingDetails.Terms.BalanceDueDate | Integer | Balance due date/day depending on `PaymentIsDue`. |
| BuyingDetails.Terms.DiscountForEarlyPayment | Double (99.99%) | Early payment discount percentage. |
| BuyingDetails.Terms.VolumeDiscount | Double (99.99%) | Volume discount percentage. |
| PaymentDetails.BSBNumber | String (6) | AU only. Default bank account BSB number. |
| PaymentDetails.BankAccountNumber | String (9) | Default bank account number; NZ formatting rules apply where relevant. |
| PaymentDetails.BankAccountName | String (32) | Default bank account name. |
| PaymentDetails.StatementText | String (18) | AU only. Default statement text. |
| PaymentDetails.StatementCode | String | NZ only. Default statement code. |
| PaymentDetails.StatementReference | String | NZ only. Default statement reference. |
| PaymentDetails.Refund.PaymentMethod | PaymentMethod | Default refund payment method. |
| PaymentDetails.Refund.CardNumber | String (4) | Last 4 digits only. |
| PaymentDetails.Refund.NameOnCard | String (50) | Default name on card. |
| PaymentDetails.Refund.Notes | String (255) | Default refund notes. |
| ForeignCurrency.UID | Guid (36) | AccountRight-only linked currency identifier. |
| ForeignCurrency.Code | String (3) | AccountRight-only currency code. |
| ForeignCurrency.CurrencyName | String | AccountRight-only currency name. |
| ForeignCurrency.URI | String | AccountRight-only currency URI. |
| LastModified | DateTime | Last modification date for the supplier resource. |
| PhotoURI | String | AccountRight-only photo URI. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 3) EmployeePaymentDetails [S3]

**Entity summary:** Australian employee payment details, especially for electronic payroll payment setup.  
**Source material date:** Released **Aug 2014**; Updated **Dec 2020**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique employee payment details identifier. Required for updates. |
| Employee.UID | Guid (36) | Linked employee contact identifier. |
| Employee.Name | String (30) | Employee name. |
| Employee.DisplayID | String (15) | Employee contact card ID. |
| Employee.URI | String | Employee contact URI. |
| PaymentMethod | String | Payment method enum: `Cash`, `Cheque`, `Electronic` (AU only). |
| BankStatementText | String (18) | Statement text shown where `PaymentMethod=Electronic`. |
| BankAccounts[].BSBNumber | String (6) | Required for electronic payment updates; format like `123-456`. |
| BankAccounts[].BankAccountNumber | String (9) | Required for electronic payment updates. |
| BankAccounts[].BankAccountName | String (32) | Required for electronic payment updates. |
| BankAccounts[].Value | Double | Net pay transfer amount using Dollars or Percent. |
| BankAccounts[].Unit | String | Enum: `Percent`, `Dollars`, `RemainingAmount` (read-only for final account). |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 4) Invoice [S4]

**Entity summary:** Sales invoice entity covering multiple invoice layouts/types.  
**Source material date:** Released **Aug 2013**; Updated **Jan 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique sale invoice identifier. |
| Number | String (13) | Sales invoice number. |
| Date | DateTime | Transaction date. |
| CustomerPurchaseOrderNumber | String (255) | Customer PO number. |
| Customer.UID | Guid (36) | Linked customer identifier. |
| Customer.Name | String (50) | Customer name. |
| Customer.DisplayID | String (15) | Customer card ID. |
| Customer.URI | String | Customer URI. |
| PromisedDate | DateTime | Promised transaction date. |
| BalanceDueAmount | Decimal (13.2) | Amount still payable. |
| BalanceDueAmountForeign | Decimal (13.2) | Foreign-currency balance still payable. |
| Status | String | Invoice status: `Open`, `Closed`, `Credit`. |
| ShipToAddress | String (255) | Ship-to address text. |
| Terms.PaymentIsDue | String | Payment term mode. |
| Terms.DiscountDate | Integer | Discount date/day depending on term mode. |
| Terms.BalanceDueDate | Integer | Due date/day depending on term mode. |
| Terms.DiscountForEarlyPayment | Double (99.99%) | Early payment discount percentage. |
| Terms.MonthlyChargeForLatePayment | Double (99.99%) | Monthly late-payment charge percentage. |
| Terms.DiscountExpiryDate | DateTime | Deadline to receive discount. |
| Terms.Discount | Decimal (13.2) | Discount amount in local currency. |
| Terms.DiscountForeign | Decimal (13.2) | Discount amount in foreign currency. |
| Terms.DueDate | DateTime | Payment due date. |
| Terms.FinanceCharge | Decimal (13.2) | Late-payment finance charge. |
| Terms.FinanceChargeForeign | Decimal (13.2) | Late-payment finance charge in foreign currency. |
| IsTaxInclusive | Boolean | Whether the transaction is tax-inclusive. |
| Subtotal | Decimal (13.2) | Line subtotal. |
| SubtotalForeign | Decimal (13.2) | Foreign-currency subtotal. |
| Freight | Decimal (13.2) | Freight amount. |
| FreightForeign | Decimal (13.2) | Foreign-currency freight amount. |
| FreightTaxCode.UID | Guid (36) | Linked freight tax code identifier. |
| FreightTaxCode.Code | String (3) | Linked freight tax code. |
| FreightTaxCode.URI | String | Linked freight tax code URI. |
| TotalTax | Decimal (13.2) | Total tax. |
| TotalTaxForeign | Decimal (13.2) | Foreign-currency total tax. |
| TotalAmount | Decimal (13.2) | Total invoice amount. |
| TotalAmountForeign | Decimal (13.2) | Foreign-currency total amount. |
| Category.UID | Guid (36) | Linked category identifier. |
| Category.Name | String (30) | Linked category name. |
| Category.DisplayID | String (15) | Linked category display ID. |
| Category.URI | String | Linked category URI. |
| Salesperson.UID | Guid (36) | Linked employee/salesperson identifier. |
| Salesperson.Name | String (30) | Salesperson name. |
| Salesperson.DisplayID | String (15) | Salesperson card ID. |
| Salesperson.URI | String | Salesperson URI. |
| Comment | String (2000) | Sale invoice comment. |
| ShippingMethod | String (20) | Shipping method text. |
| JournalMemo | String (255) | Journal memo describing the sale. |
| ReferralSource | String (20) | Referral source. |
| InvoiceDeliveryStatus | String (20) | Delivery status: `Print`, `Email`, `PrintAndEmail`, `Nothing`. |
| LastPaymentDate | DateTime | Most recent invoice payment date. |
| InvoiceType | InvoiceType | Layout type: `Item`, `Service`, `Professional`, `TimeBilling`, `Miscellaneous`. |
| Order.UID | Guid (36) | Linked sale order identifier if created from order conversion. |
| Order.Number | String (8) | Linked sales order number. |
| Order.URI | String | Linked sales order URI. |
| OnlinePaymentMethod | String | Which online payment methods are enabled (`All` or `None`). |
| ForeignCurrency.UID | Guid (36) | Linked currency identifier. |
| ForeignCurrency.Code | String (3) | Currency code. |
| ForeignCurrency.CurrencyName | String | Currency name. |
| ForeignCurrency.URI | String | Currency URI. |
| CurrencyExchangeRate | Decimal (13.2) | Exchange rate between local and foreign currency. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 5) CustomerPayment [S5]

**Entity summary:** Customer receipt/payment allocation entity.  
**Source material date:** Released **Aug 2013**; Updated **Jan 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique customer payment identifier. |
| DepositTo | String | `Account` for banking account, or `UndepositedFunds`. |
| Account.UID | Guid (36) | Linked account identifier. |
| Account.Name | String (60) | Linked account name. |
| Account.DisplayID | String (6) | Linked account code. |
| Account.URI | String | Linked account URI. |
| Customer.UID | Guid (36) | Linked customer identifier. |
| Customer.Name | String (30) | Customer name. |
| Customer.DisplayID | String (15) | Customer card ID. |
| Customer.URI | String | Customer URI. |
| ReceiptNumber | String (13) | Payment transaction ID/reference. |
| Date | DateTime | Transaction date. |
| AmountReceived | Decimal (13.2) | Total amount received. |
| AmountReceivedForeign | Decimal (13.2) | Total amount received in foreign currency. |
| PaymentMethod | PaymentMethod | Payment method configured in the company file. |
| Memo | String (255) | Customer payment memo text. |
| Invoices[].RowId | Integer | Sequence within the payment allocation set. |
| Invoices[].Number | String (8) | Sales invoice number. |
| Invoices[].UID | Guid (36) | Linked invoice identifier. |
| Invoices[].AmountApplied | Decimal (13.2) | Amount applied in local currency. |
| Invoices[].AmountAppliedForeign | Decimal (13.2) | Amount applied in foreign currency. |
| Invoices[].Type | String | Sale type: `Invoice` or `Order`. |
| Invoices[].TransactionID | String | Transaction ID of the payment transaction. |
| Invoices[].ForeignCurrency.UID | Guid (36) | Linked currency identifier. |
| Invoices[].ForeignCurrency.Code | String (3) | Currency code. |
| Invoices[].ForeignCurrency.Name | String | Currency name. |
| Invoices[].ForeignCurrency.URI | String | Currency URI. |
| Invoices[].CurrencyExchangeRate | Decimal | Currency exchange rate. |
| Invoices[].URI | String | Nested resource URI. |

---

## 6) SupplierPayment [S6]

**Entity summary:** Supplier payment/allocation entity.  
**Source material date:** Released **Sep 2013**; Updated **Jan 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique supplier payment identifier. |
| PayFrom | String | `Account` for banking account, or `ElectronicPayments`. |
| Account.UID | Guid (36) | Linked account identifier; optional when using `ElectronicPayments`, required for bank-account allocation. |
| Account.Name | String (30) | Linked account name. |
| Account.DisplayID | String (6) | Linked account code. |
| Account.URI | String | Linked account URI. |
| Supplier.UID | Guid (36) | Linked supplier identifier. |
| Supplier.Name | String | Supplier name. |
| Supplier.DisplayID | String (15) | Supplier card ID. |
| Supplier.URI | String | Supplier URI. |
| StatementParticulars | String | Electronic-payment particulars (where applicable). |
| StatementCode | String | NZ only. Electronic-payment code. |
| StatementReference | String | NZ only. Electronic-payment reference. |
| PaymentNumber | String (8) | Payment transaction number. |
| Date | DateTime | Transaction date. |
| AmountPaid | Decimal (13.2) | Total amount paid. |
| AmountPaidForeign | Decimal (13.2) | Total amount paid in foreign currency. |
| Memo | String (255) | Supplier payment memo text. |
| Lines[].RowId | Integer | Sequence within the payment allocation set. |
| Lines[].Type | String | Purchase type: `Bill` or `Order`. |
| Lines[].Purchase.UID | Guid (36) | Linked purchase bill/order identifier. |
| Lines[].Purchase.Number | String (8) | Purchase bill/order number. |
| Lines[].Purchase.URI | String | Purchase bill/order URI. |
| Lines[].AmountApplied | Decimal (13.2) | Amount applied in local currency. |
| Lines[].AmountAppliedForeign | Decimal (13.2) | Amount applied in foreign currency. |
| Lines[].RowVersion | String | Nested change-control version token. |
| DeliveryStatus | String (20) | Delivery status: `Print`, `Email`, `PrintAndEmail`, `Nothing`. |
| ForeignCurrency.UID | Guid (36) | Linked currency identifier. |
| ForeignCurrency.Code | String (3) | Currency code. |
| ForeignCurrency.CurrencyName | String | Currency name. |
| ForeignCurrency.URI | String | Currency URI. |
| CurrencyExchangeRate | Decimal | Currency exchange rate. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 7) Bank Account [S7]

**Entity summary:** Bank-feed-linked bank account entity with masking for sensitive data.  
**Source material date:** Released **Feb 2015**; Updated **Feb 2023**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique bank account identifier. |
| FinancialInstitution | String (3) | Financial institution code. |
| BankAccountName | String | Account name; masked to comply with PII standards. |
| BSB | String (6) | AU only. BSB; masked to comply with PII standards. |
| BankAccountNumber | String (9) | Bank account number; masked to comply with PII standards. |
| CardName | String | Credit-card name; masked to comply with PII standards. |
| CardNumber | String | Credit-card number; masked to comply with PII standards. |
| Account.UID | Guid (36) | Linked general-ledger account identifier. |
| Account.Name | String (30) | Linked account name. |
| Account.DisplayID | String (6) | Linked account code. |
| Account.URI | String | Linked account URI. |
| BankLinkStatus | String | Bankfeed connection status. |
| LastReconciledDate | DateTime | Date the account was last reconciled. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 8) Account [S8]

**Entity summary:** General ledger account entity.  
**Source material date:** Released **Aug 2013**; Updated **Jan 2022**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique account identifier. Required for updates; not required for create. |
| Name | String (60) | Account name. |
| DisplayID | String (6) or (10) | Parent account code with separator when `UseAlphaAccountIdentifier=false`; alphanumeric when `true`. |
| Classification | Classification | One of `Asset`, `Liability`, `Equity`, `Income`, `CostOfSales`, `Expense`, `OtherIncome`, `OtherExpense`. |
| Type | AccountType | Account type within the selected classification. |
| Number | Integer | Unique four-digit account number excluding classification digit/separator. |
| Description | String (255) | Account description. |
| ParentAccount.UID | Guid (36) | Parent account identifier. |
| ParentAccount.Name | String (6) | Parent account name. |
| ParentAccount.DisplayID | String (6) | Parent account display code. |
| ParentAccount.URI | String | Parent account URI. |
| IsActive | Boolean | Whether the account is active. |
| TaxCode.UID | Guid (36) | Assigned tax code identifier. |
| TaxCode.Code | String (3) | Assigned tax code. |
| TaxCode.URI | String | Assigned tax code URI. |
| Level | Integer | Hierarchy level in the accounts list (`1` to `4`). |
| OpeningBalance | Decimal (13.3) | Balance at company-file conversion date. |
| CurrentBalance | Decimal (13.3) | Current balance including future-dated activity. |
| BankingDetails.BSBNumber | String (9) | AU only. BSB. |
| BankingDetails.BankAccountNumber | String (20) | Bank account number. |
| BankingDetails.BankAccountName | String (32) | Bank account name. |
| BankingDetails.CompanyTradingName | String (50) | AU only. Company trading name for bank account. |
| BankingDetails.BankCode | String (3) | AU only. Bank code. |
| BankingDetails.CreateBankFiles | Boolean | Whether the account is used to create bank files (ABA). |
| BankingDetails.DirectEntryUserId | String (6) | AU only. Direct entry user ID. |
| BankingDetails.IncludeSelfBalancingTransaction | Boolean | AU only. Whether self-balancing transaction is required. |
| BankingDetails.StatementParticulars | String (12) | Statement particulars for the bank account. |
| BankingDetails.StatementCode | String | NZ only. Statement code. |
| BankingDetails.StatementReference | String | NZ only. Statement reference. |
| IsHeader | Boolean | `true` for header account; `false` for detail account. |
| LastReconciledDate | DateTime | Last reconciliation date, or `null` if never reconciled. |
| ForeignCurrency.UID | Guid (36) | Linked currency identifier. |
| ForeignCurrency.Code | String (3) | Currency code. |
| ForeignCurrency.CurrencyName | String | Currency name. |
| ForeignCurrency.URI | String | Currency URI. |
| LastModified | DateTime | Last direct modification datetime. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 9) Category [S9]

**Entity summary:** Cost-centre tracking category.  
**Source material date:** Released **Aug 2013**; Updated **Dec 2020**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique category identifier. Required for updates; not required for create. |
| DisplayID | String (15) | Category display ID. |
| Name | String (30) | Category name. |
| Description | String (255) | Category description. |
| IsActive | Boolean | Whether the category is active; defaults to `true` on POST if blank. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## 10) TaxCode [S10]

**Entity summary:** General-ledger tax code setup.  
**Source material date:** Released **Dec 2013**; Updated **Dec 2020**.

| Field | Type | Description |
|---|---|---|
| UID | Guid (36) | Unique tax code identifier. Required for updates; not required for create. |
| Code | String (3) | Three-digit tax code. |
| Description | String (30) | Tax code description. |
| Type | TaxCodeType | Includes `ImportDuty`, `SalesTax`, `GST_VAT`, `InputTaxed`, `Consolidated`, `LuxuryCarTax`, `WithholdingsTax`, `NoABN_TFN`. |
| Rate | Decimal (8.4) | Assigned tax rate. |
| IsRateNegative | Boolean | Whether the rate is negative. |
| TaxCollectedAccount.UID | Guid (36) | Tax-collected account identifier. |
| TaxCollectedAccount.Name | String (60) | Tax-collected account name. |
| TaxCollectedAccount.DisplayID | String (6) | Tax-collected account code. |
| TaxCollectedAccount.URI | String | Tax-collected account URI. |
| TaxPaidAccount.UID | Guid (36) | Tax-paid account identifier. |
| TaxPaidAccount.Name | String (60) | Tax-paid account name. |
| TaxPaidAccount.DisplayID | String (6) | Tax-paid account code. |
| TaxPaidAccount.URI | String | Tax-paid account URI. |
| WithholdingCreditAccount.UID | Guid (36) | Withholding-credit account identifier. |
| WithholdingCreditAccount.Name | String (60) | Withholding-credit account name. |
| WithholdingCreditAccount.DisplayID | String (6) | Withholding-credit account code. |
| WithholdingCreditAccount.URI | String | Withholding-credit account URI. |
| WithholdingPayableAccount.UID | Guid (36) | Withholding-payable account identifier. |
| WithholdingPayableAccount.Name | String (60) | Withholding-payable account name. |
| WithholdingPayableAccount.DisplayID | String (6) | Withholding-payable account code. |
| WithholdingPayableAccount.URI | String | Withholding-payable account URI. |
| ImportDutyPayableAccount.UID | Guid (36) | Import-duty-payable account identifier. |
| ImportDutyPayableAccount.Name | String (60) | Import-duty-payable account name. |
| ImportDutyPayableAccount.DisplayID | String (6) | Import-duty-payable account code. |
| ImportDutyPayableAccount.URI | String | Import-duty-payable account URI. |
| LinkedSupplier.UID | Guid (36) | Linked supplier identifier. |
| LinkedSupplier.Name | String (10) | Linked supplier name. |
| LinkedSupplier.DisplayID | String (15) | Linked supplier card ID. |
| LinkedSupplier.URI | String | Linked supplier URI. |
| LuxuryCarTaxThreshold | Decimal (13.6) | Threshold above which luxury car tax is calculated. |
| LastModified | DateTime | Last direct modification datetime. |
| URI | String | Resource URI. |
| RowVersion | String | Change-control version token. |

---

## Consolidated sources

- **[S1] Customer** — https://developer.myob.com/api/myob-business-api/v2/contact/customer/  
  Source material date: **Date Released: Aug 2013; Date Updated: Jan 2022**

- **[S2] Supplier** — https://developer.myob.com/api/myob-business-api/v2/contact/supplier/  
  Source material date: **Date Released: Dec 2013; Date Updated: Apr 2022**

- **[S3] EmployeePaymentDetails** — https://developer.myob.com/api/myob-business-api/v2/contact/employee-payment-details/  
  Source material date: **Date Released: Aug 2014; Date Updated: Dec 2020**

- **[S4] Invoice** — https://developer.myob.com/api/myob-business-api/v2/sale/invoice/  
  Source material date: **Date Released: Aug 2013; Date Updated: Jan 2022**

- **[S5] CustomerPayment** — https://developer.myob.com/api/myob-business-api/v2/sale/customerpayment/  
  Source material date: **Date Released: Aug 2013; Date Updated: Jan 2022**

- **[S6] SupplierPayment** — https://developer.myob.com/api/myob-business-api/v2/purchase/supplierpayment/  
  Source material date: **Date Released: Sep 2013; Date Updated: Jan 2022**

- **[S7] Bank Account** — https://developer.myob.com/api/myob-business-api/v2/banking/bank-account/  
  Source material date: **Date Released: Feb 2015; Date Updated: Feb 2023**

- **[S8] Account** — https://developer.myob.com/api/myob-business-api/v2/generalledger/account/  
  Source material date: **Date Released: Aug 2013; Date Updated: Jan 2022**

- **[S9] Category** — https://developer.myob.com/api/myob-business-api/v2/generalledger/category/  
  Source material date: **Date Released: Aug 2013; Date Updated: Dec 2020**

- **[S10] TaxCode** — https://developer.myob.com/api/myob-business-api/v2/generalledger/taxcode/  
  Source material date: **Date Released: Dec 2013; Date Updated: Dec 2020**

---

## Practical interpretation note

This catalogue should be treated as an **API contract catalogue**, not as a definitive physical SQL schema of MYOB’s underlying storage engine. MYOB publicly documents these entities through the Business API and related endpoint pages, and those endpoints are the most reliable public source for integration work.
