# Contributing

Aleph development should favor narrow, evidence-backed changes over broad rewrites.

## Before opening a change

- identify the owning component and trust boundary;
- check for existing local modifications;
- avoid unrelated formatting/refactors;
- add or update focused tests;
- document any release-gate impact.

## Pull requests

A useful change description includes:

- problem being solved;
- affected product/runtime boundary;
- files/components changed;
- tests executed;
- whether the packaged application must be rebuilt;
- screenshots for visible UI changes;
- known limitations.

## Security-sensitive code

Changes involving auth, OAuth, connectors, browser/network policy, local services, files, process spawning, execution isolation, or native commands should include explicit regression tests for the security boundary being modified.
