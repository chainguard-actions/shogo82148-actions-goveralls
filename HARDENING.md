<!-- markdownlint-disable -->

# Hardening Report: shogo82148--actions-goveralls/v1.9.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **shogo82148--actions-goveralls/v1.9.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in test.yml use mutable version tags instead of pinned 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if the referenced action tags are moved. Unpinned references: `actions/checkout@v4` (lines 14, 66, 80), `actions/setup-node@v4` (line 18), `actions/setup-go@v5` (lines 22, 62), `actions/upload-artifact@v4` (line 36), `actions/download-artifact@v4` (lines 67, 81).

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:18`
- `.github/workflows/test.yml:22`
- `.github/workflows/test.yml:36`
- `.github/workflows/test.yml:62`
- `.github/workflows/test.yml:66`
- `.github/workflows/test.yml:67`
- `.github/workflows/test.yml:80`
- `.github/workflows/test.yml:81`

### unpinned-uses (severity: high)

All `uses:` references in codeql-analysis.yml use mutable version tags instead of pinned 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks. Unpinned references: `actions/checkout@v4` (line 36), `github/codeql-action/init@v3` (line 40), `github/codeql-action/autobuild@v3` (line 51), `github/codeql-action/analyze@v3` (line 62).

Locations:

- `.github/workflows/codeql-analysis.yml:36`
- `.github/workflows/codeql-analysis.yml:40`
- `.github/workflows/codeql-analysis.yml:51`
- `.github/workflows/codeql-analysis.yml:62`

### missing-permissions (severity: medium)

The workflow file test.yml has no top-level `permissions:` key and none of its jobs (build, test, finish) define job-level `permissions:` blocks. This means the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/test.yml:1`

### missing-permissions (severity: medium)

The workflow file codeql-analysis.yml has no top-level `permissions:` key and its only job (analyze) has no job-level `permissions:` block. This means the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/codeql-analysis.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 findings across 2 workflow files:

**test.yml:**
- Added `permissions: {}` top-level block (no GITHUB_TOKEN permissions needed)
- Pinned actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5 (3 occurrences)
- Pinned actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020
- Pinned actions/setup-go@v5 → @40f1582b2485089dde7abd97c1529aa768e1baff (2 occurrences)
- Pinned actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02
- Pinned actions/download-artifact@v4 → @d3f86a106a0bac45b974a628896c90dbdf5c8093 (2 occurrences)

**codeql-analysis.yml:**
- Added `permissions: { contents: read, security-events: write }` top-level block (minimum needed for CodeQL)
- Pinned actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5
- Pinned github/codeql-action/init@v3 → @b7351df727350dca84cb9d725d57dcf5bc82ba26
- Pinned github/codeql-action/autobuild@v3 → @b7351df727350dca84cb9d725d57dcf5bc82ba26
- Pinned github/codeql-action/analyze@v3 → @b7351df727350dca84cb9d725d57dcf5bc82ba26

All original tag names preserved as inline comments for readability.

