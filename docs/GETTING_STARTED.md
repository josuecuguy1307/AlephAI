# Getting Started

This document describes how to approach Aleph as a product user and as a developer validating a build.

## 1. Launch model

Aleph is a desktop application. The current release target is macOS.

A normal launch should bring up the shared Aleph shell and allow entry into the available workspaces. Depending on the build and account state, the product may operate with a local device session, an authenticated account, or both.

Do not assume every external connector or model shown by the interface is ready to use. Some integrations require a local CLI, a user authorization flow, or a user-provided credential.

## 2. Main surfaces

### Home

Home is the system-level entry point. It provides navigation to workspaces and product-level capabilities.

### The Workshop

The Workshop is the composition surface for arranging agents, tools, and pieces into reusable working systems.

### Workspaces

The six primary workspace surfaces are:

- Science
- Education
- Office
- Finance
- Legal
- Design

Each workspace uses the shared Aleph shell but owns its domain-specific artifacts, tools, and views.

## 3. Models and coding agents

A build may expose multiple model/provider paths. Availability depends on runtime configuration and credentials.

CLI-backed integrations can depend on software installed on the machine. A visible CLI option does not imply that the underlying CLI is installed or authenticated.

## 4. Connectors

Connectors must be explicitly authorized or configured. A connector may provide capabilities such as mail, files, calendars, source control, or other external services.

Treat connected accounts as user-controlled data boundaries. Never ship a release bundle containing developer credentials, authenticated browser state, or personal connector tokens.

## 5. Files and artifacts

Artifacts can include documents, spreadsheets, charts, generated files, code outputs, scientific files, and workspace-specific structured results.

A release should begin from a clean user state. The shipped application must not contain the developer's local sessions, documents, conversations, browser state, local paths, or private databases.

## 6. Build validation mode

When validating a release candidate, use a temporary/clean HOME where possible and confirm at minimum:

- onboarding launches;
- The Workshop opens;
- all six workspaces open;
- the packaged sidecars start;
- the application has no personal sessions or credentials;
- release-specific security gates pass;
- the final bundle verifies with the platform signing tools.

See `RELEASE.md` for the full release checklist.
