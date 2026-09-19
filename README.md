# .github

Org-wide defaults for every repository under `avalon-initiative`.

## What lives here

- `profile/README.md` — the org's public profile page.
- Repository labels are managed natively via org Settings → Repository →
  General → Repository labels, not by a file in this repo.
- `.github/workflows/*.yml` — reusable (`workflow_call`) workflows that other
  repos call into rather than reimplementing:
  - `claim-check.yml` — lets a contributor comment `/claim` on an unassigned
    issue to self-assign it; labels it `claimed`; tells them if it's already
    taken.
  - `stale.yml` — marks inactive issues/PRs `stale` and closes them after a
    grace period, exempting `status: blocked` and `decision`.
- `examples/caller-workflows/` — copy-paste starting points for wiring the
  reusable workflows above into an individual repo's `.github/workflows/`.
- `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md` — fallback
  community health files, used by any repo in the org that doesn't define its
  own.

## Adding a new repo

1. Copy the relevant files from `examples/caller-workflows/` into the new
   repo's `.github/workflows/`.
2. Give it its own issue templates / PR template / CONTRIBUTING.md once its
   conventions are established — these org defaults are a fallback, not meant
   to be permanent for an active repo.
