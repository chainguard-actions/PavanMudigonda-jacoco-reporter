<!-- markdownlint-disable -->

# Hardening Report: PavanMudigonda--jacoco-reporter/v5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **PavanMudigonda--jacoco-reporter/v5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags (@v1, @v2, @v3) instead of pinned full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit.

codeql-analysis.yml:
  - uses: actions/checkout@v2
  - uses: github/codeql-action/init@v1
  - uses: github/codeql-action/autobuild@v1
  - uses: github/codeql-action/analyze@v1

codeql.yml:
  - uses: actions/checkout@v3
  - uses: github/codeql-action/init@v2
  - uses: github/codeql-action/autobuild@v2
  - uses: github/codeql-action/analyze@v2

Locations:

- `.github/workflows/codeql-analysis.yml:35`
- `.github/workflows/codeql-analysis.yml:40`
- `.github/workflows/codeql-analysis.yml:49`
- `.github/workflows/codeql-analysis.yml:57`
- `.github/workflows/codeql.yml:36`
- `.github/workflows/codeql.yml:41`
- `.github/workflows/codeql.yml:55`
- `.github/workflows/codeql.yml:63`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 8 unpinned action references across two workflow files:

**codeql-analysis.yml** (v1 tags → SHA 231aa2c8a89117b126725a0e11897209b7118144):
- actions/checkout@v2 → @ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2
- github/codeql-action/init@v1 → @231aa2c8a89117b126725a0e11897209b7118144 # v1
- github/codeql-action/autobuild@v1 → @231aa2c8a89117b126725a0e11897209b7118144 # v1
- github/codeql-action/analyze@v1 → @231aa2c8a89117b126725a0e11897209b7118144 # v1

**codeql.yml** (v2/v3 tags → respective SHAs):
- actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744 # v3
- github/codeql-action/init@v2 → @b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2
- github/codeql-action/autobuild@v2 → @b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2
- github/codeql-action/analyze@v2 → @b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2

Note: codeql-analysis.yml was fully rewritten because initial targeted edits corrupted the file (the autobuild and analyze step content got merged into comment text). Both files are now clean and valid.

