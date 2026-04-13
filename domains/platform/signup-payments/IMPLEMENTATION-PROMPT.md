# Implementation Prompt — Signup, Payments & Trial Management

Copy the text below and paste it into Claude Code to start implementing this feature. Claude will show you the plan first and ask for your confirmation before making any changes.

---

## Prompt to paste into Claude Code:

```
I need to implement the Signup, Payments & Trial Management feature for Ledgius. This is defined in two specification documents:

- Requirements: ledgius-specs/domains/platform/signup-payments/R-0048.md
- Architecture: ledgius-specs/domains/platform/signup-payments/A-0024.md

Please read both spec documents carefully, then present me with:

1. **Implementation Plan** — a numbered list of every file that needs to be created or modified, grouped by repo (ledgius-db, ledgius-api, ledgius-website, ledgius-web-app), in the order they should be built
2. **Phase breakdown** — which phases from A-0024 you'll implement and in what order
3. **Dependencies** — what needs to be set up before coding starts (Stripe account, API keys, etc.)
4. **Estimated scope** — how many files will be created/modified per repo
5. **What I need to do** — any manual steps I need to take (e.g., create Stripe products, set DNS, configure secrets)

DO NOT start coding until I confirm the plan by saying "proceed" or "go ahead".

After I confirm, implement each phase one at a time. After each phase:
- Show me what was built
- Run any tests
- Ask me to verify before moving to the next phase

Important context:
- The repos are at ~/dev/crestline/accounting/ (ledgius-api, ledgius-web-app, ledgius-db, ledgius-website, ledgius-specs, ledgius-infra)
- The API uses Go 1.25, Gin, GORM, PostgreSQL
- The website and web app use React 19, TypeScript, Vite, Tailwind CSS v4
- Payment processing uses Stripe (we need to set up a Stripe account first if not done)
- Emails use Resend (already configured)
- Deployment is on Fly.io (Sydney region)
- Read the CLAUDE.md in each repo for coding conventions
- Create feature branches: feat/signup-payments in each repo
- Do NOT raise PRs until I've tested and confirmed each phase works
```

---

## Tips for the person running this:

1. **Open Claude Code** in the terminal: `cd ~/dev/crestline/accounting && claude`
2. **Paste the prompt** above
3. **Wait for the plan** — Claude will read the specs and present a detailed plan
4. **Review the plan** — make sure it makes sense, ask questions if anything is unclear
5. **Say "proceed"** to start implementation
6. **After each phase** — Claude will pause and ask you to verify. Test it locally with `make dev` from ledgius-infra
7. **If something breaks** — tell Claude what happened (paste the error). It will fix it.
8. **To deploy** — Claude will offer to deploy. Say yes when ready.

## What you'll need before starting:

- [ ] A Stripe account (test mode is fine for development) — https://dashboard.stripe.com/register
- [ ] Create 4 products in Stripe matching our plans (Starter $0, Essential $29, Professional $59, Business $99)
- [ ] Copy the Stripe secret key, webhook secret, and 4 price IDs
- [ ] Access to the Fly.io dashboard (to set secrets)
