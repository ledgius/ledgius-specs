# ledgius-specs

This repository is the canonical specification layer for requirements-driven and AI-assisted software delivery.

Its purpose is to provide a durable, structured, human-maintained source of truth that sits above the codebase and guides implementation over time.

## Why this repository exists

AI-assisted code generation is materially more reliable when implementation work is constrained by stable, reviewable specifications rather than conversational prompts alone. Without that control layer, implementation tends to become session-driven rather than system-driven, which increases drift, regressions, inconsistency, and rework.

This repository is intended to:

- define feature intent, scope, constraints, and acceptance criteria in a durable form
- separate business requirements from technical design and implementation planning
- provide traceability from requirements to architecture, tasks, AI guidance, code changes, and pull requests
- preserve implementation intent over time for both humans and AI systems
- reduce ambiguity and uncontrolled expansion of scope during delivery
- support change management by comparing the current canonical domain documents with prior versions

## Core process documents

- [AI-prompt.md](./AI-prompt.md)  
  Top-level instructions for AI systems using this repository. It tells the model to treat the current canonical domain documents as authoritative, compare current content with previous versions to identify requirement changes, and use those changes to guide implementation safely.

- [Requirement Methodology.md](./Requirement%20Methodology.md)  
  Explains the rationale, design principles, and operating model for requirements-driven and AI-assisted delivery.

- [Requirement Canonical Templates.md](./Requirement%20Canonical%20Templates.md)  
  Defines the mandatory document types, metadata, template sections, traceability rules, naming conventions, and working practices.

## Example documents

All examples are located under:

`/example/banking/reconciliation/manual-import-data/`

- `R-0001.md` — example living requirement contract
- `A-0001.md` — example living architecture/design contract
- `T-0001.md` — example implementation task/change plan
- `AI-0001.md` — example AI guidance / implementation steering note

## Canonical document types

The recommended minimum document types are:

- **R** — Requirement: the authoritative statement of what must be true from business and observable-system perspectives
- **A** — Architecture: the technical design and implementation approach for satisfying the requirement
- **T** — Task Plan: the bounded implementation slices and execution order for safe delivery
- **AI** — AI Guidance: explicit steering notes for AI-assisted generation and change analysis

## Recommended repository structure

```text
domains/
  banking/
    reconciliation/
      manual-import-data/
        R-0001.md
        A-0001.md
        T-0001.md
        AI-0001.md
        wireframe-01.png
```

## Operating principles

1. Domain documents are living contracts, not throwaway request tickets.
2. The current version of each canonical document is the authoritative source of truth.
3. Change history is primarily managed through git history and diffs, not by creating long chains of superseding requirement files.
4. Architecture/design documents describe how the requirement will be satisfied.
5. Task plans describe the safest execution sequence.
6. AI guidance documents constrain AI behaviour and reduce drift.
7. Pull requests, commit messages, and selective code comments should reference the small set of canonical documents that govern the affected code.
8. The system should favor a few durable references over many scattered requirement references.

## Notes on provenance in generated code

This starter pack supports provenance references in code, pull requests, and commits.

That is a good practice when it remains concise and standardized. It is useful for:

- traceability
- review context
- auditability
- future AI prompting
- change attribution

The recommended approach is:

- include references in pull requests and commit messages by default
- include concise file-level or subsystem-level provenance comments where they add durable value
- avoid repeating references on every small function or trivial code block
- prefer a few canonical references that act as the implementation contract for the code area

The canonical rules for this are defined in [Requirement Canonical Templates.md](./Requirement%20Canonical%20Templates.md).
