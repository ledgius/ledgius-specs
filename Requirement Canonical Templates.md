# Requirement Canonical Templates

## Purpose

This document defines the mandatory document types, metadata, naming rules, section templates, and traceability rules for the `ledgius-specs` repository.

It is the canonical reference for how the requirements process operates.

## Canonical goals

The process must:

- preserve stable delivery intent
- support both human and AI consumption
- provide traceability to implementation
- reduce ambiguity and drift
- remain low-tech and easy to maintain

## Document types

The standard document types are:

- `R` — Requirement
- `A` — Architecture / Design
- `T` — Task Plan / Execution Plan
- `AI` — AI Guidance / Steering Note

## ID conventions

Each document type uses a stable identifier.

Examples:

- `R-0001`
- `A-0001`
- `T-0001`
- `AI-0001`

### Alignment rules

- `R-0001` is the primary requirement identifier.
- `A-0001`, `T-0001`, and `AI-0001` should align to the same feature where possible.
- Additional related documents may use suffixes where needed, for example `A-0001-01` or `AI-0001-02` if the feature grows in complexity.

## Repository structure

Recommended structure:

```text
domains/
  <domain>/
    <sub-domain>/
      <feature-slug>/
        R-0001.md
        A-0001.md
        T-0001.md
        AI-0001.md
        supporting-assets...
```

Example:

```text
domains/
  banking/
    reconciliation/
      manual-import-data/
        R-0001.md
        A-0001.md
        T-0001.md
        AI-0001.md
```

## Mandatory metadata

Every canonical document must begin with a metadata block using the following format.

```md
ID: R-0001
Title: Manual Import Data
Domain: Banking/Reconciliation
Feature: manual-import-data
Status: Draft
Owner: Team Ledger
Created: 2026-04-10
Updated: 2026-04-10
Related Requirements:
  - R-0001
Related Architecture:
  - A-0001
Related Tasks:
  - T-0001
Related AI Guidance:
  - AI-0001
Impacted Repositories:
  - ledgius-api
  - ledgius-web
Supersedes:
Superseded By:
```

### Metadata rules

- `ID`, `Title`, `Domain`, `Status`, `Owner`, `Created`, and `Updated` are mandatory.
- Related document fields must be present even if empty.
- `Impacted Repositories` must be populated whenever known.
- `Supersedes` and `Superseded By` must be populated when lifecycle changes require it.

## Lifecycle statuses

Allowed statuses:

- `Draft`
- `Approved`
- `In Progress`
- `Implemented`
- `Deprecated`
- `Superseded`

### Lifecycle rules

- Only `Approved` requirements should be used as the basis for production implementation unless an explicit exception is made.
- `Deprecated` and `Superseded` documents must not be used as the primary source for new implementation work.
- If a requirement changes materially, either revise it carefully with update history or create a new requirement and mark the old one `Superseded`.

## Canonical template: Requirement (`R`)

```md
ID: R-0001
Title: <title>
Domain: <domain/sub-domain>
Feature: <feature-slug>
Status: Draft
Owner: <owner>
Created: YYYY-MM-DD
Updated: YYYY-MM-DD
Related Requirements:
  - R-0001
Related Architecture:
  - A-0001
Related Tasks:
  - T-0001
Related AI Guidance:
  - AI-0001
Impacted Repositories:
  - <repo>
Supersedes:
Superseded By:

# Summary

# Problem / Business Context

# Scope

# Out of Scope

# Actors / Users

# Preconditions

# Functional Requirements

# Data / Entities / Fields

# UX / UI Behaviour

# Validation Rules

# Error Handling

# Security / Permissions

# Acceptance Criteria

# Open Questions

# Related Documents
```

### Requirement rules

- Acceptance criteria are mandatory.
- Out-of-scope statements are mandatory.
- Requirements must describe observable behaviour, not implementation detail unless the detail is itself a requirement.
- If wireframes or mockups exist, they must be linked from the requirement.

## Canonical template: Architecture (`A`)

```md
ID: A-0001
Title: <title>
Domain: <domain/sub-domain>
Feature: <feature-slug>
Status: Draft
Owner: <owner>
Created: YYYY-MM-DD
Updated: YYYY-MM-DD
Related Requirements:
  - R-0001
Related Architecture:
  - A-0001
Related Tasks:
  - T-0001
Related AI Guidance:
  - AI-0001
Impacted Repositories:
  - <repo>
Supersedes:
Superseded By:

# Summary

# Requirement Link

# Technical Context

# Proposed Design

# Affected Components

# Data Flow

# API / Interface Changes

# Storage / Schema Changes

# Background Processing

# Risks / Trade-offs

# Alternatives Considered

# Test Strategy

# Rollout / Migration Notes

# Related Documents
```

### Architecture rules

- Architecture documents should be created by default, even if brief.
- They must define system boundaries, not just implementation preferences.
- They must identify what should be reused, what should be changed, and what should not be touched.

## Canonical template: Task Plan (`T`)

```md
ID: T-0001
Title: <title>
Domain: <domain/sub-domain>
Feature: <feature-slug>
Status: Draft
Owner: <owner>
Created: YYYY-MM-DD
Updated: YYYY-MM-DD
Related Requirements:
  - R-0001
Related Architecture:
  - A-0001
Related Tasks:
  - T-0001
Related AI Guidance:
  - AI-0001
Impacted Repositories:
  - <repo>
Supersedes:
Superseded By:

# Summary

# Requirement and Design References

# Assumptions

# Preconditions

# Implementation Slices

# Recommended Execution Order

# Testing Tasks

# Rollout Tasks

# Done Criteria

# Related Documents
```

### Task plan rules

- Use a task plan whenever work benefits from bounded execution slices.
- Implementation slices should be small enough for safe AI-assisted generation and review.
- The task plan should define a recommended order of work and clear completion criteria.

## Canonical template: AI Guidance (`AI`)

```md
ID: AI-0001
Title: <title>
Domain: <domain/sub-domain>
Feature: <feature-slug>
Status: Draft
Owner: <owner>
Created: YYYY-MM-DD
Updated: YYYY-MM-DD
Related Requirements:
  - R-0001
Related Architecture:
  - A-0001
Related Tasks:
  - T-0001
Related AI Guidance:
  - AI-0001
Impacted Repositories:
  - <repo>
Supersedes:
Superseded By:

# Summary

# Authoritative Sources

# Implementation Boundaries

# Reuse Expectations

# Modules / Components to Prefer

# Modules / Components to Avoid

# Non-goals

# Testing Expectations

# Provenance Expectations

# Prompting Notes

# Related Documents
```

### AI guidance rules

- Use this document to constrain AI behaviour explicitly.
- It must not replace the requirement or architecture documents.
- It may include prompt-ready implementation steering.

## Traceability rules

### Pull requests

Every pull request implementing or changing behaviour tied to a requirement must reference the governing document IDs.

Recommended pull request section:

```md
## Specification References
- Requirement: R-0001
- Architecture: A-0001
- Task Plan: T-0001
- AI Guidance: AI-0001
```

### Commit messages

Recommended format:

```text
R-0001: add CSV upload validation endpoint
```

or

```text
R-0001 A-0001: implement import parsing service
```

### Code comments and provenance

I agree with including provenance references, with discipline.

#### Canonical rule

AI-generated or AI-assisted code should include concise provenance comments when one of the following is true:

- the file or function implements non-trivial business rules
- the linkage to the requirement materially helps future maintenance
- a reviewer would benefit from knowing the governing specification sources

#### Avoid

- repeating references in every trivial helper
- adding noisy comments with no maintenance value
- creating provenance comments that drift out of date without review

#### Recommended formats

File-level comment:

```go
// Implements manual bank import processing.
// Spec references: R-0001, A-0001, AI-0001.
```

Function-level comment:

```go
// validateImportedRows applies acceptance criteria from R-0001.
// Parsing and deduplication constraints are defined in A-0001.
```

#### Minimum provenance requirement

At least one of the following should exist for any substantive change:

- pull request spec references
- commit message reference to the primary requirement
- targeted code comment where it adds durable value

That balances traceability with code cleanliness.

## Working rules for AI-assisted implementation

When using AI to generate or modify code:

1. Provide the relevant `R`, `A`, `T`, and `AI` documents as the authoritative context.
2. Instruct the AI to implement only approved scope.
3. Require the AI to satisfy all acceptance criteria.
4. Require the AI to respect out-of-scope items and non-goals.
5. Require the AI to reference governing documents in the pull request and, where appropriate, in concise code comments.
6. Require tests to align to acceptance criteria and architecture constraints.

## Governance rules

- Do not implement against draft documents unless explicitly authorized.
- Do not silently change behaviour without updating the governing specification.
- Do not leave superseded specifications ambiguous.
- Do not use AI guidance as a substitute for missing requirements.

## Summary

These templates and rules define the canonical structure for requirements-driven, traceable, and AI-assisted delivery in `ledgius-specs`.
