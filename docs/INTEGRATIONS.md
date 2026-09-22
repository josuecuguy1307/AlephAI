# Models, CLI Agents, and Connectors

Aleph separates the product shell from the model/provider layer. The model is selected as part of a workflow; it is not the entire application architecture.

## Model providers

Release-specific builds can expose one or more API-backed providers. Availability depends on configuration, authentication, and supported runtime adapters.

Do not document a provider as available merely because a visual asset exists. The source/build must contain a working adapter and the release must expose it intentionally.

![Model and CLI overview](../assets/overview/models-and-cli.png)

## CLI coding agents

Aleph can integrate local coding CLIs when they are installed and authenticated on the user's machine. CLI integrations should:

- detect installation state;
- distinguish installed from authenticated;
- avoid silently copying CLI credentials into unrelated child processes;
- show actionable status to the user;
- fail closed when the CLI is unavailable.

## Connectors

Connectors can expose external services such as mail, calendars, files, source control, and knowledge systems.

![Connectors](../assets/overview/connect-tools.png)

A connector implementation should define:

- authentication mechanism;
- scope/permissions requested;
- credential storage boundary;
- token refresh/revocation behavior;
- network destination policy;
- artifact/file behavior;
- error and reauthorization behavior.

## Custom provider URLs

User-supplied provider endpoints are security-sensitive. They must pass URL safety checks that account for:

- scheme restrictions;
- DNS resolution;
- loopback/private/link-local/reserved ranges;
- redirects;
- IPv4-mapped IPv6 and encoded address forms;
- credential forwarding across redirects;
- deployment-level egress restrictions.

## Release documentation rule

Public docs should describe only integrations actually intended for that release. Experimental or internal adapters should remain undocumented or clearly marked as unavailable.
