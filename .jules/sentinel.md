## 2024-09-16 - [Proactive Security Foundation]
**Vulnerability:** Missing `.gitignore` and `SECURITY.md` in a fresh repository.
**Learning:** Repositories without a basic `.gitignore` are at high risk of accidentally committing secrets (like `.env` files or SSH keys) early in development. A missing `SECURITY.md` means there's no clear, private path for reporting future vulnerabilities, increasing the risk of public disclosure.
**Prevention:** Always initialize repositories with a robust `.gitignore` covering common secrets and environment variables, and establish a `SECURITY.md` policy from day one.
## 2024-05-24 - [Automated Secret Scanning]
**Vulnerability:** Lack of automated scanning for secrets and credentials in the codebase.
**Learning:** Even with a `.gitignore` in place, secrets can still accidentally be committed (e.g. testing files, misconfigured environments). Relying purely on developer diligence is error-prone.
**Prevention:** Implemented a Gitleaks GitHub Action workflow (`.github/workflows/secret-scanning.yml`) to automatically scan all pushes and pull requests for potential secrets, providing a critical layer of defense-in-depth.

## 2025-01-20 - [GitHub Actions Least Privilege]
**Vulnerability:** GitHub Action workflow lacked explicit `permissions` block and used deprecated `actions/checkout@v3` (Node 16).
**Learning:** Relying on default `GITHUB_TOKEN` permissions can grant overly broad access (e.g. write access). Using deprecated Node versions in Actions introduces known vulnerabilities.
**Prevention:** Always define explicit top-level `permissions` blocks (e.g., `contents: read`) in GitHub Action workflows to adhere to least-privilege principles, and regularly audit/upgrade Action dependencies to mitigate risks from outdated runtime environments.
## 2025-02-12 - [GitHub Actions Node Deprecation]
**Vulnerability:** GitHub Action `gitleaks-action@v2` targeting deprecated Node.js 20 environment.
**Learning:** Using outdated major versions of GitHub Actions can lead to CI failures when the underlying runtime (like Node.js) is deprecated by GitHub, potentially disrupting security scanning workflows.
**Prevention:** Regularly update GitHub Actions to their latest major versions (e.g., `gitleaks-action@v3`) to ensure compatibility with supported runner environments and avoid deprecation warnings or failures.
## 2025-02-12 - [GitHub Actions Mutable Tags]
**Vulnerability:** GitHub Action workflows using mutable version tags (e.g., `@v4`, `@v3`).
**Learning:** Referencing GitHub Actions by tags (e.g., `@v4`) is susceptible to supply chain attacks. If a malicious actor compromises the action's repository, they can move the tag to a malicious commit, which will automatically be executed in our CI pipeline.
**Prevention:** Always pin GitHub Actions to their full-length commit SHAs and include a comment with the corresponding version tag (e.g., `actions/checkout@11d5960... # v4`) to ensure immutability and protect against unauthorized modifications.
