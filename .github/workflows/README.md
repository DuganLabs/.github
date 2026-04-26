# DuganLabs reusable workflows + automation

Two kinds of workflows live here:

## Reusable workflows (called from project repos)

Per-project `deploy.yml` files are thin callers like:

```yaml
jobs:
  deploy:
    uses: DuganLabs/.github/.github/workflows/cf-deploy.yml@v1
    with:
      project-name: t4bs
    secrets:
      DOPPLER_TOKEN: ${{ secrets.DOPPLER_TOKEN }}
```

| Workflow | Purpose |
|---|---|
| `ci.yml` | lint + typecheck + test |
| `cf-deploy.yml` | Cloudflare Pages deploy via Doppler |
| `d1-migrate.yml` | idempotent D1 schema apply |

**Boundary rule:** these workflows never embed any project-specific value. Cloudflare credentials are passed at call time via Doppler service tokens.

## Org-wide automation (run in this repo)

Workflows that run on **this** `.github` repo to keep the org's GitHub state honest. They're triggered by issue/PR events on member repos via the `org` event scope when permissions allow, or are invoked by per-project workflows that delegate to them.

| Workflow | Trigger | Purpose |
|---|---|---|
| `labeler.yml` | PR opened/sync | Auto-applies path-based labels (frontend, backend, infra, db, docs, deps, basenative) |
| `auto-close-milestone.yml` | Issue/PR closed | Closes a milestone when its last open issue lands |
| `stale-state-sweep.yml` | Weekly cron | Marks/closes stale issues + PRs |

## Versioning

Tag this repo `v1`, `v2`, etc. Per-project callers pin to a major version (`@v1`) so patches propagate. Breaking changes require a major bump.
