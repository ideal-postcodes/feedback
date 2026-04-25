# AGENTS.md — Filing Issues Programmatically

This document is for AI coding agents (Claude Code, Cursor, Codex, etc.) and CLI/API automation that need to file bugs or feature requests against Ideal Postcodes products.

## TL;DR

Use the `gh` CLI with one of the markdown templates:

```bash
gh issue create \
  --repo ideal-postcodes/feedback \
  --template bug_report.md \
  --title "[bug] idpc cleanse: foo" \
  --body "$(cat <<'EOF'
## Product
- [x] CLI (@ideal-postcodes/cli)

## Version
@ideal-postcodes/cli v0.1.0

## What happened
…
EOF
)"
```

That's it. The repo is public; any GitHub account can file.

## Before filing

1. **Check existing issues.** Search first; don't file duplicates.
   ```bash
   gh issue list --repo ideal-postcodes/feedback --search "your-query-here"
   ```
2. **Check the docs.** Many "is this a bug?" questions are answered at [docs.ideal-postcodes.co.uk](https://docs.ideal-postcodes.co.uk).
3. **Redact secrets.** Never include `api_key`, `user_token`, customer addresses, emails, or other personal data. Issues are public and indexed.
4. **Pick the right product.** Use the product list below; "Other / not sure" is fine if uncertain but slows triage.

## Authentication

`gh` uses the user's existing GitHub auth. Agents running on a developer's machine will inherit it. Agents in CI need a `GITHUB_TOKEN` or PAT with `public_repo` (or the fine-grained equivalent).

For unauthenticated environments, use the REST API with a token:

```bash
curl -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  https://api.github.com/repos/ideal-postcodes/feedback/issues \
  -d '{
    "title": "[bug] idpc cleanse: foo",
    "body": "## Product\n- [x] CLI (@ideal-postcodes/cli)\n\n## Version\n…",
    "labels": ["bug", "needs-triage"]
  }'
```

## Templates

Two markdown templates live in `.github/ISSUE_TEMPLATE/`:

- `bug_report.md` — for bugs. Fields: product, version, what happened, expected, steps to reproduce, environment, logs.
- `feature_request.md` — for feature requests. Fields: product, problem, proposed solution, alternatives, context.

Both are plain markdown. `gh issue create --template <name>` opens an editor pre-filled with the template; for non-interactive use, render the body yourself and pass `--body`.

The `.yml` issue *forms* in the same directory are for the GitHub web UI only — **`gh` and the API ignore them**. Use the `.md` templates for programmatic filing.

## Required fields

These are the fields a triager needs to act on a bug. Agents should populate all of them:

| Field | Required | Notes |
|---|---|---|
| Title | yes | Prefix with `[bug]` or `[feature]`. Be specific (mention the command, endpoint, or library affected). |
| Product | yes | Use the canonical labels (see below). |
| Version | yes (bugs) | Package version, API version, or commit SHA. |
| What happened | yes (bugs) | Concrete description of observed behaviour. |
| Expected | yes (bugs) | What should have happened. |
| Steps to reproduce | yes (bugs) | Minimal repro. Redact secrets. |
| Problem | yes (features) | Underlying problem, not the solution. |
| Proposed solution | yes (features) | Specific behaviour you want. |

## Product labels

Pick exactly one in the **Product** section. Canonical strings:

- `CLI (@ideal-postcodes/cli)`
- `Ideal Postcodes API`
- `Address Finder Library`
- `Postcode Lookup Library`
- `Agent skills (@ideal-postcodes/skills)`
- `Documentation (docs.ideal-postcodes.co.uk)`
- `Other / not sure`

## What does NOT belong here

- **Account, billing, sensitive issues** → email `support@ideal-postcodes.co.uk`. Do not file public issues with credentials, invoices, or PII.
- **Ecommerce integration bugs** (`woocommerce`, `magento`, `shopify`, `bigcommerce-app`, `salesforce`) → file in their own repos under `ideal-postcodes/<integration>`.

If unsure whether something belongs, file with product = "Other / not sure" and triage will redirect.

## Verification

After filing, confirm the issue exists and is well-formed:

```bash
gh issue view <number> --repo ideal-postcodes/feedback
```

Expect: title is set, body contains the product label, `bug` or `enhancement` label is applied, `needs-triage` is applied.
