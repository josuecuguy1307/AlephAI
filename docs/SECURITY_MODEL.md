# Security Model

This document describes the technical security boundaries that Aleph engineering should preserve. It is not a guarantee that any specific build is vulnerability-free.

## Primary trust boundaries

### 1. UI/web content -> native application

Webview content must not automatically gain native authority. Native commands should be scoped, authenticated/capability-checked where appropriate, and narrow in purpose.

### 2. UI -> local sidecar

Loopback does not equal trusted. Local services need explicit authentication, origin/host checks, session/capability handling, and safe lifecycle behavior.

### 3. User URL -> outbound network

Custom provider/connector URLs require SSRF defenses, redirect revalidation, DNS/IP classification, and safe credential forwarding.

### 4. User path -> filesystem

Privileged file operations must resist traversal, symlink escape, and race replacement.

### 5. User code -> host machine

Python/shell execution should occur in an isolated guest boundary. The release must fail closed if the isolation runtime is unavailable; host execution must not silently become the fallback.

### 6. OAuth callback -> authenticated capability

State, nonce, PKCE, callback origin/port, token claim, listener lifecycle, and log redaction must be handled explicitly.

### 7. Artifact content -> renderer

Generated HTML or other active content must not obtain privileged same-origin/native capabilities through the artifact viewer.

## Release validation gates

A final macOS bundle should be checked for:

- deep/strict code-sign verification;
- clean-user launch from a temporary HOME;
- onboarding and all six workspaces;
- The Workshop;
- personal path/hostname leakage;
- secret candidates and unclassified credentials;
- OAuth boundary behavior;
- isolated Python/shell guest execution;
- browser proxy/URL policy;
- filesystem/symlink regressions;
- artifact rendering boundaries;
- packaged productivity tooling such as OfficeCLI when present.

## Reporting

Do not publish exploit details for an unresolved issue in a public issue. Use the process in the root `SECURITY.md`.
