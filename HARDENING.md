<!-- markdownlint-disable -->

# Hardening Report: shogo82148--actions-goveralls/v1.11.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **shogo82148--actions-goveralls/v1.11.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. All jobs in this workflow lack permissions scoping.

Locations:

- `.github/workflows/check-dist.yml:22`
- `.github/workflows/codeql-analysis.yml:23`
- `.github/workflows/test.yml:9`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added top-level `permissions:` blocks to all three workflow files:
- `.github/workflows/check-dist.yml`: `contents: read` (checkout and build only)
- `.github/workflows/codeql-analysis.yml`: `contents: read`, `security-events: write` (required for CodeQL SARIF upload), `actions: read` (required for CodeQL on private repos)
- `.github/workflows/test.yml`: `contents: read` (checkout, build, and artifact operations)

