<!-- markdownlint-disable -->

# Hardening Report: mittwald--deploy-container-action/v1.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **mittwald--deploy-container-action/v1.0.5** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image reference with a mutable tag ('v1') instead of a SHA digest. The reference 'docker://ghcr.io/mittwald/deploy-container-action:v1' can be silently updated to point to a different (potentially malicious) image. It should be pinned to a specific SHA digest, e.g. 'docker://ghcr.io/mittwald/deploy-container-action@sha256:<64-hex-char-digest>'.

Locations:

- `action.yaml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yaml from 'docker://ghcr.io/mittwald/deploy-container-action:v1' to 'docker://ghcr.io/mittwald/deploy-container-action@sha256:96aec5760ab3d79ed4af3fe2647fe3f1ae82d0aa5abbeb976cdf1b56f9e65a17' # v1. The comment is placed outside the YAML string quotes to preserve readability while ensuring the image reference is immutable.

