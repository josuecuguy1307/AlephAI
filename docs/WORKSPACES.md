# Workspaces

Aleph uses specialized workspaces on top of a common application shell.

## Workspace contract

Every workspace should preserve these product-level invariants:

- common Aleph navigation and session framing;
- consistent composer/input behavior when chat is present;
- explicit workspace identity;
- predictable artifact opening and file handling;
- consistent model/tool selection semantics;
- clean behavior for a first-time user with no existing sessions;
- no dependency on developer-specific local state.

## Science

Science supports research and evidence-heavy workflows. Typical surfaces can include scientific files, molecule/structure viewers, plots, code-assisted analysis, and structured scientific artifacts.

![Science workspace](../assets/hero/science-dark.png)

## Education

Education supports guided study, explanations, exercises, and learning artifacts. It should remain a real workspace rather than a thin themed chat screen.

## Office

Office focuses on productive document work: documents, spreadsheets, presentations, tables, and file-centric workflows. Rows, cells, pages, tables, and sheets should remain meaningful product units rather than decorative previews.

## Finance

Finance supports market analysis, backtests, run reports, metrics, charts, trading/portfolio views, and finance-specific agents or tools.

![Finance workspace](../assets/workspaces/finance-light.png)

## Legal

Legal supports matters, documents, templates, workflows, review, and jurisdiction-aware organization.

![Legal workspace](../assets/workspaces/legal-light.png)

## Design

Design supports iterative visual work, generated assets, editing requests, and design-specific artifacts while remaining inside the shared Aleph workspace frame.

## The Workshop

The Workshop is not a seventh domain workspace. It is a system-level composition environment for agents, tools, and pieces that can connect capabilities across the product.
