# Privacy — Technical Notes

This file documents engineering expectations for data handling. It is not a jurisdiction-specific privacy policy or legal notice.

## Release artifact hygiene

A shipped Aleph application must not include developer or test-user personal state. In particular, release bundles should be checked for:

- conversations and session history;
- authenticated connector state;
- API keys/tokens;
- local documents;
- browser profiles;
- developer usernames/home paths/hostnames;
- private databases and logs;
- Application Support data copied from a development machine.

## External services

When a user enables an external model or connector, data handling is also governed by that service and the scopes/credentials the user authorizes. Release-specific documentation should state which integrations are actually available.

## Local state

Aleph may maintain local application state required for sessions, workspaces, artifacts, or connector configuration. Engineering should minimize unnecessary persistence and keep sensitive state out of logs and public release artifacts.
