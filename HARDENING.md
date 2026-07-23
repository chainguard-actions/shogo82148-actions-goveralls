<!-- markdownlint-disable -->

# Hardening Report: shogo82148--actions-goveralls/v1.9.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **shogo82148--actions-goveralls/v1.9.1** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in test.yml use mutable tag refs instead of pinned full-length SHA commit hashes, making the workflow vulnerable to supply-chain attacks if the referenced action tags are moved or compromised. Unpinned refs: actions/checkout@v4, actions/setup-node@v4, actions/setup-go@v5, actions/upload-artifact@v4, actions/download-artifact@v4.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:18`
- `.github/workflows/test.yml:22`
- `.github/workflows/test.yml:34`
- `.github/workflows/test.yml:51`
- `.github/workflows/test.yml:54`
- `.github/workflows/test.yml:55`
- `.github/workflows/test.yml:72`
- `.github/workflows/test.yml:74`

### unpinned-uses (severity: high)

All `uses:` references in codeql-analysis.yml use mutable tag refs instead of pinned full-length SHA commit hashes, making the workflow vulnerable to supply-chain attacks. Unpinned refs: actions/checkout@v4, github/codeql-action/init@v3, github/codeql-action/autobuild@v3, github/codeql-action/analyze@v3.

Locations:

- `.github/workflows/codeql-analysis.yml:31`
- `.github/workflows/codeql-analysis.yml:35`
- `.github/workflows/codeql-analysis.yml:42`
- `.github/workflows/codeql-analysis.yml:52`

### missing-permissions (severity: medium)

The workflow file test.yml has no top-level `permissions:` key and no job-level `permissions:` keys on any of its jobs (build, test, finish). Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

### missing-permissions (severity: medium)

The workflow file codeql-analysis.yml has no top-level `permissions:` key and no job-level `permissions:` key on its `analyze` job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/codeql-analysis.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in both workflow files:

**test.yml:**
- Added top-level `permissions: {}` to deny all permissions by default
- Added `permissions: { contents: read }` to all three jobs (build, test, finish)
- Pinned all action references to full SHA commits:
  - actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262
  - actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020
  - actions/setup-go@v5 → @40f1582b2485089dde7abd97c1529aa768e1baff
  - actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02
  - actions/download-artifact@v4 → @d3f86a106a0bac45b974a628896c90dbdf5c8093

**codeql-analysis.yml:**
- Added top-level `permissions: {}` to deny all permissions by default
- Added job-level `permissions: { actions: read, contents: read, security-events: write }` to the analyze job (security-events: write is required for CodeQL to upload SARIF results)
- Pinned all action references to full SHA commits:
  - actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262
  - github/codeql-action/init@v3 → @4187e74d05793876e9989daffde9c3e66b4acd07
  - github/codeql-action/autobuild@v3 → @4187e74d05793876e9989daffde9c3e66b4acd07
  - github/codeql-action/analyze@v3 → @4187e74d05793876e9989daffde9c3e66b4acd07

