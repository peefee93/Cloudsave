## 2024-09-16 - [Proactive Security Foundation]
**Vulnerability:** Missing `.gitignore` and `SECURITY.md` in a fresh repository.
**Learning:** Repositories without a basic `.gitignore` are at high risk of accidentally committing secrets (like `.env` files or SSH keys) early in development. A missing `SECURITY.md` means there's no clear, private path for reporting future vulnerabilities, increasing the risk of public disclosure.
**Prevention:** Always initialize repositories with a robust `.gitignore` covering common secrets and environment variables, and establish a `SECURITY.md` policy from day one.
## 2024-05-24 - [Automated Secret Scanning]
**Vulnerability:** Lack of automated scanning for secrets and credentials in the codebase.
**Learning:** Even with a `.gitignore` in place, secrets can still accidentally be committed (e.g. testing files, misconfigured environments). Relying purely on developer diligence is error-prone.
**Prevention:** Implemented a Gitleaks GitHub Action workflow (`.github/workflows/secret-scanning.yml`) to automatically scan all pushes and pull requests for potential secrets, providing a critical layer of defense-in-depth.
