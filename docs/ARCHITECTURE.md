# Architecture

Aleph is a desktop AI work environment built as a set of explicit runtime boundaries rather than a single monolithic chat application.

## Architectural goals

- keep workspace UX consistent while allowing domain-specific implementations;
- avoid coupling the product to one model provider;
- separate privileged local capabilities from web/UI content;
- make external connectors explicit and revocable;
- isolate code execution from the host where possible;
- package the actual product as a reproducible desktop bundle;
- validate the packaged bundle, not only the source tree.

## High-level components

### Desktop shell

The desktop shell owns the application window, native lifecycle, packaged resources, sidecar launch, and privileged desktop boundary.

The current macOS shell uses Tauri-based packaging in the production source tree.

### Shared workspace shell

Workspace UI should preserve a common Aleph frame: navigation, session context, input/composer behavior, model/tool selection, artifacts, and workspace identity.

Domain workspaces may provide different internal surfaces, but they should not invent unrelated application shells.

### Backend/application sidecar

The local backend coordinates product APIs, workspace state, connectors, session behavior, artifact routing, and privileged local capability mediation.

The production source tree contains Python/FastAPI services packaged into the desktop application.

### Browser boundary

Browser and web-facing capabilities must not receive unrestricted access to the host or loopback network. URL validation, redirect handling, DNS/IP classification, and explicit loopback exceptions are security-sensitive parts of the runtime.

### Execution boundary

Python and shell execution are treated as a separate trust boundary. On macOS, current release work uses an isolated guest Linux runtime backed by Apple's Virtualization.framework rather than falling back to unrestricted host execution.

### Filesystem boundary

Filesystem operations must resist path traversal, symlink escape, and time-of-check/time-of-use races. Path validation alone is not sufficient for privileged operations.

### OAuth and connector boundary

OAuth flows need explicit state/nonce/capability handling, loopback listener restrictions, redirect checks, and log redaction. Connector credentials must not leak into child-process environments or release artifacts.

## Source-tree orientation

Internal production source has historically been organized around:

```text
product/       product applications, backend routes, workspace UI
platform/      shared runtime, safety, execution, browser, inspection
 deploy/       packaging, shell, release scripts, frozen sidecars
third_party/   selected integrated upstream projects/components
qa/            release and boundary verification
```

Do not treat `third_party/` as first-party application code. Only components actually packaged and reachable in a release belong in release threat modeling.

## Workspaces

The six domain workspaces share system-level primitives but diverge in domain content:

```text
Aleph shell
├── Science
├── Education
├── Office
├── Finance
├── Legal
└── Design
```

The Workshop sits above/beside these as a composition surface for capabilities and agents.

## Artifact model

Artifacts are outputs that outlive a single model response: files, documents, charts, datasets, code results, structured domain objects, and previews.

Artifact renderers should be treated as potentially hostile-content boundaries. A rendered artifact must not silently gain native or same-origin authority.

## Release architecture

The release artifact is the packaged desktop application, not the source checkout. A change is not considered release-safe only because unit tests pass in source. The bundle must be rebuilt and revalidated after source changes that affect runtime behavior or packaging.
