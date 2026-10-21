# beats-fragment-injection-base

Security research lab. **Not production, not affiliated with Elastic.**

Reproduces one composition reported to Elastic: `.github/workflows/fragment-in-pr.yml` in
`elastic/beats` reads a version string out of a pull-request-controlled Go source file and splices it
into a later step's shell script through a step output.

- `.github/workflows/fragment-in-pr.yml` lines 1-29 are copied byte for byte from
  `elastic/beats@main`, blob `2d2acc4ec0fd6ea913af5a37ccb48763e1c4221e`. The only addition is the
  final step, labelled `LAB ONLY`, which reports whether a marker file exists.
- `libbeat/version/version.go` is copied byte for byte from `elastic/beats@main`.
- `config.changelog.yaml` is lab-only: it points the upstream changelog tool's default `--owner` at
  this account instead of `elastic`, because the vendored step passes only `--repo`.
