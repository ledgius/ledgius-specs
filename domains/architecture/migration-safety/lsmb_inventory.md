# LSMB Legacy Artifact Inventory

Spec references: R-0054, A-0030, T-0028.

This is the **canonical inventory** of LedgerSMB-era PL/pgSQL triggers
and functions present in a freshly bootstrapped Ledgius tenant database.
See R-0054 §Terms for vocabulary; A-0030 §"Inventory format" for the
schema of each row.

This file is the **single source of truth** consumed by:

- `ledgius-db/scripts/lsmb_inventory_audit.sql` — drift detection
- `ledgius-db/cmd/lsmb-lint/` — CI guardrail
- `ledgius-api/internal/admin/migration/` — reporting endpoint

A status transition (e.g. `in-use → replaced`) **must** be made in the
same PR that adds the Go replacement. A drop migration **must** be made
in the same PR that flips status to `dropped`.

---

## Status legend

- `unmapped` — present in DB, not yet inventoried (should be zero in this file)
- `in-use` — present in DB, no Go replacement yet
- `replaced` — Go replacement in place, awaiting drop migration soak period
- `dropped` — removed from DB by a versioned drop migration
- `retained` — Ledgius-shape, deliberately retained, excluded from completeness percentage

## Risk tier legend

- `high` — fires on financial tables (`acc_trans`, `ap`, `ar`, `gl`, `journal_entry`, `invoice`, `entity_credit_account`); audit-trail or balance-affecting
- `medium` — fires on business-state tables (chart of accounts, contacts, payroll, reconciliation, reports, budgets)
- `low` — utility / CDC last-updated / cosmetic / sequence tracker

---

## Section 1 — Triggers (33 total)

| name | schema.table | purpose | status | risk_tier | replaced_by | dropped_in_migration |
|---|---|---|---|---|---|---|
| acc_trans_prevent_closed | public.acc_trans | Blocks INSERT/UPDATE/DELETE on acc_trans rows whose period is locked (closed accounting period) | in-use | high | — | — |
| trigger_open_item_maintenance | public.acc_trans | Maintains open_item linkage when acc_trans rows reference an open_item_id | in-use | high | — | — |
| trigger_duplicate_account_accno | public.account | Prevents inserting a duplicate `accno` value | in-use | medium | — | — |
| loop_detection | public.account_heading | Prevents creating a parent-child cycle in account_heading.parent_id | in-use | medium | — | — |
| trigger_duplicate_account_heading_accno | public.account_heading | Prevents inserting a duplicate `accno` value | in-use | medium | — | — |
| prohibit_multiple_summary_account_links | public.account_link | Limits an account to a single 'summary' link | in-use | medium | — | — |
| ap_audit_trail | public.ap | Writes a row to `audittrail` on every INSERT/UPDATE/DELETE — calls `gl_audit_trail_append` | in-use | high | — | — |
| ap_track_deleted_transaction | public.ap | Calls `track_global_sequence` on DELETE — records deletion in `transactions_history` | in-use | high | — | — |
| ar_audit_trail | public.ar | Writes a row to `audittrail` on every INSERT/UPDATE/DELETE — calls `gl_audit_trail_append` | in-use | high | — | — |
| ar_track_deleted_transaction | public.ar | Calls `track_global_sequence` on DELETE | in-use | high | — | — |
| audit_log_immutable | public.audit_log | Ledgius-shape: enforces append-only on the audit_log table per R-0040 (forbids UPDATE/DELETE) | retained | low | n/a — purposefully retained | — |
| business_update_last_updated | public.business | CDC: updates last_updated timestamp on row change — calls `cdc_update_last_updated` | in-use | low | — | — |
| country_update_last_updated | public.country | CDC last-updated timestamp | in-use | low | — | — |
| block_change_when_approved | public.cr_report | Prevents editing a reconciliation report after it has been approved | in-use | medium | — | — |
| cr_report_links_update | public.cr_report | Maintains report-line link consistency on submission | in-use | medium | — | — |
| cr_report_line_links_update | public.cr_report_line | Maintains line-cleared link consistency | in-use | medium | — | — |
| cr_report_line_link_insert | public.cr_report_line_links | Maintains link integrity on insert | in-use | medium | — | — |
| eca_maintain_b_units | public.entity_credit_account | Maintains business_unit links on insert/update | in-use | high | — | — |
| eca_maintain_b_units_del | public.entity_credit_account | Removes business_unit links on delete | in-use | high | — | — |
| eclass_perms_check | public.entity_credit_account | Enforces entity_class permissions | in-use | high | — | — |
| gifi_update_last_updated | public.gifi | CDC last-updated timestamp | in-use | low | — | — |
| gl_audit_trail | public.gl | Writes audit trail on every GL transaction change — calls `gl_audit_trail_append` | in-use | high | — | — |
| gl_track_deleted_transaction | public.gl | Records GL transaction deletions in transactions_history | in-use | high | — | — |
| gl_track_global_sequence | public.gl | Maintains global sequence tracking for GL transactions | in-use | high | — | — |
| trigger_invoice_prevent_allocation_delete | public.invoice | Prevents deleting an invoice line that has been allocated | in-use | high | — | — |
| je_audit_trail | public.journal_entry | Writes audit trail on every journal_entry change — calls `gl_audit_trail_append` | in-use | high | — | — |
| language_update_last_updated | public.language | CDC last-updated timestamp | in-use | low | — | — |
| parts_short | public.parts | Inventory short-item warning trigger | in-use | medium | — | — |
| partsgroup_update_last_updated | public.partsgroup | CDC last-updated timestamp | in-use | low | — | — |
| pricegroup_update_last_updated | public.pricegroup | CDC last-updated timestamp | in-use | low | — | — |
| sic_update_last_updated | public.sic | CDC last-updated timestamp | in-use | low | — | — |
| warehouse_update_last_updated | public.warehouse | CDC last-updated timestamp | in-use | low | — | — |
| trigger_workflow_user | public.workflow_history | Stamps the acting user onto workflow_history rows | in-use | medium | — | — |

---

## Section 2 — Functions (503 total)

The vast majority of the function inventory is LedgerSMB's API surface
following the `<domain>__<method>` naming convention (double-underscore
namespace separator). Functions are bucketed below by domain prefix;
detail for each function is enumerated as each domain's migration begins.

A drop migration that removes a function MUST add a per-function row at
the bottom of this section (`status=dropped`, `dropped_in_migration=<file>`)
so that the audit query catches accidental re-introduction.

### Domain function buckets (status: `in-use`)

| domain prefix | function count | risk_tier | notes |
|---|---|---|---|
| eca__* | 21 | high | Entity credit account API (vendors + customers AP/AR linkage) |
| reconciliation__* | 19 | medium | Bank reconciliation API |
| asset_report__* | 19 | medium | Fixed-asset reporting |
| lsmb__* | 17 | low | LSMB platform-level utilities |
| entity__* | 17 | medium | Entity (person/company) base API |
| file__* | 16 | low | Attachment / file storage API |
| account__* | 16 | medium | Chart-of-accounts API |
| person__* | 15 | medium | Person record API |
| admin__* | 13 | medium | User/role administration API |
| budget__* | 12 | medium | Budget management API |
| report__* | 10 | medium | Generic report builder API |
| journal__* | 10 | high | Journal entry API |
| inventory_adjust__* | 9 | medium | Inventory adjustment API |
| asset_class__* | 8 | medium | Asset class definitions |
| employee__* | 7 | medium | Employee record API |
| account_heading__* | 7 | medium | Chart-of-accounts heading API |
| timecard__* | 6 | medium | Timecard / time tracking API |
| sequence__* | 6 | low | Sequence number generation |
| cogs__* | 6 | high | Cost of Goods Sold computations |
| user__* | 5 | medium | User profile API |
| robot__* | 5 | low | Background-task / robot API |
| pnl__* | 5 | medium | P&L statement generation |
| exchangerate_type__* | 5 | low | Exchange rate type definitions |
| currency__* | 5 | low | Currency table API |
| business_unit__* | 5 | low | Business unit (cost centre) API |
| template__* | 4 | low | Template management |
| tax_form__* | 4 | medium | Tax-form definitions (1099, etc.) |
| inventory__* | 4 | medium | Inventory tracking |
| exchangerate__* | 4 | medium | Exchange rate values |
| company__* | 4 | medium | Company record API |
| (other domains, ~250 functions) | ~250 | mixed | Assorted; enumerated as encountered during migration work |

### Trigger functions (called by triggers in Section 1)

| name | called by | status | risk_tier | replaced_by | dropped_in_migration |
|---|---|---|---|---|---|
| gl_audit_trail_append() | ap_audit_trail, ar_audit_trail, gl_audit_trail, je_audit_trail | in-use | high | — | — |
| track_global_sequence() | ap_track_deleted_transaction, ar_track_deleted_transaction, gl_track_deleted_transaction, gl_track_global_sequence | in-use | high | — | — |
| cdc_update_last_updated() | business_update_last_updated, country_update_last_updated, gifi_update_last_updated, language_update_last_updated, partsgroup_update_last_updated, pricegroup_update_last_updated, sic_update_last_updated, warehouse_update_last_updated | in-use | low | — | — |
| prevent_audit_modification() | audit_log_immutable | retained | low | n/a — Ledgius-shape | — |
| prevent_closed_transactions() | acc_trans_prevent_closed | in-use | high | — | — |
| trigger_open_item_maintenance() | trigger_open_item_maintenance | in-use | high | — | — |
| trigger_duplicate_account_accno() | trigger_duplicate_account_accno | in-use | medium | — | — |
| account_heading__check_tree() | loop_detection | in-use | medium | — | — |
| trigger_duplicate_account_heading_accno() | trigger_duplicate_account_heading_accno | in-use | medium | — | — |
| limit_summary_account_links() | prohibit_multiple_summary_account_links | in-use | medium | — | — |
| cr_report_block_changing_approved() | block_change_when_approved | in-use | medium | — | — |
| cr_report_submitted_update() | cr_report_links_update | in-use | medium | — | — |
| cr_report_line_cleared_update() | cr_report_line_links_update | in-use | medium | — | — |
| cr_report_line_link_insert() | cr_report_line_link_insert | in-use | medium | — | — |
| eca_bu_trigger() | eca_maintain_b_units, eca_maintain_b_units_del | in-use | high | — | — |
| tg_enforce_perms_eclass() | eclass_perms_check | in-use | high | — | — |
| trigger_invoice_prevent_allocation_delete() | trigger_invoice_prevent_allocation_delete | in-use | high | — | — |
| trigger_parts_short() | parts_short | in-use | medium | — | — |
| trigger_workflow_user() | trigger_workflow_user | in-use | medium | — | — |

---

## Completeness summary (auto-calculated by reporting endpoint)

```
Total artifacts inventoried:    33 triggers + 503 functions = 536
Status:
  unmapped:    0
  in-use:      534
  replaced:    0
  dropped:     0
  retained:    2 (audit_log_immutable + prevent_audit_modification)

Completeness:  (replaced + dropped) / (in-use + replaced + dropped)
            =  0 / 534
            =  0.00%
```

A 0.00% starting completeness is correct — this inventory captures the
state at the moment migration tracking was introduced. Per-domain
migrations (each its own task spec) raise the percentage as work lands.
