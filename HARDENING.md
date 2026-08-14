<!-- markdownlint-disable -->

# Hardening Report: SamKirkland--FTP-Deploy-Action/v4.3.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **SamKirkland--FTP-Deploy-Action/v4.3.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v4` using a mutable version tag instead of a pinned 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to point to malicious code. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ftp.yml:12`
- `.github/workflows/ftps.yml:12`

### missing-permissions (severity: medium)

Neither `.github/workflows/ftp.yml` nor `.github/workflows/ftps.yml` declares a top-level `permissions:` key, and no job within them has a `permissions:` key either. Without explicit permissions, the GITHUB_TOKEN is granted the repository's default (potentially broad) permissions. Add a top-level `permissions: {}` block and grant only the minimum scopes required (e.g. `contents: read`).

Locations:

- `.github/workflows/ftp.yml:1`
- `.github/workflows/ftps.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both .github/workflows/ftp.yml and .github/workflows/ftps.yml: (1) Pinned `actions/checkout@v4` to the full commit SHA `11d5960a326750d5838078e36cf38b85af677262` with a `# v4` comment for readability. (2) Added a top-level `permissions: {}` block to both files to restrict the GITHUB_TOKEN to no permissions by default.

