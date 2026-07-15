---
name: gitleaks
description: "When the user wants to scan a repository for leaked secrets, hardcoded credentials, API keys, tokens, passwords, or private keys — or says 'gitleaks,' 'secret scan,' 'check for secrets,' 'did I commit a key,' 'leaked credentials,' 'scan git history,' or asks how to set up secret scanning in pre-commit hooks or CI. Also use when a secret has already leaked and the user needs to remediate: rotate the credential and purge it from git history."
metadata:
  version: 1.0.0
---

# Gitleaks Secret Scanning

You help users find and remediate leaked secrets using [Gitleaks](https://github.com/gitleaks/gitleaks), an open-source SAST tool that detects hardcoded secrets (API keys, tokens, passwords, private keys) in files and git history using a large set of built-in rules.

## Check availability first

```bash
gitleaks version
```

If it's not installed, offer the right install path for the platform:

| Platform | Command |
|----------|---------|
| macOS (Homebrew) | `brew install gitleaks` |
| Docker | `docker run -v "$(pwd):/path" ghcr.io/gitleaks/gitleaks:latest git /path` |
| Go | `go install github.com/gitleaks/gitleaks/v8@latest` |
| Binary release | Download from https://github.com/gitleaks/gitleaks/releases |

## Core scan modes

Gitleaks v8.19+ has two primary subcommands:

```bash
# Scan full git history (every commit) — use for "has a secret ever been committed?"
gitleaks git .

# Scan current files only (no git history) — use for "are there secrets in the code right now?"
gitleaks dir .

# Scan only unstaged/staged changes before committing
gitleaks git --pre-commit --staged
```

Useful flags:

- `--report-format json --report-path gitleaks-report.json` — machine-readable output you can parse and summarize for the user
- `--redact` — mask secret values in output (recommended when showing results in a shared context)
- `--verbose` — show findings as they're discovered
- `--log-opts="main..feature-branch"` — restrict a `git` scan to a commit range
- `--baseline-path baseline.json` — ignore previously triaged findings
- `--exit-code` — customize the exit code on leaks (default: 1 when leaks found, 0 clean, 126 on error)

## Running a scan for the user

1. Prefer `gitleaks git` for repositories (it covers history, where deleted-but-committed secrets hide); use `gitleaks dir` for non-git directories or when the user only cares about current files.
2. Always use `--redact` unless the user explicitly asks to see the secret values.
3. Write a JSON report, then summarize: rule ID, file, line, commit (if history scan), and author. Group duplicate secrets that appear in many commits.
4. Distinguish **real secrets** from **false positives** (test fixtures, example keys, high-entropy non-secrets). Recommend allowlisting false positives rather than ignoring the tool.

## Configuration (`.gitleaks.toml`)

Place a `.gitleaks.toml` at the repo root, or pass `--config path`. To extend the default rules rather than replace them:

```toml
[extend]
useDefault = true

# Custom rule example
[[rules]]
id = "internal-api-token"
description = "Internal service token"
regex = '''svc_[a-zA-Z0-9]{32}'''
tags = ["internal", "token"]

# Allowlist false positives
[[allowlists]]
description = "Test fixtures"
paths = ['''tests/fixtures/.*''']

[[allowlists]]
description = "Known example values"
regexes = ['''EXAMPLE_KEY_[A-Z0-9]+''']
```

Inline suppression: append `# gitleaks:allow` to a line to skip it (use sparingly, and only for confirmed false positives).

## Baselines for existing repos

For legacy repos with known findings, create a baseline so only *new* leaks fail:

```bash
gitleaks git --report-path baseline.json .
gitleaks git --baseline-path baseline.json --report-path new-findings.json .
```

## Prevention: pre-commit and CI

**Pre-commit hook** (via [pre-commit](https://pre-commit.com), `.pre-commit-config.yaml`):

```yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.24.0
    hooks:
      - id: gitleaks
```

**GitHub Actions** (`.github/workflows/gitleaks.yml`):

```yaml
name: gitleaks
on: [pull_request, push]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Note: `fetch-depth: 0` matters — a shallow checkout limits history scanning.

## Remediation when a real secret is found

Walk the user through this order — rotation first, history rewriting second:

1. **Rotate immediately.** Treat the secret as compromised the moment it was committed (even in a private repo). Revoke it at the provider and issue a new one.
2. **Remove from current code.** Move it to an environment variable or secret manager; add the env/config file to `.gitignore`.
3. **Purge from history only if needed.** If the repo is public or shared, rewrite history with `git filter-repo` or [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/), then force-push and have collaborators re-clone. Warn the user this rewrites shared history and that forks/clones/caches may still hold the old commits — which is why rotation is the step that actually matters.
4. **Re-scan** to confirm the leak is gone, and add prevention (pre-commit hook or CI) so it doesn't recur.
