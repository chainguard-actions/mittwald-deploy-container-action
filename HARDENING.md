<!-- markdownlint-disable -->

# Hardening Report: mittwald--deploy-container-action/v1.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mittwald--deploy-container-action/v1.0.5** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yaml uses a mutable Docker image tag instead of a SHA digest: `image: docker://ghcr.io/mittwald/deploy-container-action:v1`. This tag can be silently updated to point to a different (potentially malicious) image. It should be pinned to a specific SHA256 digest, e.g. `docker://ghcr.io/mittwald/deploy-container-action@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:11`

### unpinned-uses (severity: high)

One or more `uses:` references in .github/workflows/docker-image.yml are pinned to a mutable version tag rather than a full 40-character commit SHA: `actions/checkout@v4`. These should be pinned to their full commit SHAs to prevent supply-chain attacks.

Locations:

- `.github/workflows/docker-image.yml:16`

### unpinned-uses (severity: high)

Multiple `uses:` references in .github/workflows/release.yml are pinned to mutable version tags rather than full 40-character commit SHAs: `actions/checkout@v4`, `docker/login-action@v3`, `docker/metadata-action@v5`, `docker/build-push-action@v6`. These should be pinned to their full commit SHAs to prevent supply-chain attacks.

Locations:

- `.github/workflows/release.yml:12`
- `.github/workflows/release.yml:15`
- `.github/workflows/release.yml:22`
- `.github/workflows/release.yml:30`

### missing-permissions (severity: medium)

.github/workflows/docker-image.yml has no top-level `permissions:` key and its only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository default (typically `contents: write` for older repositories), granting broader access than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four findings: (1) Pinned docker image in action.yaml to SHA256 digest while preserving the docker:// scheme and :v1 tag inline. (2) Pinned actions/checkout@v4 in docker-image.yml to full commit SHA and added top-level `permissions: contents: read` block. (3) Pinned all four action references in release.yml (actions/checkout@v4, docker/login-action@v3, docker/metadata-action@v5, docker/build-push-action@v6) to their full commit SHAs with version tag comments preserved.

