# MYOB AccountRight Import/Export Field Reference

## ACCOUNTS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Account Number | Required | 5 numeric chars, optional separator (e.g., 1-1234) |
| Account Name | Optional | 30 alphanumeric |
| Header | Optional | 1 char; non-blank = Header, blank = Detail |
| Balance | Optional | 15 chars including currency symbols, rounded to 2 decimals |
| Account Type | Optional | 25 alphanumeric |
| Last Cheque Number | Optional | 7 alphanumeric |
| Tax Code (AU) | Optional | Up to 3 alphanumeric |
| GST Code (NZ) | Optional | Up to 3 alphanumeric |
| Currency Code (Premier) | Optional | 3 alphabetic; must match existing code |
| Inactive Account | Optional | Y/blank=active, N=active, other=inactive |
| AccountantLink Code | Optional | Up to 9 alphanumeric |
| BSB Number (AU) | Optional | XXX-XXX format, 6 numeric + separator |
| Bank Account Number | Optional | 20 alphanumeric (AU), 16 (NZ) |
| Bank Account Name | Optional | 32 alphanumeric (AU), 20 (NZ) |
| Company Trading Name | Optional | 16 alphanumeric |
| Create Bank Files (AU) | Optional | 1 char; non-blank triggers additional fields |
| Bank Code (AU) | Optional | 3 alphabetic |
| Direct Entry User ID (AU) | Optional | 6 numeric |
| Self Balancing Transaction (AU) | Optional | 1 character |
| Description | Optional | 255 alphanumeric |
| Classification for Statement of Cash Flow | Optional | 1 char: O/I/F/E |
| Subtotal Header Accounts | Optional | Y or N |

---

## ACTIVITIES

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Activity ID | Required | 30 alphanumeric |
| Activity Name | Optional | 30 alphanumeric |
| Description | Optional | 255 alphanumeric |
| Use Desc. On Sale | Optional | 1 char; non-blank = use description |
| Non-Hourly | Optional | 1 char; non-blank = Non-Hourly |
| Non-Chargeable | Optional | 1 char; non-blank = Non-Chargeable |
| Use Rate | Optional | 1 char: E/C/A (Employee/Customer/Activity) |
| Activity Rate | Optional | 11 digits, 4 decimal places |
| *Income Account | Required (if chargeable) | 5 numeric; must match existing account |
| Tax Code When Sold (AU) | Optional | 3 alphanumeric; must match pre-existing code |
| GST Code When Sold (NZ) | Optional | 3 alphanumeric; must match pre-existing code |
| Unit of Measure | Optional | 5 alphanumeric |
| Inactive Activity | Optional | Y/blank=active, N=active, other=inactive |

---

## ACTIVITY SLIPS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Emp. Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name) |
| Emp. First Name | Optional | 20 alphanumeric |
| Slip ID | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| *Activity ID | Required | 30 alphanumeric; must match existing |
| Cust. Co./Last Name | Optional | 31 alphanumeric (company), 15 (last name) |
| Cust. First Name | Optional | 15 alphanumeric |
| Units | Optional | 11 numeric, 2 decimal places |
| Rate | Optional | 11 numeric, 2 decimal places |
| Job | Optional | 30 alphanumeric; must match existing |
| Notes | Optional | 255 alphanumeric |
| Adjustment Dollars | Optional | 11 numeric, 2 decimal places |
| Adjustment Units | Optional | 11 numeric, 2 decimal places |
| Already Billed Dollars | Optional | 11 numeric, 2 decimal places |
| Already Billed Units | Optional | 11 numeric, 2 decimal places |
| Start Time | Optional | h:mm:ss AM/PM format |
| Stop Time | Optional | h:mm:ss AM/PM format |
| Payroll Category (AU) | Optional | 30 alphanumeric; must match linked category |
| ^Emp. Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Emp. Record ID | Conditional | 10 numeric |

---

## BUDGETS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Account Number | Required | 5 numeric, optional separator |
| Account Name | Optional | 30 alphanumeric |
| This FY Budget - Months 1-12 | Optional | 12 digits before decimal, 2 after |
| Next FY Budget - Months 1-12 | Optional | 12 digits before decimal, 2 after |

---

## CUSTOMER CARDS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name) |
| First Name | Optional | 20 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| Card Status | Optional | Blank/N=active, Y/other=inactive |
| Address Lines 1-4 (Addr 1-5) | Optional | Max 255 total; alphanumeric |
| City | Optional | 255 alphanumeric |
| State | Optional | 255 alphanumeric |
| Postcode | Optional | 10 alphanumeric |
| Country | Optional | 255 alphanumeric |
| Phone No. 1-3 | Optional | 21 alphanumeric each |
| Fax No., Email, WWW | Optional | 21 alphanumeric each |
| Contact Name | Optional | 25 alphanumeric |
| Salutation | Optional | 15 alphanumeric |
| Notes | Optional | 255 alphanumeric |
| Identifiers | Optional | 10 alpha only |
| Custom List 1-3 | Optional | 30 alphanumeric each |
| Custom Field 1-3 | Optional | 30 alphanumeric each |
| Billing Rate | Optional | 10 numeric, 4 decimal places |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 (COD/Prepaid/Days/Day of Month/EOM/Day EOM) |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| Terms - % Discount | Optional | 2 chars before/after decimal |
| Terms - % Monthly Charge | Optional | 2 chars before/after decimal |
| Tax Code (AU) | Optional | 3 alphanumeric; must match existing |
| GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Credit Limit | Optional | 7 numeric before decimal, 2 after |
| Tax ID No. (AU) | Optional | 19 alphanumeric |
| GST ID No. (NZ) | Optional | 19 alphanumeric |
| Volume Discount % | Optional | 2 before/after decimal |
| Sales/Purchase Layout | Optional | S/I/P/M/T or blank |
| Price Level | Optional | 1 numeric: 0-6 |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| BSB (AU) | Optional | XXX-XXX format |
| Bank and Branch (NZ) | Optional | XX-XXXX format |
| Account Number (AU) | Optional | 9 numeric |
| Account Name (AU) | Optional | 32 alphanumeric |
| Account Number (NZ) | Optional | XX-XXXX-XXXXXXX-XX/XXX format |
| Account Name (NZ) | Optional | 20 alphanumeric |
| ABN (AU) | Optional | 11 numeric with up to 3 spaces |
| ABN Branch (AU) | Optional | 11 numeric |
| Account | Optional | 5 numeric, optional separator |
| Salesperson | Optional | 31 alphanumeric |
| Salesperson Card ID | Optional | 15 alphanumeric |
| Comment | Optional | 255 alphanumeric |
| Shipping Method | Optional | 20 alphanumeric |
| Printed Form | Optional | 255 alphanumeric |
| Freight Tax Code (AU) | Optional | 3 alphanumeric; must match existing |
| Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Use Customer's Tax Code (AU) | Optional | 1 char; non-blank = use customer code |
| Use Customer's GST Code (NZ) | Optional | 1 char; non-blank = use customer code |
| Receipt Memo | Optional | 255 alphanumeric |
| Invoice/PO Delivery | Optional | P/E/B/A (Print/Email/Both/Already) |
| ^Record ID | Conditional | 10 numeric |

---

## SUPPLIER CARDS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name) |
| First Name | Optional | 20 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| Card Status | Optional | Blank/N=active, Y/other=inactive |
| Address Lines 1-4 (Addr 1-5) | Optional | Max 255 total; alphanumeric |
| City | Optional | 255 alphanumeric |
| State | Optional | 255 alphanumeric |
| Postcode | Optional | 10 alphanumeric |
| Country | Optional | 255 alphanumeric |
| Phone No. 1-3 | Optional | 21 alphanumeric each |
| Fax No., Email, WWW | Optional | 21 alphanumeric each |
| Contact Name | Optional | 25 alphanumeric |
| Salutation | Optional | 15 alphanumeric |
| Notes | Optional | 255 alphanumeric |
| Identifiers | Optional | 10 alpha only |
| Custom List 1-3 | Optional | 30 alphanumeric each |
| Custom Field 1-3 | Optional | 30 alphanumeric each |
| Billing Rate | Optional | 10 numeric, 4 decimal places |
| Cost Per Hour | Optional | 10 numeric, 4 decimal places |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| Terms - % Discount | Optional | 2 before/after decimal |
| Tax Code (AU) | Optional | 3 alphanumeric; must match existing |
| GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Credit Limit | Optional | 7 numeric before decimal, 2 after |
| Tax ID No. | Optional | 19 alphanumeric |
| GST ID No. | Optional | 19 alphanumeric |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| BSB (AU) | Optional | 999-999 format |
| Account Number (AU) | Optional | 9 numeric |
| Account Name (AU) | Optional | 32 alphanumeric |
| Statement Text (AU) | Optional | 18 alphanumeric |
| Remittance Method (AU) | Optional | E/P/B/A |
| Remittance Address (AU) | Optional | Valid email format |
| Account Number (NZ) | Optional | XX-XXXX-XXXXXXX-XXX format |
| Account Name (NZ) | Optional | 20 alphanumeric |
| Particulars (NZ) | Optional | 12 alphanumeric |
| Code (NZ) | Optional | 12 alphanumeric |
| Reference (NZ) | Optional | 12 alphanumeric |
| ABN (AU) | Optional | 11 numeric with up to 3 spaces |
| ABN Branch (AU) | Optional | 11 numeric |
| Volume Discount % | Optional | 2 before/after decimal |
| Sales/Purchase Layout | Optional | S/I/P/M/T or blank |
| Account | Optional | 5 numeric, optional separator |
| Comment | Optional | 255 alphanumeric |
| Shipping Method | Optional | 20 alphanumeric |
| Printed Form | Optional | 255 alphanumeric |
| Freight Tax Code (AU) | Optional | 3 alphanumeric; must match existing |
| Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Use Supplier's Tax Code (AU) | Optional | 1 char; non-blank = use supplier code |
| Use Supplier's GST Code (NZ) | Optional | 1 char; non-blank = use supplier code |
| Report Taxable Payments (AU) | Optional | Blank/Y=report, N/other=don't report |
| Payment Memo | Optional | 255 alphanumeric |
| Invoice/PO Delivery | Optional | P/E/B/A |
| ^Record ID | Conditional | 10 numeric |

---

## EMPLOYEE CARDS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name) |
| First Name | Optional | 20 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| Card Status | Optional | Blank/N=active, Y/other=inactive |
| Address Lines 1-4 (Addr 1-5) | Optional | Max 255 total; alphanumeric |
| City | Optional | 255 alphanumeric |
| State | Optional | 255 alphanumeric |
| Postcode | Optional | 10 alphanumeric |
| Country | Optional | 255 alphanumeric |
| Phone No. 1-3 | Optional | 21 alphanumeric each |
| Fax No., Email, WWW | Optional | 21 alphanumeric each |
| Salutation | Optional | 15 alphanumeric |
| Notes | Optional | 255 alphanumeric |
| Identifiers | Optional | 10 alpha only |
| Custom List 1-3 | Optional | 30 alphanumeric each |
| Custom Field 1-3 | Optional | 30 alphanumeric each |
| Billing Rate | Optional | 10 numeric, 4 decimal places |
| Cost Per Hour | Optional | 10 numeric, 4 decimal places |
| Account Number (NZ) | Optional | XX-XXXX-XXXXXXX-XX/XXX format |
| Account Name (NZ) | Optional | 20 alphanumeric |
| Particulars (NZ) | Optional | 12 alphanumeric |
| Code (NZ) | Optional | 12 alphanumeric |
| Reference (NZ) | Optional | 12 alphanumeric |
| Number of Bank Accounts | Optional | 1 numeric |
| BSB 1-3 | Optional | 7 numeric with separator (999-999) |
| Account Number 1-3 | Optional | 9 numeric |
| Account Name 1-3 | Optional | 32 alphanumeric |
| Statement Text | Optional | 18 alphanumeric |
| Bank Value 1-2 | Optional | 13 before/2 after decimal (Dollars); 3 before/2 after (Percent) |
| Bank Value Type 1-2 | Optional | D or P |
| Employment Basis | Optional | 1 numeric: 0/1/2 |
| Payment Method | Optional | 1 numeric: 1/2/3 (Cash/Cheque/Electronic) |
| Employment Classification | Optional | 255 alphanumeric |
| Date of Birth | Optional | 10 chars; system date format |
| Gender | Optional | M/F/I |
| Start Date | Optional | 10 chars; system date format |
| Termination Date | Optional | 10 chars; system date format |
| Pay Basis | Optional | S or H (Salary/Hourly) |
| Salary/Rate | Optional | 13+4 decimals (Hourly), 13+2 (Annual) |
| Pay Frequency | Optional | W/F/T/M (Weekly/Fortnightly/Twice/Monthly) |
| Hours in Pay Period | Optional | 3 digits, 3 decimal places |
| Wages Expense Account | Optional | 5 numeric; must match existing |
| Superannuation Fund | Optional | 76 alphanumeric; must match existing |
| Employee Membership No. | Optional | 16 alphanumeric |
| Tax File Number | Optional | 9 numeric |
| Tax Table | Optional | 34 alpha; must match existing |
| Withholding Variation Rate | Optional | 3 digits, 4 decimal places |
| Total Rebates | Optional | 13 digits, 2 decimal places |
| Extra Tax | Optional | 13 digits, 2 decimal places |
| Default Category | Optional | 15 alphanumeric; must match existing |
| ^Record ID | Conditional | 10 numeric |
| Employment Category | Optional | P or T (Permanent/Temporary) |
| Employment Status | Optional | F/P/O/C (Full/Part/Other/Casual) |
| Terminated By | Optional | 40 alphanumeric |
| Method of Termination | Optional | C/N/S/O |
| Termination Reason | Optional | 255 alphanumeric |
| Pay Slip Delivery | Optional | P/E/B/A |
| Pay Slip Email | Optional | 255 alphanumeric |
| Memo | Optional | 255 alphanumeric |

---

## PERSONAL CARDS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name) |
| First Name | Optional | 20 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| Card Status | Optional | Blank/N=active, Y/other=inactive |
| Currency Code (Premier) | Optional | 3 alphabetic; must match existing |
| Address Lines 1-4 (Addr 1-5) | Optional | Max 255 total; alphanumeric |
| City | Optional | 255 alphanumeric |
| State | Optional | 255 alphanumeric |
| Postcode | Optional | 10 alphanumeric |
| Country | Optional | 255 alphanumeric |
| Phone No. 1-3 | Optional | 21 alphanumeric each |
| Fax No., Email, WWW | Optional | 21 alphanumeric each |
| Salutation | Optional | 15 alphanumeric |
| Notes | Optional | 255 alphanumeric |
| Identifiers | Optional | 10 alpha only |
| Custom List 1-3 | Optional | 30 alphanumeric each |
| Custom Field 1-3 | Optional | 30 alphanumeric each |
| ^Record ID | Conditional | 10 numeric |

---

## CONTACT LOGS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Contact Log Record ID | Conditional | 10 numeric |
| ^Date | Conditional | 10 chars; system date format |
| ^Card ID | Conditional | 15 alphanumeric |
| ^Card Record ID | Conditional | 10 numeric |
| ^Co./Last Name | Conditional | 50 alphanumeric |
| Contact | Optional | 255 alphanumeric |
| Elapsed Time | Optional | 4 numeric |
| First Name | Optional | 20 alphanumeric |
| Notes | Optional | 255 alphanumeric |
| Recontact Date | Optional | 10 chars; date format |
| Remove from Contact Alert | Optional | 1 alpha |

---

## CUSTOM LISTS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Custom List Name | Required | 30 alphanumeric |
| *Type | Required | 1 alpha |
| *Number | Required | 1 alphabetic |
| Update Custom List Name | Optional | 30 alphanumeric |

---

## ITEMS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Item Number | Required | 30 alphanumeric |
| Item Name | Optional | 30 alphanumeric |
| Buy | Optional | 1 char; non-blank = bought |
| Sell | Optional | 1 char; non-blank = sold |
| Inventory | Optional | 1 char; non-blank = inventoried |
| Asset Acct | Optional | 5 numeric; must match existing |
| Income Acct | Optional | 5 numeric; must match existing |
| Expense/COS Acct | Optional | 5 numeric; must match existing |
| Description | Optional | 255 alphanumeric |
| Use Desc. On Invoice | Optional | 1 char; non-blank = use description |
| Custom List 1-3 | Optional | 30 alphanumeric each; must match existing |
| Custom Field 1-3 | Optional | 30 alphanumeric each |
| Primary Supplier | Optional | 31 alphanumeric; must match existing |
| Supplier Item Number | Optional | 30 alphanumeric |
| Tax Code When Bought (AU) | Optional | 3 alphanumeric; must match existing |
| GST Code When Bought (NZ) | Optional | 3 alphanumeric; must match existing |
| Buy Unit Measure | Optional | 5 alphanumeric |
| No. Items/Buy Unit | Optional | 4 numeric |
| Reorder Quantity | Optional | 10 numeric, 3 decimal places |
| Minimum Level | Optional | 10 numeric, 3 decimal places |
| Selling Price | Optional | 11 numeric, 4 decimal places |
| Sell Unit Measure | Optional | 5 alphanumeric |
| Tax Code When Sold (AU) | Optional | 3 alphanumeric; must match existing |
| GST Code When Sold (NZ) | Optional | 3 alphanumeric; must match existing |
| Sell Price Inclusive | Optional | X indicates GST-inclusive |
| Sales Tax Calc. Method (AU) | Optional | 1 char: 0/3/4/5/6/7/8/9 |
| No. Items/Sell Unit | Optional | 4 numeric |
| Quantity Break 1-5 | Optional | 10 numeric, 3 decimal places (must be 0, greater, or progressively larger) |
| Price Level A-F, Qty Break 1-5 | Optional | 11 numeric, 4 decimal places |
| Inactive Item | Optional | Y/blank=active, N=active, other=inactive |
| Standard Cost | Optional | 10 numeric, 4 decimal places |
| Default Ship/Sell Location | Optional | 10 alphanumeric; must match existing |
| Default Recvd/Auto Location | Optional | 10 alphanumeric; must match existing |

---

## INVENTORY ADJUSTMENTS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Amount | Required | 13 numeric, 2 decimal places; rounded if more |
| *Item Number | Required | 30 alphanumeric; must match existing inventoried item |
| Account | Optional | 5 numeric; must match existing |
| Allocation Memo | Optional | 255 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Is Year-End Adjustment | Optional | Y or N |
| Job | Optional | 30 alphanumeric; must match existing |
| Journal Number | Optional | 8 alphanumeric |
| Location | Optional | 10 alphanumeric |
| Memo | Optional | 255 alphanumeric |
| Quantity | Optional | 11 numeric, 3 decimal places; rounded if more |
| Unit Cost | Optional | 11 numeric, 4 decimal places; rounded if more |

---

## JOBS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Job Number | Required | 30 alphanumeric |
| Job Name | Optional | 25 alphanumeric |
| Sub Job Of | Optional | 30 alphanumeric |
| Header | Optional | H or D |
| Description | Optional | 255 alphanumeric |
| Contact | Optional | 25 alphanumeric |
| Percent Complete | Optional | Not greater than 100; 2 before/after decimal |
| Start Date | Optional | 10 chars; system date format |
| Finish Date | Optional | 10 chars; system date format |
| Manager | Optional | 25 alphanumeric |
| Linked Customer | Optional | 50 alphanumeric (company), 30 (last name); must match existing |
| Inactive Job | Optional | Y/blank=active, N=active, other=inactive |
| Track Reimbursables | Optional | Y/other=marked, N/blank=unmarked |

---

## GENERAL JOURNAL ENTRIES

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Account Number | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| *GST Reporting (NZ) | Required | S or P (Supply/Purchase) |
| *GST/BAS Reporting (AU) | Required | S or P (Supply/Purchase) |
| *Is Credit | Required | Y or N |
| *Tax Amount (AU) / *GST Amount (NZ) | Required | 15 chars, 2 decimal places; must be 0 if no tax |
| Allocation Memo | Optional | 255 alphanumeric |
| Amount Foreign (Premier) | Optional | 15 chars, 2 decimal places; rounded if more |
| Category | Optional | 15 alphanumeric |
| Currency Code (Premier) | Optional | 3 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Exchange Rate (Premier) | Optional | 10 chars including decimal |
| Inclusive | Optional | X indicates GST-inclusive |
| Is Year-End Adjustment | Optional | Y or N |
| Job | Optional | 30 alphanumeric |
| Journal Number | Optional | 255 alphanumeric |
| Memo | Optional | 255 alphanumeric |
| Tax Amount Foreign (AU) / GST Amount Foreign (NZ) (Premier) | Optional | 15 chars, 2 decimal places; rounded if more; must be 0 if none |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; Tax-exclusive if not pre-existing |

---

## TRANSACTION JOURNALS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| Journal Number | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Memo | Optional | 255 alphanumeric |
| *Account Number | Required | 5 numeric, optional separator; must match existing |
| Is Credit | Optional | Y or N |
| Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Currency Code (Premier) | Optional | 3 alphabetic; must match account currency; one per entry |
| Allocation Memo | Optional | 255 alphanumeric |
| Category | Optional | 15 alphanumeric |
| Is Year-End Adjustment | Optional | Y or N |

---

## PAY BILLS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 255 alphanumeric |
| First Name | Optional | 255 alphanumeric |
| Payee Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| *Payment Account No. | Required | 5 numeric, optional separator; must match existing |
| Cheque Number | Optional | 8 alphanumeric |
| Payment Date | Optional | 10 chars; system date format |
| Statement Text (AU) | Optional | 18 alphanumeric |
| ^Purchase No. | Conditional | 8 alphanumeric |
| ^Supplier's No. | Conditional | 20 alphanumeric |
| Bill Date | Optional | 10 chars; system date format |
| *Amount Applied | Required | 15 chars, 2 decimal places; rounded if more |
| Memo | Optional | 255 alphanumeric |
| Already Printed | Optional | 1 alpha |
| Currency Code (Premier) | Optional | 3 alphabetic; must match account currency |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |

---

## PURCHASES - SERVICES

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| % Discount | Optional | 2 before/after decimal |
| Balance Due Days | Optional | 3 numeric |
| Discount Days | Optional | 3 numeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| ^Record ID | Conditional | 10 numeric |
| Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Category | Optional | 15 alphanumeric |
| Comment | Optional | 255 alphanumeric |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Date | Optional | 10 chars; system date format |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Description | Optional | 255 alphanumeric |
| First Name | Optional | 20 alphanumeric |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Inclusive | Optional | X indicates tax-inclusive |
| Job | Optional | 30 alphanumeric; must match existing |
| Journal Memo | Optional | 255 alphanumeric |
| Purchase No. | Optional | 8 alphanumeric |
| Purchase Status | Optional | O/Q or blank (Order/Quote/Bill) |
| Ship Via | Optional | 20 alphanumeric |
| Shipping Date | Optional | 10 chars; system date format |
| Supplier Invoice No. | Optional | 20 alphanumeric |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |

---

## PURCHASES - ITEMS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Item Number | Required | 30 alphanumeric; must match existing |
| % Discount | Optional | 2 before/after decimal |
| Balance Due Days | Optional | 3 numeric |
| Discount Days | Optional | 3 numeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| ^Record ID | Conditional | 10 numeric |
| Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Billed | Optional | 10 numeric, 3 decimal places; cannot exceed Received or Ordered |
| Category | Optional | 15 alphanumeric |
| Comment | Optional | 255 alphanumeric |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Date | Optional | 10 chars; system date format |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Description | Optional | 255 alphanumeric |
| Discount | Optional | 10 numeric, 2 decimal places |
| First Name | Optional | 20 alphanumeric |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Inclusive | Optional | X indicates tax-inclusive |
| Job | Optional | 30 alphanumeric; must match existing |
| Journal Memo | Optional | 255 alphanumeric |
| Location ID | Optional | 10 alphanumeric |
| Order | Optional | 10 numeric, 3 decimal places |
| Price | Optional | 11 numeric, 3 decimal places |
| Purchase No. | Optional | 8 alphanumeric |
| Purchase Status | Optional | O/Q or blank (Order/Quote/Bill) |
| Quantity | Optional | 10 numeric, 3 decimal places |
| Received | Optional | 10 numeric, 3 decimal places |
| Ship Via | Optional | 20 alphanumeric |
| Shipping Date | Optional | 10 chars; system date format |
| Supplier Invoice No. | Optional | 20 alphanumeric |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| Total | Optional | 15 chars, 2 decimal places; rounded if more |

---

## PURCHASES - PROFESSIONAL

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Purchase No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Supplier Invoice No. | Optional | 20 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Journal Memo | Optional | 255 alphanumeric |
| Detail Date | Optional | 10 chars; system date format |
| Description | Optional | 255 alphanumeric |
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Promised Date | Optional | 10 chars; system date format |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Purchase Status | Optional | O/Q or blank (Order/Quote/Bill) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| % Discount | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## PURCHASES - MISCELLANEOUS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Supplier Invoice No. | Optional | 20 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Memo | Optional | 255 alphanumeric |
| Description | Optional | 255 alphanumeric |
| *Account Number | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Purchase Status | Optional | O/Q or blank (Order/Quote/Bill) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match card currency or blank |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| % Discount | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## RECEIVE MONEY

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Deposit Account | Required | 5 numeric, optional separator; defaults if missing |
| ID No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| ^Co./Last Name | Conditional | 255 alphanumeric |
| First Name | Optional | 255 alphanumeric |
| Memo | Optional | 255 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| *Allocation Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job No. | Optional | 30 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; Tax-exclusive if not pre-existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Payment Method | Optional | 20 alphanumeric |
| Drawer/Account Name | Optional | 50 alphanumeric |
| BSB (AU) | Optional | 7 numeric |
| Account Number | Optional | 9 alphanumeric |
| Cheque Number | Optional | 17 alphanumeric |
| Card Number | Optional | 25 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Authorisation Code | Optional | 30 alphanumeric |
| Notes | Optional | 50 alphanumeric |
| Allocation Memo | Optional | 255 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## RECEIVE PAYMENTS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 255 alphanumeric |
| First Name | Optional | 255 alphanumeric |
| *Deposit Account No. | Required | 5 numeric, optional separator; defaults if missing |
| ID No. | Optional | 8 alphanumeric |
| Receipt Date | Optional | 10 chars; system date format |
| ^Invoice No. | Conditional | 8 alphanumeric |
| ^Customer PO No. | Conditional | 20 alphanumeric |
| Invoice Date | Optional | 10 chars; system date format |
| *Amount Applied | Required | 15 chars, 2 decimal places; rounded if more |
| Memo | Optional | 255 alphanumeric |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 50 alphanumeric |
| Drawer/Account Name | Optional | 50 alphanumeric |
| BSB | Optional | 7 numeric |
| Account Number | Optional | 9 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 25 alphanumeric |
| Authorisation Code | Optional | 30 alphanumeric |
| Cheque No. | Optional | 17 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SALES - SERVICES

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Invoice No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Customer PO | Optional | 20 alphanumeric |
| Ship Via | Optional | 20 alphanumeric |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Description | Optional | 255 alphanumeric |
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Journal Memo | Optional | 255 alphanumeric |
| Salesperson Last Name | Optional | 31 alphanumeric; must match employee card |
| Salesperson First Name | Optional | 15 alphanumeric |
| Promised Date | Optional | 10 chars; system date format |
| Referral Source | Optional | 20 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Sale Status | Optional | O/Q or blank (Order/Quote/Invoice) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| Terms - % Discount | Optional | 2 before/after decimal |
| Terms - % Monthly Charge | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| Authorisation Code | Optional | 255 alphanumeric |
| BSB (AU) | Optional | 25 alphanumeric |
| Account Number (AU) | Optional | 25 alphanumeric |
| Drawer/Account Name (AU) | Optional | 32 alphanumeric |
| Cheque Number | Optional | 8 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SALES - ITEMS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Invoice No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Customer PO | Optional | 20 alphanumeric |
| Ship Via | Optional | 20 alphanumeric |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| *Item Number | Required | 30 alphanumeric; must match existing |
| Quantity | Optional | 10 numeric, 3 decimal places |
| Description | Optional | 255 alphanumeric |
| Price | Optional | 11 numeric, 3 decimal places; must be tax-exclusive |
| Discount | Optional | 10 numeric, 2 decimal places |
| Total | Optional | 15 chars, 2 decimal places; tax-exclusive |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Journal Memo | Optional | 255 alphanumeric |
| Salesperson Last Name | Optional | 31 alphanumeric; must match employee card |
| Salesperson First Name | Optional | 20 alphanumeric |
| Shipping Date | Optional | 10 chars; system date format |
| Referral Source | Optional | 20 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Sale Status | Optional | O/Q or blank (Order/Quote/Invoice) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| Terms - % Discount | Optional | 2 before/after decimal |
| Terms - % Monthly Charge | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| Authorisation Code | Optional | 255 alphanumeric |
| BSB (AU) | Optional | 25 alphanumeric |
| Account Number | Optional | 25 alphanumeric |
| Drawer/Account Name | Optional | 32 alphanumeric |
| Cheque Number | Optional | 8 alphanumeric |
| Category | Optional | 15 alphanumeric |
| Location ID | Optional | 10 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SALES - PROFESSIONAL

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Invoice # | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Customer PO | Optional | 20 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Detail Date | Optional | 10 chars; system date format |
| Description | Optional | 255 alphanumeric |
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Journal Memo | Optional | 255 alphanumeric |
| Salesperson Last Name | Optional | 31 alphanumeric; must match employee card |
| Salesperson First Name | Optional | 20 alphanumeric |
| Promised Date | Optional | 10 chars; system date format |
| Referral Source | Optional | 20 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Sale Status | Optional | O/Q or blank (Order/Quote/Invoice) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| % Discount | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| Authorisation Code | Optional | 255 alphanumeric |
| BSB (AU) | Optional | 25 alphanumeric |
| Account Number (AU) | Optional | 25 alphanumeric |
| Drawer/Account Name (AU) | Optional | 32 alphanumeric |
| Cheque Number | Optional | 8 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SALES - TIME BILLING

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Invoice # | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Customer PO | Optional | 20 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Detail Date | Optional | 10 chars; system date format |
| Description | Optional | 255 alphanumeric |
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Units | Required | 11 numeric, 2-4 decimal places |
| *Rate | Required | 11 numeric, 2-4 decimal places |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Journal Memo | Optional | 255 alphanumeric |
| Salesperson Last Name | Optional | 31 alphanumeric; must match employee card |
| Salesperson First Name | Optional | 20 alphanumeric |
| Promised Date | Optional | 10 chars; system date format |
| Referral Source | Optional | 20 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Sale Status | Optional | O/Q or blank (Order/Quote/Invoice) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| % Discount | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| Authorisation Code | Optional | 255 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SALES - MISCELLANEOUS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| First Name | Optional | 20 alphanumeric |
| Invoice No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| Customer PO | Optional | 20 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| Delivery Status | Optional | P/E/B/A (defaults to P if blank) |
| Description | Optional | 255 alphanumeric |
| *Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Comment | Optional | 255 alphanumeric |
| Journal Memo | Optional | 255 alphanumeric |
| Salesperson Last Name | Optional | 31 alphanumeric; must match employee card |
| Salesperson First Name | Optional | 20 alphanumeric |
| Promised Date | Optional | 10 chars; system date format |
| Referral Source | Optional | 20 alphanumeric |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Amount | Optional | 15 chars, 2 decimal places; rounded if more |
| Freight Tax Code (AU) / Freight GST Code (NZ) | Optional | 3 alphanumeric; must match existing |
| Freight Tax Amount (AU) / Freight GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Sale Status | Optional | O/Q or blank (Order/Quote/Invoice) |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Terms - Payment is Due | Optional | 1 numeric: 0-5 |
| Terms - Discount Days | Optional | 3 numeric |
| Terms - Balance Due Days | Optional | 3 numeric |
| % Discount | Optional | 2 before/after decimal |
| Amount Paid | Optional | 15 chars, 2 decimal places; rounded if more |
| Payment Method | Optional | 20 alphanumeric |
| Payment Notes | Optional | 255 alphanumeric |
| Name on Card | Optional | 50 alphanumeric |
| Card Number | Optional | 4 alphanumeric |
| Authorisation Code | Optional | 255 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## SPEND MONEY

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Payment Account | Required | 5 numeric, optional separator; must match existing |
| Cheque No. | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| ^Co./Last Name | Conditional | 255 alphanumeric |
| First Name | Optional | 255 alphanumeric |
| Payee Address Lines 1-4 | Optional | Max 255 total; alphanumeric |
| Memo | Optional | 255 alphanumeric |
| Inclusive | Optional | X indicates tax-inclusive |
| *Allocation Account No. | Required | 5 numeric, optional separator; must match existing |
| *Amount | Required | 15 chars, 2 decimal places; rounded if more |
| Job | Optional | 30 alphanumeric; must match existing |
| Tax Code (AU) / GST Code (NZ) | Optional | 3 alphanumeric; Tax-exclusive if not pre-existing |
| Tax Amount (AU) / GST Amount (NZ) | Optional | 15 chars, 2 decimal places; rounded if more |
| Currency Code (Premier) | Optional | 3 alphabetic; one per purchase; must match existing & card |
| Allocation Memo | Optional | 255 alphanumeric |
| Category | Optional | 15 alphanumeric |
| ^Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Record ID | Conditional | 10 numeric |

---

## TIMESHEETS

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| ^Emp. Co./Last Name | Conditional | 50 alphanumeric (company), 30 (last name); must match existing |
| Emp. First Name | Optional | 20 alphanumeric |
| Timesheet ID | Optional | 8 alphanumeric |
| Date | Optional | 10 chars; system date format |
| ^Activity ID | Conditional | 30 alphanumeric; must match existing |
| Cust. Co./Last Name | Optional | 31 alphanumeric (company), 15 (last name) |
| Cust. First Name | Optional | 15 alphanumeric |
| Hours | Optional | 11 numeric, 2 decimal places |
| Rate | Optional | 11 numeric, 2 decimal places |
| Job | Optional | 30 alphanumeric; must match existing |
| Notes | Optional | 255 alphanumeric |
| Start Time | Optional | h:mm:ss AM/PM format |
| Stop Time | Optional | h:mm:ss AM/PM format |
| Payroll Category (AU) | Optional | 30 alphanumeric; must match linked category |
| ^Emp. Card ID | Conditional | 15 alphanumeric; must be unique |
| ^Emp. Record ID | Conditional | 10 numeric |

---

## TAX/GST CODE LIST

| Field | Type | Format/Constraints |
|-------|------|-------------------|
| *Tax/GST Code | Required | 3 alphanumeric |
| Description | Optional | 30 alphanumeric |
| Tax/GST Account (AU) | Optional | 5 numeric; must match existing |
| Tax/GST Rate | Optional | 5 numeric, 2 decimal places |
| Purchase Tax/GST Account (AU) | Optional | 5 numeric; must match existing |

---

## NOTES

- **Required fields** marked with * must have valid entries for import to succeed
- **Conditional fields** marked with ^ require at least one field from the group to have valid data
- Character counts exclude formatting elements unless specified
- **Decimal places**: automatic rounding applied if exceeds specified limits
- **Account numbers**: optional non-numeric separators allowed (e.g., 1-1234)
- **Date formats**: follow system conventions; any non-numeric separators acceptable
- **Currency**: Premier version only; must match pre-existing codes
- **Matching requirements**: foreign key references require exact matches to existing records
- **Tax/GST amounts**: must equal zero if no applicable tax
- **Employee cards**: additional AU-specific payroll fields require tax tables and payroll setup
- **Export behavior**: current balances exported for accounts; opening balances for budgets
- **Import restrictions**: do not match Record ID unless from same company file