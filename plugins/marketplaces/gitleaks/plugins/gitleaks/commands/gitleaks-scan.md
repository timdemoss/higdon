---
description: Scan this repository for leaked secrets with Gitleaks and summarize the findings
argument-hint: "[history|dir|staged] (default: history)"
allowed-tools: Bash(gitleaks *), Read, Grep, Glob
---

Run a Gitleaks secret scan of the current repository and report the results.

Mode requested: `$ARGUMENTS` (if empty, default to a full git-history scan).

Steps:

1. Verify gitleaks is installed with `gitleaks version`. If missing, tell the user how to install it (`brew install gitleaks`, Go install, Docker, or a release binary from https://github.com/gitleaks/gitleaks/releases) and stop.
2. Pick the scan command from the requested mode:
   - `history` (default): `gitleaks git --redact --report-format json --report-path /tmp/gitleaks-report.json .`
   - `dir`: `gitleaks dir --redact --report-format json --report-path /tmp/gitleaks-report.json .`
   - `staged`: `gitleaks git --pre-commit --staged --redact --report-format json --report-path /tmp/gitleaks-report.json`
   If a `.gitleaks.toml` exists at the repo root, gitleaks picks it up automatically — mention that it was used.
3. Exit code 0 means clean; 1 means leaks were found; anything else is an error to report verbatim.
4. If leaks were found, read the JSON report and present a summary table: rule ID, file, line, commit (short SHA, history scans only), and redacted match. Group repeats of the same secret across commits into one row with a commit count.
5. Triage each finding as likely-real or likely-false-positive (test fixture, example value, placeholder). For false positives, suggest a `.gitleaks.toml` allowlist entry or `# gitleaks:allow` inline comment.
6. For likely-real secrets, remind the user of remediation order: rotate the credential first, remove it from code in favor of env vars or a secret manager, and only then consider history rewriting (`git filter-repo` / BFG) — noting that rotation is what actually neutralizes the leak.

Never print unredacted secret values in your response.
