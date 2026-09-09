<!-- markdownlint-disable -->

# Hardening Report: mittwald--deploy-container-action/v1.0.7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mittwald--deploy-container-action/v1.0.7** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple action references and the Docker image in action.yaml are pinned to mutable version tags rather than immutable full-length commit SHAs or digest references. This exposes the workflow to supply-chain attacks if the tag is moved.

Failing references:
- action.yaml: `image: 'docker://ghcr.io/mittwald/deploy-container-action:v1'` (tag, not a SHA digest)
- .github/workflows/automerge.yml: `uses: dependabot/fetch-metadata@v2`
- .github/workflows/docker-image.yml: `uses: actions/checkout@v4`
- .github/workflows/release.yml: `uses: actions/checkout@v4`, `uses: docker/login-action@v3`, `uses: docker/metadata-action@v5`, `uses: docker/build-push-action@v6`

Locations:

- `action.yaml:11`
- `.github/workflows/automerge.yml:13`
- `.github/workflows/docker-image.yml:16`
- `.github/workflows/release.yml:13`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/docker-image.yml` has no top-level `permissions:` key and its only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents by default on many repositories).

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action/image references by resolving them to immutable SHAs: (1) action.yaml: pinned ghcr.io/mittwald/deploy-container-action:v1 to its sha256 digest while preserving the docker:// scheme and tag inline; (2) automerge.yml: pinned dependabot/fetch-metadata@v2 to full commit SHA; (3) docker-image.yml: pinned actions/checkout@v4 to full commit SHA and added top-level `permissions: contents: read` block; (4) release.yml: pinned actions/checkout@v4, docker/login-action@v3, docker/metadata-action@v5, and docker/build-push-action@v6 to their respective full commit SHAs.

