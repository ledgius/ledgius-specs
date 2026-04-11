# Ledgius Specs — Claude Code Project Guide

## Project Overview

Canonical specification repository for requirements-driven and AI-assisted software delivery. This repo is the authoritative source of truth for what must be built, how, and why.

- **Organisation**: `github.com/ledgius`

## Document Types

- **R-xxxx** — Requirement: what must be true from business and observable-system perspectives
- **A-xxxx** — Architecture: technical design and implementation approach
- **T-xxxx** — Task Plan: bounded implementation slices and execution order
- **AI-xxxx** — AI Guidance: steering notes for AI-assisted implementation

## Structure

```
domains/
  architecture/       — Cross-cutting architecture decisions (A-0009 to A-0016)
  compliance/         — AU tax, regulatory requirements (R-0021, AI-0021)
  import/             — Data import pipeline (R-0017, A-0017, A-0018)
  banking/            — Reconciliation workflow (R-0019, A-0019)
  knowledge/          — Knowledge pipeline (R-0008, A-0020, AI-0023)
  payroll/            — Employee, pay run, leave, STP, super, PAYG (R-0002 to R-0007)
  ledger/             — Chart of accounts, tax codes (R-0024, R-0025)
  sales/              — Invoices, credit notes, receipts (R-0026 to R-0028)
  purchases/          — Bills, debit notes, payments (R-0029 to R-0031)
  tax/                — BAS reporting (R-0032)
  reporting/          — Financial reports (R-0033)
  contacts/           — Contact management (R-0034)
  dashboard/          — Operational dashboard (R-0035)
  recurring/          — Recurring schedules (R-0036)
  products/           — Product catalogue (R-0037)
  currency/           — Exchange rates (R-0038)
  feedback/           — User feedback system (R-0039)
  audit/              — Audit trail (R-0040)
  platform/           — Auth & RBAC (R-0041)
  templates/          — Transaction templates (R-0042)
```

## Conventions

### IDs
- Globally unique across the entire repo
- R-0001 through R-0042+ for requirements
- A-0001 through A-0020+ for architecture
- T-0022 for task plans
- AI-0021, AI-0023 for AI guidance
- Aligned: R-0017 and A-0017 govern the same feature (import pipeline)

### Metadata (mandatory on every document)
- ID, Title, Domain, Feature, Status, Owner, Created, Updated
- Related Requirements/Architecture/Tasks/AI Guidance
- Impacted Repositories
- Supersedes / Superseded By

### Statuses
- Draft → Approved → In Progress → Implemented → Deprecated / Superseded

### Rules
- Acceptance criteria are mandatory on R documents
- Out-of-scope statements are mandatory
- Architecture documents created by default, even if brief
- Don't implement against Draft without explicit authorisation
- Current version is the authoritative source — use git history for change tracking

### Traceability
- PRs reference governing spec IDs in the description
- Commit messages reference primary requirement
- Source code has file-level provenance comments: `// Spec references: R-XXXX, A-XXXX.`

## Core Process Documents

- `AI-prompt.md` — Instructions for AI systems using this repo
- `Requirement Methodology.md` — Rationale and operating model
- `Requirement Canonical Templates.md` — Templates, metadata, naming, traceability rules
