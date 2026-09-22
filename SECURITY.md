# Security

## Reporting a vulnerability

Please do not open a public issue containing exploit details, private credentials, tokens, user data, or instructions that materially increase exploitability of an unresolved vulnerability.

For this repository, use GitHub's private vulnerability-reporting / Security Advisory flow when enabled. If private reporting is unavailable, contact the repository maintainers through a private channel before disclosing technical details publicly.

A useful report includes:

- affected release/build;
- affected component or workspace;
- reproduction prerequisites;
- expected vs. actual security boundary;
- impact;
- logs or traces with secrets removed;
- whether the issue is reproducible on a clean user profile.

## Scope

Security-sensitive areas include OAuth, connectors, browser/network boundaries, local sidecars, filesystem access, artifact renderers, native/Tauri commands, local process spawning, packaged third-party services, and isolated code execution.

## Release validation

Aleph release candidates are expected to undergo bundle-level validation in addition to source-level tests. See `docs/SECURITY_MODEL.md` and `docs/RELEASE.md`.
