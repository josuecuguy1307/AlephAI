# Troubleshooting

This document is for maintainers debugging build and validation failures.

## Build succeeds but packaged app fails

Treat the packaged bundle as the source of truth. Common causes include:

- resources copied into the wrong bundle location;
- runtime data files omitted from packaging;
- nested helpers re-signed without required entitlements;
- sidecar executable/resource path differences between source and bundle;
- build tools using an unexpected package-manager or runtime version.

## Signing failure

Verify the failing executable independently. Nested helpers can require their own entitlements; the outer `.app` signature does not automatically grant them.

## Browser works in source but not in bundle

Check packaged runtime resources, ICU/data files, executable paths, and proxy arguments. Validate both the allowed control case and the blocked security case.

## Clean-user failure

Look for assumptions about an existing HOME, Application Support state, cached sessions, connector credentials, user files, or browser profiles.

## Sanitization failure

Search the actual bundle bytes for developer usernames, home paths, build output directories, hostnames, and local metadata. Fix the build or source cause rather than manually editing the final `.app`.

## Secret-scan candidates

Classify every candidate. A release gate should distinguish at least:

- real private secret;
- synthetic fixture;
- placeholder;
- public key/public web token;
- vendor/example material;
- hash/integrity value;
- false positive.

Do not mark the gate complete while candidates remain unclassified.

## Local test failure in sandboxed tooling

Separate environment restrictions from product regressions. A test that requires binding sockets or writing outside the allowed workspace can fail because of the tool sandbox; reproduce in an appropriate controlled environment before treating it as a product failure.
