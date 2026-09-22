# Release Process

Aleph release work is bundle-first: the release candidate is the packaged application, not a source checkout.

## Release sequence

1. Freeze intended source changes.
2. Run focused tests for recently changed boundaries.
3. Build into a new isolated output directory.
4. Do not reuse an incomplete previous bundle as the final candidate.
5. Verify signing and packaged resources.
6. Run clean-user, sanitization, secrets, and runtime gates against the produced bundle.
7. Perform a manual smoke test of the installed prefinal candidate.
8. Package distributables and checksums.
9. Update release notes/documentation.
10. Publish only after explicit release approval.

## Build

The internal production source currently uses a macOS build recipe under `deploy/fase4/`.

A typical internal invocation resembles:

```bash
bash deploy/fase4/build_app.sh public
```

Exact environment variables and toolchain paths are release-machine specific and should not be copied into public documentation.

## Required final gates

A release candidate should not be considered final until applicable gates are green:

```text
Build                         PASS
codesign deep/strict          PASS
Clean user                    PASS
Sanitization                  PASS
Secrets classification        PASS
Personal paths                0
Unclassified secrets          0
Onboarding                    PASS
The Workshop                  PASS
6/6 workspaces                PASS
OAuth                         PASS
Python guest                  PASS
Browser/proxy                 PASS
Filesystem regressions        PASS
Artifact regressions          PASS
OfficeCLI (when packaged)     PASS
```

## Sanitization

The packaged application must not contain:

- developer home-directory paths;
- personal hostnames;
- user conversations/sessions;
- authenticated connectors;
- private API keys/tokens;
- local documents;
- browser profiles;
- application support databases copied from a developer machine;
- private build logs/backups.

Fixtures must be synthetic.

## Packaging

The release repository can publish a `.dmg`, `.zip`, or other approved distributable plus a checksum file such as `SHA256SUMS`.

The exact release formats should be decided per release. Do not publish a bundle merely because the build succeeds; the validation gates above must be complete.

## Source/license wording

Do not claim that source is available under a license unless the corresponding source is actually published under that license. Documentation and binary distribution can exist independently from source publication.
