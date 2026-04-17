# Policy Registry

Centralised registry of compliance, regulatory, and professional obligations that govern Ledgius features. Each policy is a YAML file carrying structured metadata — the web app's `usePagePolicies` hook and help panel "Policies" sections reference these by code.

## Why centralised

Most policies cut across multiple domains (ATO record-keeping affects export, import, audit, reporting). A single `/policies` directory avoids duplication — the `applies_to` field on each policy is the join between policy and domain.

## File naming

`P-NNNN-short-slug.yaml` — e.g. `P-0001-ato-record-keeping.yaml`

## Schema

```yaml
code: P-0001
version: "1.0"
title: "ATO Electronic Record-Keeping"
short_title: "ATO TR 2018/2"
jurisdiction: AU
authority: Australian Taxation Office
source_url: https://...
effective_from: "2018-01-01"
effective_to: null              # null = still in force
summary: >
  One-paragraph plain-English summary.
applies_to:
  - export
  - import
  - audit
  - reporting
severity: mandatory             # mandatory | recommended | advisory
tags:
  - record-keeping
  - electronic-records
```

## How the web app consumes this

1. `usePagePolicies(["export", "tax"])` — the hook loads all policies where `applies_to` includes any of the listed domains
2. Help panel "Policies" section — cites `short_title` + `summary` from the matched policies
3. Export page sidebar — lists governing policies with links to source URLs
