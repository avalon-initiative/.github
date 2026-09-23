# .github

Org-wide defaults for every repository under `avalon-initiative`.

## What lives here

- `profile/README.md` — the org's public profile page.
- Repository labels are managed natively via org Settings → Repository →
  General → Repository labels, not by a file in this repo.
- `.github/workflows/*.yml` — reusable (`workflow_call`) workflows that other
  repos call into rather than reimplementing:
  - `claim-issue.yml` — comment `/claim` on an unassigned issue to self-assign it.
  - `claim-check.yml` — PR check: the author must be assigned every issue the PR closes.
  - `stale-claim-check.yml` — pings quiet claims and unassigns them after a grace period.
  - `pr-format-lint.yml` — PR title/commit format check.
  - `welcome.yml` — first-issue / first-PR greeting.
  - `dependabot-security-title.yml` — retitles security-driven Dependabot PRs.
  - `stale.yml` — marks inactive issues/PRs `stale` and closes them after a
    grace period, exempting `status: blocked` and `decision`.
- `examples/caller-workflows/` — copy-paste starting points for wiring the
  reusable workflows above into an individual repo's `.github/workflows/`.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`,
  `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md` — community
  health files, inherited by every repo in the org that doesn't define its own.
  Repos should normally not carry copies.

## Adding a new repo

1. Copy the files from `examples/caller-workflows/` into the new repo's
   `.github/workflows/`.
2. Add the per-repo files GitHub does not inherit: `LICENSE` (Apache-2.0),
   `.github/CODEOWNERS`, `.github/dependabot.yml`.
3. Override an inherited community file only when the repo genuinely needs its
   own version.

Reusable workflows are pinned to `@main`, so a change here applies to every
repo that calls them.

## Branch ruleset

`rulesets/default-protections.json` is the standard default-branch ruleset.
Rulesets need a public repo (or a paid plan), so apply it once a repo qualifies:

```bash
gh api -X POST repos/avalon-initiative/<repo>/rulesets --input rulesets/default-protections.json
```

Turn Actions on first: the required checks come from the caller workflows,
and their reported names are `call / title-lint` and `call / claim`.
