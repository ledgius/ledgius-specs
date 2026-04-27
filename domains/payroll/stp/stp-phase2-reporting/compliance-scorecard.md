# STP Phase 2 + DSP OSF Compliance Scorecard

Periodic compliance review of the Ledgius product against the two ATO documents
that gate whitelisting for STP Phase 2 production lodgement.

**Scope:** ledgius-api, ledgius-web-app, ledgius-db, ledgius-specs.
**Companion spec:** R-0005 (Single Touch Payroll Phase 2 Reporting).
**Score model:** each item carries a weight (1=tail, 2=validation rule, 3=Phase 2 mandatory or OSF mandatory, 4=high impact, 5=blocking). Status factor: PASS=1.0, PARTIAL=0.5, GAP=0.0. Section % = sum(weight x factor) / sum(weight). Combined % = total score / 213.

## Version

| Version | Date scored | Heads (a/w/s/d) | Combined % |
|---------|-------------|-----------------|------------|
| 2.0 | 2026-04-28 | api `aed4656` / web `3f185f0` / specs `32b14fb` / db `origin/master 4a04450` | 26% |
| 2.1 | 2026-04-28 | api `aed4656` / web `3f185f0` / specs `1a0c194` / db `origin/master 4a04450` | 28% |

History before v2.0 (in-chat only, not persisted):
- v1.0 (2026-04-27): STP-only, 2%.
- v1.1 (2026-04-27): STP-only after re-pull, 26% (added STP submission engine slice).
- v2.0 (2026-04-28): expanded to include DSP OSF Cat A; first persisted version.
- v2.1 (2026-04-28): rebase pulled in A-0005 (STP architecture), A-0049 (encryption-at-rest), R-0005 promoted Draft -> Approved, and PAY-STP-011 Payroll ID lifecycle clarification. Closes OSF-A5 (key-management policy now exists as A-0049). Partial close of OSF-A11 (supply chain functional roles documented in A-0005).

## Source documents

| Document | Issuer | Version | Local copy |
|---|---|---|---|
| Single Touch Payroll Phase 2 Extended Conformance Testing Guide | ATO | V2.1, Aug 2022 | not in repo (see /Users/.../Downloads) |
| DSP Operational Security Framework Questionnaire | ATO | V3.2, Sep 2025 | not in repo (see /Users/.../Downloads) |
| Business Implementation Guide PAYEVNT.0004 | ATO | V1.2 | not in repo |
| ATO PAYEVNT.0004 (2020) Package (MST + validation rules) | ATO | V1.3 | not in repo |

## Assumed OSF Category

**Category A** -- commercial cloud SaaS, Payroll/STP high-risk APIs, intent to exceed 10,000 unique TFN records. Cat B applies temporarily while sub-10k; the scorecard sizes for Cat A as the eventual target.

## Headline

| Regime | Score | Weight | % | Delta vs v2.0 |
|---|---|---|---|---|
| STP Phase 2 ECT | 44.5 | 174 | 26% | unchanged |
| DSP OSF Cat A (mandatory controls) | 14.5 | 39 | 37% | +4.0 (A-0049, A-0005 supply chain) |
| **Combined** | **59** | **213** | **28%** | **+4.0** |

ECT-blocking gates cleared: 3 of 6 (unchanged).
OSF-blocking gates cleared: 0 of 3 (MFA, Independent Certification, ABR Entity Validation -- unchanged).

## Per-repo headline

Each control is owned by one or more repos. % is that repo's share of weighted points.

| Repo | STP weight | STP score | OSF weight | OSF score | Combined |
|---|---|---|---|---|---|
| ledgius-api | 113 | 30 (27%) | 18 | 6 (33%) | 36 / 131 = 27% |
| ledgius-web-app | 14 | 0 (0%) | 9 | 1.5 (17%) | 1.5 / 23 = 7% |
| ledgius-db | 30 | 12.5 (42%) | 7 | 2 (29%) | 14.5 / 37 = 39% |
| ledgius-specs | 17 | 2 (12%) | 5 | 5 (100%) | 7 / 22 = 32% |

Per-repo OSF column allocates each control's weight to its primary "owner" repo for the policy/architecture half of the evidence requirement; implementation evidence still rolls up to the code-owning repo even when the policy passes. ledgius-specs now clears its OSF share thanks to A-0049 (key-management policy) and A-0005 (supply-chain functional roles).

## Critical-path gates

These nine items each block whitelisting. Track them tightly.

| Gate | Regime | Status | Owner repo |
|---|---|---|---|
| STP-X01 PAYEVNT.0004 XML serialiser | STP | GAP | api |
| STP-X02 PAYEVNTEMP per-payee mapping | STP | PARTIAL | api |
| STP-S01 M2M auth to EVTE | STP | GAP | api |
| STP-S02 ebMS3 client w/ BMS Vendor & Name | STP | GAP | api |
| STP-Y01 employee_ytd writer | STP | PASS | api + db |
| STP-L01 SUBMIT action handler | STP | PASS | api |
| OSF-A2 Multi-Factor Authentication | OSF | GAP | api + web + specs |
| OSF-A3 Independent Certification (iRAP / ISO 27001:2022) | OSF | GAP | specs (org) |
| OSF-A8 ABN validated against ABR | OSF | GAP | api + web |

---

# Part A -- STP Phase 2 ECT detail

## A.1 Employee data model -- 9 / 22 = 41%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-E01 | TFN value (encrypted) on Employee | 3 | GAP | DB column `employee.tfn_encrypted` exists since V1.08 line 34, but Go `Employee` struct only has `TFNProvided` bool (`ledgius-api/internal/payroll/model.go:23`); no encrypt/decrypt path; V1.60 explicitly defers TFN-at-rest to a follow-up slice (R-0005 PAY-STP-039). |
| STP-E02 | IncomeType on Go Employee | 3 | PASS | `ledgius-api/internal/payroll/model.go:34` |
| STP-E03 | EmploymentBasis on Go Employee | 3 | PASS | `ledgius-api/internal/payroll/model.go:35` |
| STP-E04 | Country code (WHM/IAA) | 1 | PARTIAL | DB column added in V1.60; Go struct does not surface it. |
| STP-E05 | Tax-Free Threshold | 2 | PASS | `ledgius-api/internal/payroll/model.go:24` |
| STP-E06 | SSL/HELP/SFSS | 2 | PARTIAL | `HELPDebt` + `SFSSDebt` flags present; combined SSL view via `tax_declaration` JSONB exists in DB only. |
| STP-E07 | Medicare Levy variation | 2 | PARTIAL | DB JSONB col `tax_declaration` carries the shape; Go struct does not surface it. |
| STP-E08 | Spouse / dependants count | 1 | PARTIAL | DB only. |
| STP-E09 | Cached Tax Treatment Code | 4 | PARTIAL | DB column `tax_treatment_code CHAR(6)` added (V1.60); not on Go struct; no derivation code. |
| STP-E10 | Cessation reason code | 1 | GAP | Not added. |
| STP-E11 | payroll_id / previous_payroll_id | 2 | PARTIAL | DB columns added (V1.60); Go struct does not expose; no allocator. |

## A.2 Employer (Reporting Party) config -- 6 / 8 = 75%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-C01 | ABN with checksum-validated entry | 3 | PARTIAL | `STPEmployerConfig.ABN` stored (`ledgius-api/internal/payroll/stp.go:37`); GET/PUT routes at `/api/v1/stp/employer-config` (`stp_handler.go:129`); no checksum validator. |
| STP-C02 | Branch number (3-digit) | 2 | PASS | `stp.go:38` defaults to `001`. |
| STP-C03 | BMS Vendor + BMS Name + Software ID | 3 | GAP | Not stored anywhere; no ebMS3 client to feed. |

## A.3 Validation algorithms -- 0 / 9 = 0%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-V01 | TFN mod-11 algorithm in `pkg/` | 3 | GAP | `grep -rn "mod.11\|TFN.*algorithm" ledgius-api/pkg` -> no hits. |
| STP-V02 | ABN mod-89 algorithm | 3 | GAP | Only `collapseABN` whitespace stripper in `ledgius-api/internal/banking/normalizer.go:161`; no checksum. |
| STP-V03 | UI surfaces validation errors per ATO section 4.2 | 3 | GAP | No validators bound to UI inputs. |

## A.4 Tax Treatment Code engine -- 0 / 12 = 0%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-T01 | GoRules/CEL TTC decision table | 4 | GAP | No `tax_treatment` bundle; V1.60 defers to follow-up slice. |
| STP-T02 | 28-day no-TFN shift | 4 | GAP | DB column `no_tfn_28day_started_at` exists (V1.60); no scheduler/derivation. |
| STP-T03 | TTC re-derivation triggers | 2 | GAP | Not implemented. |
| STP-T04 | WHM withholding scale | 2 | GAP | PAYG calc still resident/non-resident only (`ledgius-api/internal/payroll/service.go:273-296`). |

## A.5 Pay run disaggregation -- 4.5 / 18 = 25%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-P01 | Gross split into wages/OT/bonus | 5 | PARTIAL | `PayLineBreakdown` reader exists (`stp_service.go:155-162`); pay-run service never writes `breakdown` to `DetailsJSON`; fallback dumps gross to salary_wages. |
| STP-P02 | Allowance categories (CD/AD/LD/MD/RD/TD/OD) | 3 | PARTIAL | Reader/merger present (`stp_service.go:298`); no producer. |
| STP-P03 | Paid-leave types | 3 | GAP | Not modelled. |
| STP-P04 | Lump Sum A/B/D/E/W | 2 | GAP | Not captured. |
| STP-P05 | Salary Sacrifice tracked separate from SG | 3 | PARTIAL | `SalarySacrificeYTD` accumulates from breakdown (`stp_service.go:244`); no producer. |
| STP-P06 | Categorised deductions | 2 | PARTIAL | Reader present, no producer. |

## A.6 YTD tracking -- 12 / 14 = 86%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-Y01 | employee_ytd written each pay-event | 5 | PASS | `stp_service.go:88-95` loops `pr.Lines` -> `applyLineToYTD` -> `UpsertYTD` (atomic in tx); test `TestSTPGeneratePayEvent_AccumulatesAcrossMultipleRuns` (`stp_integration_test.go:188`). |
| STP-Y02 | YTD reconciliation vs pay-run sum | 3 | PARTIAL | Implicit (every line folds in atomically); no explicit reconciliation report. |
| STP-Y03 | YTD transfer between BMS/Payroll IDs | 3 | GAP | DB columns added (V1.60); no transfer logic. |
| STP-Y04 | Per-FY scoping | 3 | PASS | `FinancialYearFor` (`stp_service.go:417`) + composite key `(employee_id, financial_year)`. |

## A.7 PAYEVNT payload generation -- 8 / 22 = 36%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-X01 | XML serialiser to PAYEVNT.0004 MST schema | 5 | GAP | Payload is JSON only (`stp.go:88-148`); doc comment defers wire format to SSP. |
| STP-X02 | PAYEVNTEMP children with all mandatory fields | 5 | PARTIAL | Logical model populated (income type, employment basis, YTDs, allowances, deductions, leave) (`stp_service.go:386-403`); missing TFN, country code, TTC, payroll_id, cessation, lump sums. |
| STP-X03 | PAYEVNT69 Pay/Update Date | 3 | PARTIAL | Pay-run `payment_date` flows but is not surfaced as a discrete field on the payload. |
| STP-X04 | PAYEVNT71 Run Date/Time Stamp | 3 | PARTIAL | `GeneratedAt = time.Now().UTC()` (`stp_service.go:364`); no explicit guard against VR.000194 future-timestamp rule. |
| STP-X05 | Submission ID + Full File Replacement | 3 | GAP | Not implemented. |
| STP-X06 | Period Start/End in PAYEVNTEMP | 3 | GAP | Not on payload. |

## A.8 SBR transmission (ebMS3/AS4) -- 2 / 22 = 9%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-S01 | M2M auth to EVTE | 5 | GAP | None. |
| STP-S02 | ebMS3 client with consistent BMS Vendor/Name | 5 | GAP | Only `StubTransmitter` (records `STUB-{hex}` receipt offline; `stp_service.go:29-39`). |
| STP-S03 | Pull-response handling | 3 | GAP | Not implemented. |
| STP-S04 | Record-delimiter compliance | 2 | GAP | No serialiser. |
| STP-S05 | Retry queue with backoff | 3 | PARTIAL | Manual `Resubmit` exists (`stp_service.go:151`); no scheduled queue or backoff. |
| STP-S06 | XML well-formedness guards | 2 | GAP | No XML. |
| STP-S07 | Different Product ID EVTE vs Prod | 2 | GAP | No registration / no env switch. |

## A.9 Submission lifecycle -- 15 / 17 = 88%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-L01 | SUBMIT (pay event) | 5 | PASS | `POST /api/v1/stp/pay-events` -> `GeneratePayEvent` -> `SubmitEvent` (`stp_handler.go:25-44`). |
| STP-L02 | UPDATE (correction of prior submission) | 5 | PARTIAL | `STPEventUpdate` constant exists (`stp.go:22`); only `Resubmit` (re-sends original payload) is implemented. |
| STP-L03 | EOFY Finalisation | 4 | PASS | `FinaliseEOFY` + `MarkAllTaxReady` (`stp_service.go:167`); test `TestSTPFinaliseEOFY` (`stp_integration_test.go:282`). |
| STP-L04 | ATO response stored with receipt ID | 3 | PASS | `UpdateSubmissionStatus` writes receipt_id, response_payload, submitted_at (`stp.go:283`). |

## A.10 Web UI surfaces -- 0 / 14 = 0%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-U01 | Employer STP config page | 3 | GAP | No route in `ledgius-web-app/src/router.tsx`; API endpoint exists but unconsumed. |
| STP-U02 | Employee form: TFN, income type, employment basis, MLR, country, payroll ID | 4 | GAP | `ledgius-web-app/src/domains/payroll/pages/CreateEmployeePage.tsx` unchanged. |
| STP-U03 | STP submission list | 3 | GAP | No page. |
| STP-U04 | STP submission detail | 2 | GAP | No page. |
| STP-U05 | EOFY finalisation action | 2 | GAP | No page. |

## A.11 ECT/EVTE specifics -- 0 / 7 = 0%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-K01 | Override hook for ECT payer email trigger (`ECTTEST@ect.ato`) | 1 | GAP | Not implemented. |
| STP-K02 | Override hook for ECT payee Address Line 2 trigger (`TestCaseNN.xx`) | 1 | GAP | Not implemented. |
| STP-K03 | EVTE-vs-prod environment flag | 2 | GAP | Transmitter is one stub, not env-switched. |
| STP-K04 | Blocked test ABNs (`34707919409`, `84066105404`) | 1 | GAP | No guard. |
| STP-K05 | TFN scrambling utility for non-prod | 2 | GAP | Not implemented. |

## A.12 Foundations -- 4.5 / 9 = 50%

| ID | Item | W | Status | Verification |
|---|---|---|---|---|
| STP-F01 | ATO Schedule 1 / NAT 1004 PAYG calculator | 3 | PASS | Commit 898b917 added `floor(weekly) + 0.99` tax-basis adjustment + dollar rounding per NAT 1004; covers resident/non-resident TFT brackets -- WHM/no-TFN scales still missing (covered by STP-T04). |
| STP-F02 | Super Guarantee rate table | 2 | PASS | `super_guarantee_rate` table + service. |
| STP-F03 | Pay-run -> GL double-entry posting | 2 | PASS | `ledgius-api/internal/payroll/service.go:198-260`. |
| STP-F04 | DB schema for stp_submission / employee_ytd / stp_employer_config | 2 | PASS | `ledgius-db/migrations/tenant/V1.28__stp_phase2.sql` plus V1.60 employee tax-profile extensions. |

---

# Part B -- DSP OSF Category A detail

| ID | Control | Owner repos | W | Status | Verification |
|---|---|---|---|---|---|
| OSF-A1 | Audit Logging (12-month retention, unique users, no shared logins, IP, event description, success/fail) | db + api | 4 | PARTIAL (2.0) | `audit_log` table is immutable via trigger (`ledgius-db/migrations/tenant/V1.07__recurring_templates_audit_currency.sql:61-91`) -- retention satisfies "must not be deleted within 12 months". Captures user_id, action, entity_type/id, before/after, metadata, ip_address, created_at (`ledgius-api/internal/audit/model.go`). Auth events are NOT written -- `grep audit ledgius-api/internal/platform/oauth_handler.go` returns 0 hits. No login success/failure trail. ICT location not captured. |
| OSF-A2 | Authentication / MFA -- MFA mandatory, idle <=30 min, remember-me <=24h, brute-force lockout <=5 attempts, no social MFA, tokens <=24h | api + web + specs | 5 | GAP (1.0) | Email + bcrypt + JWT (HS256) + refresh-rotation working (`ledgius-api/internal/platform/auth_service.go:51-100`); Google + Microsoft SSO (`oauth_handler.go:44`). MFA explicitly Out of Scope in `R-0041:43`. No idle timeout, no remember-me cap, no brute-force lockout, no rate-limiting on `/auth/login` (R-0041:48). `LoginPage.tsx` has no MFA challenge step. Without MFA, Cat A whitelisting is unattainable. |
| OSF-A3 | Certification -- independent (iRAP or ISO 27001:2022) for Cat A | specs | 4 | GAP (0.0) | No spec, no Statement of Applicability, no engagement letter. `grep -r "ISO 27\|iRAP\|SOC2" ledgius-specs` returns 0 hits. |
| OSF-A4 | Data Hosting -- onshore by default, provider documented | api + web + specs | 3 | PARTIAL (2.0) | Both apps deployed in Sydney: `primary_region = "syd"` in `ledgius-api/fly.toml` and `ledgius-web-app/fly.toml`. Fly.io provider holds SOC 2 / ISO 27001. No spec captures the provider, redundancy region, or hosting policy. |
| OSF-A5 | Encryption Key Management Policy (gen/dist/store/access/renewal/revocation/rotation/archive/length/destroy/recovery) | specs + api | 3 | PASS (3.0) | A-0049 (`domains/architecture/encryption-at-rest/A-0049.md`) is the policy document. Covers all required topics: envelope encryption with per-tenant DEK + platform Master KEK, AES-256-GCM, generation at provisioning, storage in `tenant_data_key` table, in-process LRU cache, KEK + DEK rotation procedures, decryption audit logging, archival via `dek_version`, recovery from KEK loss, key length (256-bit), destruction on tenant deletion. Implementation (`pkg/cryptostore/`) still pending; that side rolls up under OSF-A6 evidence. |
| OSF-A6 | Encryption at Rest -- AES-256 over PII (incl. TFN) | db + api | 5 | PARTIAL (2.0) | Volume-level: PASS (Fly.io disk encryption by default). App-level AES-256-GCM helper exists (`ledgius-api/internal/oauth/crypto.go:17-44`) and is wired to `external_connection.access_token_enc/refresh_token_enc` (`ledgius-db/migrations/tenant/V1.38__external_connection.sql:51-57`). `employee.tfn_encrypted` column has existed since V1.08 line 34 but the Go `Employee` struct does not expose it and nothing writes to it -- TFNs cannot currently be stored at all, encrypted or otherwise. The most sensitive PII for STP is uncovered. **A-0049 now specifies the per-tenant envelope-encryption design and concrete `pkg/cryptostore/` API surface; closure now requires implementation only.** |
| OSF-A7 | Encryption in Transit -- TLS 1.3 minimum | api + web | 4 | PARTIAL (2.5) | `force_https = true` on both fly.toml files. Fly's edge supports TLS 1.3 (default 1.2+); min-version not pinned in code or fly.toml `[[services]]` block. Internal API<->DB over Fly's private 6PN (encrypted) -- but `sslmode` not set explicitly in DB DSN. SSL Labs report not produced. |
| OSF-A8 | Entity Validation -- verify ABN against ABR; valid client email + phone | api + web + specs | 3 | GAP (0.0) | Tenants store ABN per `R-0041:123`. No ABR lookup (`grep -r "abr\.gov\.au\|AbnLookup" ledgius-api` returns 0 hits). Email verification is Out of Scope in R-0041. Phone not collected. |
| OSF-A9 | Personnel Security -- hiring/screening/separation policy | specs | 2 | GAP (0.0) | No spec. (Likely qualifies for Micro DSP exemption today if <=3 employees with no contractor source-code access -- should be documented either way.) |
| OSF-A10 | Security Monitoring -- IDS/IPS, anomaly detection, incident dashboard | api + specs | 4 | GAP (1.0) | Structured `slog` logs (`ledgius-api/CLAUDE.md` Logging section). Fly.io edge provides DDoS protection. No app-level IDS, no anomaly rules, no SIEM, no incident-management dashboard, no alerting policy. |
| OSF-A11 | Supply Chain -- functional roles (Collector/Validator/Integrator/Transformer/Provider/Transmitter) | specs | 2 | PARTIAL (1.0) | A-0005 §"Component Overview" + §"SBR Intermediary Client" documents the supply chain functional roles: Ledgius API as Data Collector / Validator / Integrator / Transformer / Provider; SBR Intermediary (MessageXchange or Ozedi) as Data Transmitter; ATO SBR Gateway as receiving party. Decision matrix between MessageXchange and Ozedi captured in A-0005 §"Decision Matrix". **Outstanding for full PASS:** intermediary selection + intermediary entity name and ABN, which are TBC pending sales engagement (A-0005 explicitly defers this). |
| OSF-A12 | Third-Party Add-on Marketplace (SSAM) | n/a | -- | N/A | Ledgius does not offer a third-party API marketplace today; control is not applicable. Re-evaluate if/when one is added. |

## OSF section roll-up

| Item | W | Score | v2.0 -> v2.1 |
|---|---|---|---|
| OSF-A1 Audit Logging | 4 | 2.0 | -- |
| OSF-A2 Authentication / MFA | 5 | 1.0 | -- |
| OSF-A3 Certification | 4 | 0.0 | -- |
| OSF-A4 Data Hosting | 3 | 2.0 | -- |
| OSF-A5 Key Management | 3 | 3.0 | +3.0 (A-0049 published) |
| OSF-A6 Encryption at Rest | 5 | 2.0 | -- (architecture now spec'd; impl pending) |
| OSF-A7 Encryption in Transit | 4 | 2.5 | -- |
| OSF-A8 Entity Validation | 3 | 0.0 | -- |
| OSF-A9 Personnel Security | 2 | 0.0 | -- |
| OSF-A10 Security Monitoring | 4 | 1.0 | -- |
| OSF-A11 Supply Chain | 2 | 1.0 | +1.0 (A-0005 §Component Overview) |
| **Total** | **39** | **14.5** | **+4.0** |

---

# Top of-priority gaps (cross-cutting, highest leverage)

1. **TFN field flow end-to-end (api + web + db)** -- `tfn_encrypted` column exists in DB since V1.08; needs:
   - `EmployeeTFN` field on Go struct + encrypt-on-write via existing `oauth/crypto.go` AES-256-GCM helper.
   - mod-11 validator in `pkg/validate/tfn.go`.
   - TFN input on web employee form (masked, never re-displayed).
   - This single thread closes STP-V01, OSF-A6 (PII path), and parts of STP-E01 / STP-U02.
2. **MFA implementation (OSF-A2)** -- required for Cat A whitelisting. Recommended path: TOTP (RFC 6238) + WebAuthn -- a green-field slice spanning api auth_service, web LoginPage, and an R-0041 update or new R document.
3. **Authentication audit-event writes (OSF-A1)** -- `auth_service.Login/SwitchTenant/Refresh` must call `audit.Repository.Create` on success/failure. Small change, big OSF compliance gain.
4. **ABR ABN-lookup integration (OSF-A8)** -- wire a `pkg/abr` client into tenant signup; small but mandatory.
5. **OSF spec set in ledgius-specs** -- A-0005 (STP architecture) and A-0049 (encryption-at-rest policy) **landed in v2.1**. Still outstanding: R/A doc for MFA + idle-timeout + brute-force lockout (closes OSF-A2 spec side), R doc for hosting/redundancy policy (closes OSF-A4 spec side), Statement of Applicability vs ISO 27001:2022 / OWASP ASVS (OSF-A3), Personnel Security policy or Micro-DSP exemption letter (OSF-A9), Entity Validation / ABR-lookup spec (OSF-A8 spec side).
6. **PAYEVNT XML serialiser + real SBR transmitter (STP-X01/S01/S02)** -- still the biggest single STP slice; pick an SSP (MessageXchange/Ozedi) to avoid direct ebMS3/AS4 work.

# How to re-score (next review)

1. `cd ledgius-api && git pull --ff-only` (and same for web-app, specs, db; for db, only fetch if on a feature branch).
2. For each row above, run the verification command/path; set status PASS / PARTIAL / GAP.
3. Recompute section % = `Sum(weight x factor) / Sum(weight)` and combined % = `score / 213`.
4. Update the Version table at the top of this file; commit with message `chore(specs): STP+OSF compliance scorecard vN.M`.
5. IDs are stable across versions -- the diff between v2.0 and vN is one-to-one and tells you which gaps closed and which regressed.

# Notes for next reviewer

- **OSF Cat changes with scale.** Cross 10,000 unique TFN/super records and the questionnaire forces Cat A regardless of intent. Recompute the OSF weight only if dropping to Cat B/C.
- **ledgius-db branch state.** v2.0 inspected `origin/master` because the local branch was `feat/qa-golden-v2` (no upstream). v2.1 inspected the same. If db is on a different branch on review day, document which ref was scored.
- **Don't confuse STP scope and OSF scope.** STP-S02 (ebMS3 client) is a transport requirement; OSF-A6/A7 (encryption) are platform requirements. They overlap only at the wire.
- **Critical-path priority.** The 9 gates above are non-negotiable for whitelisting; everything else is a depth-of-coverage concern. If only one of the 9 is open, you cannot lodge to production regardless of total %.
- **Spec-vs-impl distinction.** Several scorecard items are co-owned by ledgius-specs (the design exists) and a code repo (the implementation exists). PASS for OSF policy controls (e.g. OSF-A5) is satisfied by a published spec; PASS for STP implementation items (e.g. STP-X01) requires running code. Don't conflate the two when scoring -- check the verification column.
- **R-0005 status.** R-0005 is now Approved (since 2026-04-27); A-0005 architecture exists. Spec-driven implementation work (T-0005 task plan, when written) is therefore unblocked. STP scoring still measures implementation, not spec status.
- **Terminology convention.** The repo now requires every spec to include a `# Terms` section (per `CLAUDE.md` §Terminology). Any new R or A doc the scorecard pushes for must follow that convention.
