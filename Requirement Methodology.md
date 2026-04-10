# Requirement Methodology

## Purpose

This document defines the rationale and operating approach for using a dedicated requirements repository to guide long-lived, AI-assisted software delivery.

The intent is to establish a low-tech, durable, and disciplined control mechanism that keeps human and AI implementation work aligned over time.

## Core position

AI-assisted code generation becomes significantly more reliable when a stable specification layer exists above the codebase.

Without that layer, implementation tends to optimize for local completion rather than long-term coherence. Over time this produces drift, duplicated logic, inconsistent patterns, ambiguous scope, and subtle regressions.

A dedicated specification repository addresses that problem by preserving system intent in a structured, reviewable, version-controlled form.

## Why this exists

The repository exists to provide four essential functions.

### 1. Constraint

It constrains implementation by defining the intended scope, required behaviours, validation rules, and acceptance criteria.

### 2. Memory

It preserves decisions across sessions, contributors, and implementation cycles.

### 3. Traceability

It links requirements to design decisions, task plans, AI guidance, code changes, and pull requests.

### 4. Drift detection

It makes it possible to compare code behaviour against approved intent and identify when implementation has deviated.

## What problem this solves

Without a durable specification layer, AI-assisted delivery typically suffers from the following failure modes:

- loss of alignment with business intent
- architectural drift across repositories and services
- incomplete handling of edge cases and validation rules
- inconsistent implementation of similar features
- accidental expansion of scope
- regressions introduced by changes that were locally plausible but globally incorrect
- wasted time re-prompting the AI with missing context

## Repository design principles

The repository should follow these principles.

### Separation of concerns

The repository must distinguish clearly between:

- what the business and system need
- how the system should behave
- how the solution will be implemented
- how work should be sequenced
- what constraints should govern AI-assisted generation

### Stability

Requirement documents should remain stable, durable, and reviewable. They should not be treated as temporary notes or disposable prompt fragments.

### Low-tech simplicity

The system should be easy to maintain with plain markdown, version control, and disciplined templates. No specialized tooling is required to begin.

### Human readability and AI usability

Documents must be written so that both humans and AI systems can reliably consume them. This means using consistent metadata, headings, sections, identifiers, and terminology.

### Explicit boundaries

Every requirement should define scope and out-of-scope items to reduce ambiguity and prevent uncontrolled solution expansion.

## Canonical document model

The recommended minimum document model contains four document types.

### Requirement document (`R`)

The requirement document is the canonical statement of what must be true from the business and observable-system perspective.

It should define:

- business context
- scope
- out of scope
- users or actors
- functional requirements
- data and field requirements
- UX/UI behaviour
- validation rules
- error handling expectations
- security or permissions expectations
- acceptance criteria

### Architecture document (`A`)

The architecture document defines the technical design used to satisfy the requirement.

It should define:

- affected systems, components, and repositories
- technical constraints
- data flow
- interfaces and contracts
- schema or storage changes
- integration points
- alternatives considered
- risks and trade-offs
- testing and rollout considerations

### Task plan document (`T`)

The task plan provides bounded implementation slices and an execution sequence.

It exists because requirements and design alone do not always provide the safest order of work for humans or AI.

It should define:

- implementation steps
- recommended sequence
- dependencies
- test work
- migration or rollout tasks
- review checkpoints

### AI guidance document (`AI`)

The AI guidance document provides explicit steering instructions for AI-assisted implementation.

It should define:

- which documents are authoritative
- reuse expectations
- modules to extend or avoid
- anti-patterns to avoid
- non-goals
- test expectations
- provenance expectations

## On architecture documents being optional

A fully separate architecture document may be short, but the technical implementation intent should not be omitted.

Even when a feature appears simple, AI-assisted delivery benefits from having technical constraints and boundaries made explicit. What appears obvious to a developer today may not remain obvious later to a different contributor or an AI model.

For that reason, either:

- architecture documents should be created by default, even if brief, or
- a mandatory technical design section must exist inside the requirement document

The preferred approach in this methodology is to create an `A` document by default.

## On acceptance criteria

Acceptance criteria are mandatory.

They are the most effective way to convert a broad feature request into a testable delivery target.

For AI-assisted generation, acceptance criteria sharply reduce ambiguity because they define observable success conditions rather than broad intentions.

## On status and lifecycle

Every document must carry explicit lifecycle metadata.

At minimum this should include:

- ID
- title
- domain
- status
- owner
- created date
- updated date
- related documents
- impacted repositories

Recommended statuses are:

- Draft
- Approved
- In Progress
- Implemented
- Deprecated
- Superseded

This prevents stale documentation from being treated as active truth.

## On traceability to code

A specification repository is only effective if code changes trace back to it.

Therefore:

- pull requests should reference the relevant `R`, `A`, `T`, and `AI` IDs
- commit messages should reference the primary requirement where practical
- major code changes should preserve implementation provenance
- deprecated or superseded specifications must be marked explicitly

## On provenance comments in generated code

Provenance references are useful and recommended, with discipline.

The goal is not to annotate every line of code. The goal is to make it clear which specification sources governed a meaningful implementation or change.

Recommended practice:

- always include spec references in the pull request description
- include concise references in package-level, file-level, or function-level comments when the linkage aids future maintenance
- avoid repetitive or noisy comments on trivial code paths

A concise style is preferred, for example:

```go
// Implements CSV import validation rules for R-0001.
// Design constraints: A-0001.
// AI steering used: AI-0001.
```

## Working model

The intended workflow is:

1. Create or update the requirement document.
2. Create or update the architecture/design document.
3. Create a task plan if implementation requires bounded execution slices.
4. Create AI guidance where explicit steering is useful.
5. Use those documents as the authoritative source for implementation prompts and human development.
6. Reference the documents in pull requests, commits, and selected code comments.
7. Update document lifecycle status as work progresses.

## Benefits

If applied consistently, this methodology should improve:

- implementation accuracy
- review quality
- onboarding clarity
- architectural consistency
- regression avoidance
- AI prompt quality
- long-term maintainability

## Summary

The specification repository is not just documentation. It is the operational control surface for requirements-driven and AI-assisted delivery.

Its value comes from providing a stable source of intent, explicit constraints, traceability, and bounded implementation guidance over time.
