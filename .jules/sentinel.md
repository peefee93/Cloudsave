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
## 2024-05-30 - [GitHub Actions Supply Chain Protection]
**Vulnerability:** GitHub Action workflows using mutable tags (e.g., `@v4`, `@v2`) instead of immutable commit SHAs.
**Learning:** Tags in Git are mutable and can be moved. An attacker who compromises a GitHub Action's repository could move a widely used tag (like `v2`) to point to a malicious commit. If workflows reference this tag, they will automatically pull and run the malicious code, leading to a supply-chain attack.
**Prevention:** Always pin GitHub Actions to their specific, immutable commit SHAs (e.g., `@11d5960a326750d5838078e36cf38b85af677262`) and add comments referencing the original tag for maintainability. Use tools like Dependabot to keep these SHAs updated securely.
