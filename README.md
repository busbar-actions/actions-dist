> [!WARNING]
> **`busbar-actions` is under heavy active development — expect breaking changes.**
> These repositories are public, but **not ready for use yet** — please don't depend on them.
> A pilot is starting soon: **[star and watch the busbar-actions organization](https://github.com/busbar-actions)** for the launch of Discussions and the pilot announcement.

# busbar-actions/actions-dist

Binary release host for the `busbar-actions` suite. Prebuilt CLI binaries are
published here as GitHub Releases and downloaded by the composite actions via
the shared **`busbar-actions/setup`** action (which every action invokes with a
`binary:` name; `binary-repo` defaults to `busbar-actions/actions-dist`).

## Binaries

One dedicated binary per action (no catch-all CLI). Each binary owns its own
logic and GitHub Actions UX (it reads `INPUT_*`, writes `GITHUB_OUTPUT` / step
summary / annotations, and exits non-zero on policy gates) via the
`github-actions-ux` crate, so the action YAML is a thin install-and-invoke
wrapper. The same binaries run as plain CLIs off GitHub.

Published binaries (built by the `busbar-extensions` release pipeline):

- `sf-org-create` — create a scratch org (backs `sf-org-create`)
- `sf-org-delete` — delete a scratch org / snapshot (backs `sf-org-delete`)
- `sf-snapshot` — create an OrgSnapshot with zero-downtime rotation (backs `sf-snapshot`)
- `sf-schema-dump` — per-SObject describe export (backs `sf-schema`)
- `sf-permissions-audit` — Cedar permissions audit + SARIF (backs `sf-permissions-audit`)
- `sf-metadata-retrieve` — metadata pull (backs `sf-metadata-retrieve`)
- `sf-dependency-graph` — static metadata dependency graph (backs `sf-dependency-graph`)
- `sf-cli` — sandboxed managed `sf` CLI runner (backs `sf-cli`)
- `gh-env-scratch-ensure` — verify a reusable scratch GitHub Environment slot
- `gh-env-scratch-save` — persist a scratch org session into a GitHub Environment

Not yet published (release-blocked / experimental): `sf-pii-scan` and
`sf-deploy` (typesynth-manifest decoupling), and `sf-anonymize-extract` (needs
its own dedicated binary instead of the retired `busbar-sf` catch-all).

## Asset naming

`<binary>-<target-triple>` per release tag. GitHub-hosted runners are
linux/amd64, so only `x86_64-unknown-linux-gnu` is built and published, e.g.
`sf-schema-dump-x86_64-unknown-linux-gnu`. The `setup` action fails fast on any
other runner OS/arch.

## Release tags

Releases are built and published by the `busbar-extensions` release pipeline
(`.github/workflows/release.yml`), triggered by `workflow_dispatch` (with a
`version`) or by pushing an `actions-v*` tag (the `actions-` prefix is stripped,
so `actions-v0.1.2` publishes release `v0.1.2`). Actions resolve `latest` by
default.
