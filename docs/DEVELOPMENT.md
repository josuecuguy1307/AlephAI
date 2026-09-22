# Development

Aleph was built through a combination of human programming and AI-assisted programming, under human direction.

Product architecture, interaction design, integrations, testing, and release decisions are human-led.

## Working principles

- work from the canonical production source, not historical worktrees;
- keep changes narrow and reviewable;
- preserve existing workspace contracts unless the task explicitly changes them;
- avoid machine-specific paths and one-off local patches;
- do not package developer sessions, credentials, caches, browser profiles, logs, or local databases;
- distinguish source tests from packaged-bundle validation;
- keep generated artifacts and large build outputs outside the documentation/release repository.

## Typical source areas

```text
product/       product UI and backend behavior
platform/      runtime and shared capability boundaries
deploy/        build, shell, packaging, release recipes
qa/            release/boundary verification
third_party/   integrated upstream components
```

## Before editing

1. identify the owning runtime boundary;
2. identify existing tests and release checks;
3. inspect unrelated local modifications and preserve them;
4. determine whether the change affects the packaged bundle;
5. decide whether a rebuild is mandatory.

## After editing

At minimum:

1. run focused tests for the changed boundary;
2. run syntax/type/build checks relevant to that component;
3. inspect the diff for unrelated edits;
4. if runtime/package behavior changed, rebuild the desktop application;
5. validate the resulting bundle.

## UI development

The six workspaces should maintain a shared Aleph shell. Avoid creating isolated product shells for individual domains unless a deliberate architecture decision requires it.

## Security-sensitive changes

Changes to OAuth, filesystem operations, local process spawning, guest execution, connector URL handling, browser proxying, native/Tauri commands, or artifact rendering require targeted regression testing and should be treated as trust-boundary changes.
