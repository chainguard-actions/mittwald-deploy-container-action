<!-- markdownlint-disable -->

# Hardening Report: mittwald--deploy-container-action/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mittwald--deploy-container-action/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v4`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) commit without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/docker-image.yml:13`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single `build` job also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g., write access to contents). A minimal `permissions:` block should be added.

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/docker-image.yml: (1) Pinned `actions/checkout@v4` to its full commit SHA `11d5960a326750d5838078e36cf38b85af677262` with a `# v4` comment for readability. (2) Added a top-level `permissions: contents: read` block — the minimum permission required for the checkout step. No other permissions are needed by this workflow.

