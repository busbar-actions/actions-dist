# busbar-actions/actions-dist

Binary release host for the `busbar-actions` suite. Prebuilt CLI binaries are
published here as GitHub Releases and downloaded by the composite actions
(`sf-schema`, `sf-pii-scan`, `sf-dependency-graph`, `sf-metadata-pull`,
`sf-permissions-audit`, `sf-anonymize-extract`, `sf-metadata-deploy`) via their
`binary-repo` input (defaults to `busbar-actions/actions-dist`).

## Binaries

- **`busbar-sf`** — backs the six `sf-*` actions (schema, pii-scan, dep-graph,
  metadata pull, security audit, data pipeline).
- **`sf-deploy`** — backs `sf-metadata-deploy`.

## Asset naming

`<binary>-<target-triple>` for each release tag, e.g. `busbar-sf-aarch64-apple-darwin`,
`busbar-sf-x86_64-unknown-linux-gnu`, `sf-deploy-x86_64-pc-windows-msvc.exe`.

Releases are built and published by the `busbar-extensions` release pipeline.
