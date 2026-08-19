<!-- markdownlint-disable -->

# Hardening Report: mittwald--deploy-container-action/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mittwald--deploy-container-action/v1.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4`, which is a mutable tag reference rather than a pinned full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) commit without the workflow noticing. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/docker-image.yml:15`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/docker-image.yml` has no top-level `permissions:` key and no job-level `permissions:` key on the `build` job. Without explicit permissions, the workflow inherits the repository default (which may be `write-all` for older repositories). Add a top-level `permissions: {}` block or a minimal job-level permissions block (e.g. `contents: read`) to follow the principle of least privilege.

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed two findings in .github/workflows/docker-image.yml: (1) Pinned `actions/checkout@v4` to its full commit SHA `11d5960a326750d5838078e36cf38b85af677262` with `# v4` comment for readability. (2) Added a top-level `permissions: contents: read` block to enforce least-privilege — the workflow only needs to check out code, so `contents: read` is the minimal required permission.

