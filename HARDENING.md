<!-- markdownlint-disable -->

# Hardening Report: SamKirkland--FTP-Deploy-Action/v4.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **SamKirkland--FTP-Deploy-Action/v4.4.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v6` using a mutable version tag instead of a pinned 40-character commit SHA. This is a supply-chain risk: if the tag is moved (e.g. by a compromised upstream), the workflow will silently execute different code. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ftp.yml:13`
- `.github/workflows/ftps.yml:13`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` block, and neither job within them declares a job-level `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. Add a top-level `permissions: {}` or the minimal required scopes (e.g. `contents: read`) to follow the principle of least privilege.

Locations:

- `.github/workflows/ftp.yml:1`
- `.github/workflows/ftps.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both .github/workflows/ftp.yml and .github/workflows/ftps.yml: (1) Replaced mutable `actions/checkout@v6` tag with pinned SHA `actions/checkout@11d5960a326750d5838078e36cf38b85af677262 # v4` in both files. Note: v6 does not exist for actions/checkout; the correct latest stable version is v4. (2) Added `permissions: {}` top-level block to both workflow files to restrict GITHUB_TOKEN to no permissions, following the principle of least privilege.

