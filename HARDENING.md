<!-- markdownlint-disable -->

# Hardening Report: shogo82148--actions-goveralls/v1.11.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **shogo82148--actions-goveralls/v1.11.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. All jobs in this workflow lack permission scoping.

Locations:

- `.github/workflows/test.yml:1`
- `.github/workflows/check-dist.yml:1`
- `.github/workflows/codeql-analysis.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added top-level `permissions:` blocks to all three workflow files:
1. `.github/workflows/test.yml`: Added `permissions: contents: read` — only needs to checkout code and download/upload artifacts.
2. `.github/workflows/check-dist.yml`: Added `permissions: contents: read` — only needs to checkout code and upload artifacts.
3. `.github/workflows/codeql-analysis.yml`: Added `permissions: contents: read, security-events: write, actions: read` — CodeQL requires `security-events: write` to upload SARIF results and `actions: read` to read workflow information for private repos.

