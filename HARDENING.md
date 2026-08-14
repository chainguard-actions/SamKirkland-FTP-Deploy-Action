<!-- markdownlint-disable -->

# Hardening Report: SamKirkland--FTP-Deploy-Action/v4.3.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **SamKirkland--FTP-Deploy-Action/v4.3.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v3`, which is a mutable tag rather than a pinned 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to a different (potentially malicious) commit. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/ftp.yml:12`
- `.github/workflows/ftps.yml:12`

### missing-permissions (severity: medium)

Neither `ftp.yml` nor `ftps.yml` declares a top-level `permissions:` block, and neither of their jobs declares job-level permissions. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Add a top-level `permissions: {}` or the minimal set of scopes required by each workflow.

Locations:

- `.github/workflows/ftp.yml:1`
- `.github/workflows/ftps.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/ftp.yml and .github/workflows/ftps.yml:
1. Pinned `actions/checkout@v3` to full SHA `actions/checkout@f43a0e5ff2bd294095638e18286ca9a3d1956744 # v3` in both files.
2. Added `permissions: {}` top-level block to both files to restrict GITHUB_TOKEN to no permissions, since these workflows only perform FTP deployments and require no GitHub API access.

