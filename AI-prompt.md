# AI Prompt

## Purpose

This document provides the top-level operating instructions for any AI system using the `ledgius-specs` repository to review, generate, modify, or validate code.

The objective is to ensure that AI-assisted work remains aligned to the current canonical domain contracts and that requirement changes are identified through disciplined comparison with prior versions.

## Authoritative source rule

Treat the current version of the canonical domain documents as the authoritative source of truth.

The canonical documents are normally:

- `R-xxxx` — requirement contract
- `A-xxxx` — architecture/design contract
- `T-xxxx` — task or execution plan
- `AI-xxxx` — AI steering note

Do not treat older versions, stray notes, historical prompts, or inferred assumptions as equal authority.

## Change analysis rule

Before proposing or generating code changes:

1. Read the current canonical domain documents.
2. Compare the current version of each relevant document with its previous git version.
3. Identify what changed in:
   - scope
   - behaviour
   - validation
   - data or fields
   - API/interface contracts
   - non-functional constraints
   - out-of-scope boundaries
4. Treat those differences as the change-management input.
5. Ensure the generated implementation responds to the deltas, not just the full document in isolation.

## Working assumptions

The system is designed around living canonical contracts.

This means:

- the current `R` and `A` documents are expected to evolve organically over time
- they remain the north star for the code area they govern
- git history provides historical change context
- the AI should not expect dozens of superseding requirement files for the same feature
- the AI should not scatter many document references through code if a few canonical references are sufficient

## Implementation behaviour required from AI

When generating or reviewing code, the AI must:

- use the current canonical documents as the implementation contract
- compare current and prior document versions to detect change
- preserve stated scope and out-of-scope boundaries
- avoid inventing architecture, data fields, workflow steps, or UI behaviour not supported by the canonical documents
- respect the architecture contract where it constrains package boundaries, interfaces, storage, validation location, or sequencing
- use the task plan when sequencing or slicing work
- use the AI guidance document for style, guardrails, reuse expectations, and anti-pattern avoidance

## Provenance behaviour required from AI

The AI should record which canonical documents governed the change.

Default provenance pattern:

- PR description: always reference governing `R/A/T/AI` docs
- commit message: reference governing docs where practical
- code comments: add concise provenance comments only at durable boundaries such as a file header, package header, subsystem entry point, or non-obvious implementation block

Avoid noisy provenance such as repeating document references on every helper function or minor line-level change.

## Review behaviour required from AI

When asked to review existing code, the AI should:

1. identify the governing canonical docs
2. compare current docs with previous versions
3. identify whether the code reflects the latest contract
4. highlight mismatches between code and the current contract
5. highlight areas where the code still reflects an earlier version of the contract
6. distinguish clearly between:
   - required changes
   - optional improvements
   - unsupported assumptions

## Output expectations

When producing recommendations or code, the AI should explicitly state:

- which canonical documents were used
- what requirement changes were identified from the previous version
- which parts of the implementation are directly required by the contract
- any material uncertainty caused by gaps in the documents

## Refusal rule for ambiguity

If the canonical documents materially conflict or leave a critical behaviour unspecified, the AI should not fabricate certainty. It should identify the gap clearly and propose the smallest safe interpretation.
