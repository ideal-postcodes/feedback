# Security Policy

Found a security issue in an Ideal Postcodes product? Please report it privately — **do not open a public issue**.

## How to report

**Preferred:** use GitHub's private vulnerability reporting on this repo — [Report a vulnerability](https://github.com/ideal-postcodes/feedback/security/advisories/new). It's encrypted and routes straight to the team.

**Email fallback:** [support@ideal-postcodes.co.uk](mailto:support@ideal-postcodes.co.uk) with subject prefix `[security]`.

Include:

- Product affected (CLI, API, Address Finder, Postcode Lookup, skills, docs, etc.)
- Version / endpoint / commit SHA
- Steps to reproduce
- Impact (what an attacker can do)
- Any logs, requests, or PoC — redact your own credentials and any third-party data

We'll acknowledge within 2 working days and keep you updated as we triage and fix.

## Scope

In scope — the products this tracker covers:

- `@ideal-postcodes/cli`
- Ideal Postcodes API (`api.ideal-postcodes.co.uk`)
- `@ideal-postcodes/address-finder`, `@ideal-postcodes/postcode-lookup`
- `@ideal-postcodes/skills`
- [docs.ideal-postcodes.co.uk](https://docs.ideal-postcodes.co.uk)

Out of scope — report in the relevant repo:

- Ecommerce integrations: [`woocommerce`](https://github.com/ideal-postcodes/woocommerce), [`magento`](https://github.com/ideal-postcodes/magento), [`shopify`](https://github.com/ideal-postcodes/shopify), [`bigcommerce-app`](https://github.com/ideal-postcodes/bigcommerce-app), [`salesforce`](https://github.com/ideal-postcodes/salesforce)

## Please don't

- Post vulnerabilities, exploits, or PoCs in public issues or PRs.
- Include real API keys, user tokens, customer addresses, or other personal data — even in private reports. Redact and reference instead.
- Run automated scans, brute force, or load tests against production. We can provide a sandbox if you need one — ask first.

## Disclosure

We'll coordinate disclosure with you once a fix is released. Credit is given by default unless you'd rather stay anonymous.
